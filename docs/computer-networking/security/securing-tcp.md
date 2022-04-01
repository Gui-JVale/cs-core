---
sidebar_position: 6
---

# Securing TCP: SSL

## Introduction

Now that we've seen security in the application layer, specifically on email, let's go a layer deep, and see how security is implemented in the transport-layer. Just as a quick overview, the transport-layer is the one responsible for providing logical communication between two processes running on different end hosts.

We'll see that many of the principles and cryptography practices that we covered are also used to provide security in this layer. In practice, the most popular and widely used security protocol the transport layer is **Secure Sockets Protocol (SSL)**, and there's a version of it called **Transport Layer Protocol (TLS)**, both running over TCP. SSL is widely used these days in the client-server model, most websites being required to use **HTTPS** (as opposed to plain HTTP). HTTPS is a version of HTTP that uses the SSL protocol, providing security. In the early days, mostly e-commerce websites were required to use HTTPS, due to the sensitive data share between client and server.

Theoretically, SSL sits just in between the application layer, and the transport layer, and handles **confidentiality**, **message integrity**, and **authentication**.

## The Bigger Picture

Let us first get a look at the big picture scenario before going into the technical details, for that we'll go over an almost-SSL protocol to get the hang of it, and after that we'll discuss further details.

As always, let's use the Alice, Bob, and Trudy example, where Alice is the server, Bob is the client, and Trudy is attempting a man-in-the-middle attack.

### Connection Setup

Alright, so let's get to it, let's see how a SSL connection get's established:

1. The TCP connection gets setup, with the three-way handshake we already covered.
2. Bob (client), sends a SSL hello message to Alice (server), which she answers with her certificate (remember that a certificate is issued by a CA, and binds a public key to an identity).
3. Bob gets Alice public key from her certificate, and proceeds to generate a Master Key _MS_, that will be used for symmetric encryption during this session.
4. Bob encrypts MS with Alice public key, and sends it over to her.

### Key Derivation

After that, both Bob and alice have _MS_, so one may think that they can just use that to encrypt the data, and use a well-known encryption hash function to get message integrity. SSL goes a step further to provide another layer of security, the MS is used to divide 4 different keys, this can be done by just diving the key into 4 pieces, those being:

- E<sup>b</sup> = session encryption key for data sent from Bob to Alice
- M<sup>b</sup> = MAC session key for data sent from Bob to Alice
- E<sup>a</sup> = session encryption key for data sent from Alice to Bob
- M<sup>a</sup> = MAC session key for data sent from Alice to Bob

### Data Transfer

Now that both Bob and Alice share the same four keys, they can start sending data.

As we saw, data shared between two processes are just a stream of bytes. One may think that a way providing security is to wait for all the data to arrive from TCP, and then worry about security. That's really inefficient, and isn't robust. Instead, SSL breaks the data into _records_, for simplicity, it can be thought that one record gets encapsulated inside one TCP segment (in practice this may no be the case). So then for Bob to send data to Alice, he breaks it up into records, appends the MAC to the end of each record for message integrity, and uses E<sup>b</sup> to encrypt the record's data + MAC. To compute the MAC for each record, Bob passes into a hash function the record's data and his MAC session key M<sup>b</sup>.

Now even though we have confidentiality, this is still flawed, because we don't exactly have message integrity. Can you spot the flaw? Sure each record gets message integrity, but the flow of segments as a whole don't. Trudy can sneak in, and change the order of the segments, and even their sequence number (which is not encrypted). And so we must take this into account, and also use sequence numbers in the SSL level.

To do that, Bob maintains a sequence number counter, which begins at zero and gets incremented with each record. Bob doesn't include the sequence number itself on the record, but includes in the MAC calculation. Thus, the MAC is now a hash of data + MAC key + sequence number. Alice also keeps track Bob's sequence numbers, allowing here to include it on her MAC calculation. If she notices the MAC doesn't match, she can tell something funny is going on, and terminate the connection.

### SSL Record

![SSL Record](/img/docs/ssl-record.jpeg)

This is the SSL record format (as well as almost-SSL). The type field is used to specify if the record is a SSL hello, a terminate session signal, or just contains data.

## A More Complete Picture

Ok now that we went over some of the basics, let's get more technical on how SSL actually works. First on the connection setup.

### SSL Handshake

SSL can run over different encryption algorithms and hash functions, as we'll see that gets chosen on-the-fly. Additionally, during the handshake phase, Alice and Bob share a nonce, so that Trudy can't just sniff the records, and replay them to Alice another day. Here's a look of the SSL handshake:

1. Client sends a list of the cryptography algorithms he supports, along with a nonce.
2. Server chooses a symmetric key algorithm, a public key algorithm, and a MAC algorithm, and sends his picks back to client along with his certificate, and a server nonce.
3. Client verifies the certificate, and extracts the public key, and proceeds to generate a Pre-Master Key PMS, it encrypts the PMS with the servers public key, and sends it over.
4. Using the same key derivation function (specified by the SSL standard), both client and servers use the PSM to generate the master key MS, and the proceed to slice the master key to generate the four keys that were explained above.
5. Client sends a MAC of all it's handshake messages
6. Server sends a MAC of all teh handshake messages

One may wonder why steps 5 and 6 are needed. Notice that data exchanged on step 1, and 2 are not encrypted, nor have message integrity, Trudy could, for example, intercept the first message from the client (with the list of algorithms), eliminate all strong algorithms, and send to the server. Steps 5 and 6 are needed to ensure all handshake messages were integral.

### Communication Closure

At some point, Bob and Alice will want to terminate the connection. One naive way to handle that is to simply use TCP's connection teardown mechanisms (sending a FYN segment). However, this leads to the obvious attack where Trudy can simply terminate a connection between Alice and Bob while they still have data to send. And so we need a more secure way of doing this.

To terminate a SSL connection, the client can set the field of the last record to terminate the connection, even thought that isn't encrypted, it would still get authenticated by the server because of the MAC.
