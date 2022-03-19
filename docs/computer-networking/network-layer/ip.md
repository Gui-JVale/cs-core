---
sidebar_position: 3
---

# IP

## Overview

The Internet's network layer is basically composed of three main components: the IP protocol, routing protocols, and an error reporting protocol (ICMP).

Internet Protocol (IP) is specifically **how the Internet's network layer manages addressing, and forwarding**. Today, there are two versions of IP, IPv4, and IPv6.

## IP Datagram Format

As the transport layer has _segments_, the IP protocol payload is a **datagram**, and it looks like this:

![IP Datagram](/img/docs/ip-datagram.png)

- _Version_: IP's version number, can be 4 for IPv4, or 6 for IPv6.
- _Header Length_: IPv4 header datagram can have variant sizes due to allowing options to be specified. So this field is needed to account for that, allowing datagrams to be processed correctly. It's important to note that this varying size of the header creates overhead computations in routers, so the options field was dropped on IPv6.
- _Service Type_: The Internet's designers created this field having in mind packets that could have different kinds of services, for example packets carrying voice-over IP data, or live streaming (whose services need packets arriving continuously) could take priority over packets containing a request for an web page.
- _Total Length_: Total length of the datagram (header + data).
- _Identification_, _Flags_, and _Fragment Offset_: This fields are used for packet fragmentation (described below).
- _Time To Live(TTL)_: This field is used to avoid a packet going through infinite loops. When a router gets a packet, it must decrease the TTL field. Once a router receives a packet with the datagram's TTL field set to 0, it must drop the packet, cause it could be stuck in an infinite loop.
- _Protocol_: This field is used only on end hosts, and specifies the protocol used on the layer above (transport layer). This would be set to TCP, or UDP. Note that, just as port numbers glue the application layer with the network layer, this field glues the network layer with the application layer.
- _Checksum_: A checksum of the datagram's header, this is used for detecting errors.
- _Source IP Address_, and _Destination IP Address_: This fields are used by routers to route the datagram across the network. The routers use the **longest prefix match**, to find the correct output entry on their forwarding tables.
- _Options_: With IPv4, it's possible to extend the header with extra options.

## IP Fragmentation

It can happen that a datagram is bigger then what a router's link-layer frame can take, whenever this happens, the datagram must be fragmented into smaller datagrams to chunk up the data to fit a frame.

Because of this, fragments must be restored into their original form before getting send to the transport layer. The Internet's designers thought that this would introduce a lot of overhead in routers, so the job of reconstructing a datagram based on it's fragments occurs on end hosts network layer.

The way it works is by using the identification, flags, and fragmentation offset fields of the datagram's header. Each datagram that's sent to the same destination IP address, has a unique identification number (which gets iterated every time a datagram is sent). Whenever an end host receives datagrams with the same coming from the same source address, with the same identification number, it knows the datagrams got fragmented somewhere along the way, so it must reconstruct it back together, so it must know that it has all fragmented datagrams, and it must know when the fragments end. To allow for this, each fragmented data has a fragment flag set to 1, with the exception of the last fragment which has this bit set to 0, each fragmented datagram has a fragmentation offset field set. This allows the end host to know when the last fragment arrives, and it any got lost along the way.

Because of the overhead introduced by this mechanisms, fragmentation isn't allowed in IPv6.

## IPv4 Addressing

Before talking about addresses, it must first be said that usually hosts have only one link to the network, and the boundary between the host, and this physical link is called an interface.

IP Addresses are how devices connected to the internet are identified, they are similar to normal street addresses in the way that they have a specific format, people can change addresses, and one person only has one (unique) main address. However, each interface connected to the internet must have an IP address to receive, and send data to the network. This means that routers, because they have many interfaces, must also have just as many IP addresses.

IPv4 addresses consists of 32 bits (or 4 bytes), this means that there can only be 2^32 unique IP Addresses, or 4 billion addresses (which as you may have guessed, it's not enough). They're represented in **dotted-decimal notation**, for example the IP address 193.32.21.9 looks like this in binary format:

`1100001 00100000 11011000 0001001`

It must be reinforce that every interface (and so device) connected to the internet must have a unique IP address, with the exception of devices sitting behind a NAT (which is explained below).

Devices withing a subnet have very similar IP addresses, and so there's another notation that's used to define the most important bits used for routing, this notation is a.b.c.d/x, with x being the most significant bits of the address (and consequently the ones that routers will use to lookup on their forwarding tables). To make it more clear, let's look at an example: an organization has a subnet identified by 192.86.92.0/24, this means that router will look at 192.86.92 to address the packets going to devices on that network. It also means that devices in that subnet have addresses like 192.86.92.1, 192.86.92.2, 192.86.92.54, etc. So once inside the subnet, the Local Network (LAN) uses the 32-x bits to take care of forwarding the packets to the correct host.

### Obtaining Blocks of IP Addresses

To obtain blocks of IP addresses to be used inside an organization, the company must reach out to its ISP, but the ISP must also get those blocks from somewhere. The management, and allocation of IP addresses is handled by the global public authority ICANN. And so once an organization has blocks of IP addresses, it can assign to devices through it's subnet.

### Obtaining Host IP Address

Once an organization has blocks of IP addresses, it can manually distribute them, however this gets mostly handled automatically with **Dynamic Host Configuration Protocol (DCHP)**.

DHCP is widely used because it's plug-and-play, not requiring manual configuration. Hosts talk to a router DHCP server, and then they get an IP addresses given by the router. This is basically what happens whenever you join a network this days.

### NATs

Network Address Translation, or NAT is a router that sits between the internet, and a local network. It provides the job of abstracting IP addresses, that is, devices sitting behind a NAT don't need to worry about their IP address colliding with the outside world (the only unique address being the NAT itself), and so this doesn't restrict the number of devices to the number of IP addresses given to the organization, now there can be many more devices.

The NAT then translates addresses from datagrams coming in, and going out of it's network. It does this using a **NAT translation table**. To illustrate this, let's say a user sitting with the private address 10.0.0.1, siting behind a NAT, wants to request a Web Server for a Web page (port 80). It creates a packet with the Web server as the datagrams destination address, with it's own private IP address as source address, on the TCP segment, it puts 80 as destination port number, and the arbitrary source port number of 3345. When this packet gets to the NAT, the NAT changes it's source IP address with the NAT's own IP address, and changes the port number with an arbitrary port number that's not currently in use in the NAT translation table, it then creates a record on the table with the key consisting of these two fields it changed on the datagram (source IP address, and new port number), and as value it puts the private host IP address, and original port number. Now the NAT can use this table to translate packets received to the private addresses that it manages.

NATs have enjoy wide deployment in recent dates. It must be said, however, that there are many people who are against it, arguing that IP addresses should be used for addressing, not port number, and that NATs violate the layer abstraction by using the transport layer port numbers, as well as violating the internet's end-to-end principle of letting hosts communicate with each other. It also can interfere with P2P communication.

## IPv6 Addressing

## Interoperability Between IPv4 and IPv6
