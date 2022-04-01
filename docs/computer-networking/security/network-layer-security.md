---
sidebar_position: 7
---

# Network Layer Security: IPsec

## Introduction

As with the other layers, security in the network layer is also based on cryptography, and many of the techniques already covered.

The protocol that provides security in the network layer is **IPsec**. Any two network layer entities can use IPsec to securely send/receive IPsec datagrams (this includes hosts and routers). This protocol can provide **confidentiality**, **message integrity**, **authentication**, and **prevent playback-attacks**. Because it's implemented in the network layer, it encrypts the datagram, and so any TCP or UDP segment, ICMP message, and any application layer data all become confidential (remember that with SSL, the TCP header was still exposed), and so it's said that IPsec provides "blanket coverage". Many institutions use IPsec to create **Virtual Private Networks (VPNs)** (described below).

IPsec can get complex as it has many official definitions and versions, using different protocols itself. Because of that, for simplicity sake we'll get deeper into a specific version of IPsec. The two most widely used protocols under IPsec suite are **Authentication Header (AH)**, and **Encapsulation Security Protocol (ESP)**. AH provides authentication, and message integrity, but it doesn't provide confidentiality. ESP provides message integrity, authentication, and confidentiality, because of that, we'll focus exclusively on ESP. After learning ESP, going after AH becomes way easier too. IPsec has also two different packet forms, **transport form** and **tunnel form**, because tunnel form is used more in practice then the transport from, we'll also focus exclusively on that.

## IPsec and Virtual Private Networks (VPNs)

Many institutions that have bases distributed around a region, or across the globe, may want to have their own **private network**, so that they can exchange sensitive data between themselves securely. To do that, they'd have to deploy many routers and infrastructure, which can become very costly. And so most companies use Virtual Private Networks to achieve the same goal, but at a much more cost efficient way.

To illustrate that, let's take a look at a small company that has a headquarter, a branch office, and _n_ traveling salespeople. The HQ has sensitive data, which shouldn't be shared with the rest of the internet, and while hosts inside the HQ can safely access that data through a LAN, how would the branch office, or the traveling salespeople access that data securely? VPNs come to the rescue.

Let's say a host at the office wants to communicate with a host in the HQ, and both the HQ and branch office have one gateway router. Those routers can simply use IPsec, and all data will enjoy confidentiality, message integrity, and authentication. As we'll see, IPsec creates it's own datagram (which is encrypted), and puts that inside a vanilla IPv4 datagram, and sends it over the network. The network routers will do their job, forwarding the datagram without even knowing that they are carrying an IPsec payload.

The same would happen if a traveling salesperson wants to communicate with a host in the HQ, except the IPsec entity would be the salesperson OS (as opposed to the branch office gateway router).

As you may have guessed, both gateway routers (and in fact any IPsec entity inside a VPN) must share state, specifically state that will be used for encryption/decryption, and other security practices, such as encryption keys, MAC keys and so on.

## Security Associations

When two network layer entities (being two routers, two hosts, or a host and a router) want to communicate using IPsec, they must first establish a network layer logical connection. This logical connection is called **Security Association (SA)**, and it's a simplex; meaning it's a unidirectional connection, and so if data must flow both ways, two SAs must be established.

Let's take a look 'inside' an SA. For that let's go back to the previous example, and say that a host on the HQ wants to communicate with a host in the branch office, in essence the HQ gateway router R1 has to communicate with the office branch gateway router R2, and so they establish an SA, and that SA has the following state:

- 32-bit field used to identify the SA, this is called the **Security Parameter Index (SPI)**
- The type of encryption used
- The encryption key
- The type of integrity check
- The authentication key

This state is kept in both IPsec entities that are trying to communicate securely, in this example, R1 and R2.

An IPsec entity (router or host) often maintains many information for many SAs, and for that it uses a special data structure called the **Security Association Database (SAD)**, which is implemented directly in the OS kernel.

## The IPsec datagram

As stated before, there are two packet formats for IPsec, transport and tunnel. We'll take a look at the **tunnel** mode.

![IPsec datagram format](/img/docs/ipsec-datagram.jpeg)

Ok to understand the IPsec datagram format, let's take a look at how it gets constructed. Let's say Alice is in the HQ, and want's to talk with Bob in the branch office. As we've seen, here the gateway routers take care of IPsec, so Alice just sends a vanilla IP datagram, and once in R1, is uses the following recipe to convert the vanilla IP datagram into an IPsec datagram

1. Appends at the end of the datagram and ESP trailer field
2. Using the encryption key, it encrypts the entire original datagram + the ESP trailer
3. It then appends to the front an ESP header field. The resulting package is called an _enchilada_.
4. Creates an authentication MAC over the whole _enchilada_, and appends it to the end of the enchilada
5. Creates a brand new IP header and appends it to the front of the enchilada.

Observe that the resulting datagram is a bona fide IPv4 datagram, and so it's routed through the internet as any other IPv4 datagram.

From this, we know that all the contents from the original IP datagram are encrypted, and how is the new IP header generate? We'll let's look first at the addresses, the original addresses were Alice's and Bob's IP addresses, the new IP header uses R1 and R2 interface IP addresses. Also the protocol field is now 50, to indicate it's an IPsec datagram, if the original datagram used TCP, the original IP header protocol field was set to TCP.

Now let's take a look at these ESP fields, starting with the **ESP trailer**. This field is used mostly for encryption purposes, it's composed of a padding field, a pad-length field, and a next header field. The padding bits are specific to how the encryption works, so we won't get into details. The next header field indicates the upper layer service used by the original datagram (TCP/UDP).

On to the **ESP header** field. This field is composed of the **SPI** to indicate the AS that's currently being used for the datagrams, and a **sequence number**, which is used to prevent playback-attacks.

And finally the **ESP MAC** or ESP Auth. That field is a mac over the whole enchilada, and it's used to provide authentication, as well as message integrity to the IPsec datagram.

So R2, upon receiving the IP(sec) datagram from R2, it sees that it's IPsec using ESP by the protocol field, and then checks the SPI to query the SA state. After that it proceeds to check the ESP MAC to make sure it was sent by R1, and it hasn't been tempered with. Then it checks the sequence number to prevent playback attack. Following that, it uses the SA encryption key to decrypt the payload + the ESP trailer. R2 has now the original IP datagram, it then checks it's header, and sees that it contains Bob's address as the destination, and so it forwards it to him. Phew, what a travel!

A subtle problem rises up: how does R1 and R2 know which datagrams should use IPsec (those communicating between branches), and which shouldn't (for example a request to google.com)? To solve that, IPsec entities also keep a **Security Policy Database (SPD)** alongside with SAD. So basically SPD tells what to secure, and SAD tells how to secure.

After taking a look at all that security stuff, you must be convinced that IPsec provides confidentiality, message integrity, authentication, and playback-attack prevention.

## IKE: Key Management in IPsec

One last bit that hasn't been talked about is how do the SA state gets there in the first place? How do these keys get setup? Well if the VPN is small enough, one can manually set that up in all the IPsec entities. However, if it spans across hundreds of hosts in multiple regions, we must do it automatically. To handle that we have another protocol, the Internet Key Exchange (IKE) protocol. IKE runs between two IPsec entities who want to exchange keys for an SA, and it occurs in two steps:

- First both entities exchange messages and setup bi-directional **IKE SA** using public key encryption (specifically Diffie–Hellman), which confusingly enough its different from an SA. This creates an authenticated and encrypted channel between two routers. During this phase, encryption keys are exchanged for the IKE SA, and a master key is exchanged for the IPsec SA.
- On the second phase, both routers prove their identities to each other by signing their messages, and the two sides negotiate encryption algorithms that will be used on the IPsec SA.
