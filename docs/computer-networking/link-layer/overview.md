---
sidebar_position: 1
---

# Overview

While the network layer is concerned with routing packets throughout the network, the link layer is concerned about getting a frame from one node to another.

On routers, the link layer is implemented on it's line card. On end hosts, the link layer resides on the **network interface card**. Most of it's functions being implemented in hardware.

## A Good Analogy

Let's say someone wants to go to Madrid, Spain, and lives in San Clemente, CA. That person is lazy, so it goes to a travel agent so he can figure out everything. The travel agent says the best way to go is to get a limo from San Clemente to LAX, get a flight straight to Madrid, then once he's there, take the train to get to the 5 star hotel. The agent then books everything. Is the responsibility of the limo company to get the person to LAX, is the responsibility of the airline company to get the person to Madrid, and so on with the train company. In this analogy, the travel agent is the routing algorithm, the person is a datagram, each transportation segment is a link, and the transportation mode is a link-layer protocol.

## Services Provided by the Link Layer

The basic service that the link layer provides is getting a frame from a node to another through a link, besides that, here are a couple of other services that can be provided by the link layer:

- _Framing_: Almost all link-layer protocols encapsulate each network-layer datagram inside of a **frame**, the frame format depends on the link-layer protocol.

- _Link Access_: It provides access to the links connecting nodes on the network, and it does so using **medium access protocols (MAC)**. Note that if the link only connects two nodes, there isn't an actual need for a protocol, the nodes can send data to each other whenever they want, however, if many nodes share a common link, there must be some kind of protocol to manage link access.

- _Reliable Delivery_: The link-layer can provide reliable delivery (just like TCP). This is common when the link is not very reliable, like WiFi, where data may get lost frequently. When using physical link, the overhead of implementing reliable delivery it's not worth the overhead, because it's less likely that data will get lost through the physical link, in this cases it's usually a best-effort delivery service.

- _Error detection and correction_: Data going through links may get corrupted due to electromagnetic noise, and so the link layer can provide error detection, and in some cases even correct the error.

## Error Detection and Correction Techniques

As stated above, the link-layer can provide error detection, and correction services, it's time to talk in more practical terms to see how these get actually implemented

### Parity Check

This is a very simple way (but not 100% effective) to detect if data was corrupted. It can simply calculate the parity of 1s in the data, and store it on the frame's header. If the parity doesn't match on the receiving link, the data must've gotten corrupted somehow.

As you may have guessed, the flaw of this method is that data can get corrupted, and still maintain it's parity, which then it would go unnoticed (even worse!). A way to get around this is to calculate a more complex type of parity the **two-dimensional parity**. With this, the receiver can not only detect the errors more accurately, but also correct them.

### Checksum

Just as the network layer has the IP checksum, link layer frames also implement checksums to detect bit errors. As stated previously, this don't detect errors 100% of the times.

### Cyclic Redundancy Check

Cyclic redundancy check uses polynomial equations, and modulo arithmetic kung foo to detect errors on the data.

## Multiple Access Links and Protocols

Multiple access links are links which multiple routers share, and so there must be a way to mediate how much each router gets to use the link, while optimizing resources, and performance. A good analogy for this is a busy cocktail party, where people are talking (sending data, and the medium would be the air). Multiple Access Protocols can be divide into three categories:

### Channel Partitioning Protocols

On channel partitioning protocols, the link is divided between the nodes either using time slots, or bandwidth. Each node gets a period of time to send data. In the cocktail party analogy, this would be equivalent to everybody having a fixed amount of time to speak while others listen (or pretend to do so).

This way seems very appealing because it avoids collisions, and seems very fair. However, there are two major drawbacks to this approach. First, a node is limited to the time slot even when is the only one who has data to send. Second, a node must always wait for it's turn on the transmission sequence. This can lead to a lot of unused resources. Following the analogy, this would be a party where only one person has a whole lot to say, and all the others just want to lister, having periods to talk on this scenario wouldn't work very well.

### Random Access Protocols

On random access protocols, when nodes sense there's no flow of packets going through the channel, they start sending their packets after some random interval. Note that because nodes wait for the channel to be free before starting sending data, the randomness gets a node to start first most of the times, and so the others keep waiting.

If a collision between two nodes happen, they both stop sending, wait a random interval, and then resend their frames again, one of the nodes is going to start sending data first, which will lead the other to wait for the channel to be free again.

This leads to better resource usage then channel partitioning methods, as the nodes enjoy the full bandwidth of the channel.

### Taking-Turns Protocols

On taking-turns protocols, each node is scheduled to have the channel to transmit a maximum amount of frames. If the node doesn't have any frames to send, then is passes it's turn to the next one.

## Switched Local Area Networks

Switched local networks switches work on the link-layer level, and they switch frames through the subnet, instead of datagrams. They don't recognize IP addresses, or network layer routing protocols, this means that there must be some other way of addressing this frames through the subnet.

### Link Layer Addressing

Enters link layer addresses, or **MAC addresses**. These work on the link layer level, each host and router in the network has a unique MAC address (being more precise, each network adapter/interface on the network has a unique MAC address). This can lead to some confusion, why are there two addresses, IP and MAC? Do we really need those two?

As you may imagine, we do need it, and a good analogy to think about them is to see the MAC address as a social security number, you can't really change it, while the IP address is equivalent to a home address. You may change your address, but you won't change your social security number. Following this analogy, the IP address of a host may change when he joins a different network, however his MAC address will not change.

MAC addresses are flat (as opposed to hierarchical as IP), and each network adapter gets a unique one. They look something like this: `49-BD-D2-C7-56-2A`.

### Address Resolution Protocol (ARP)

Because of these addressing situation, there's a need to **translate between IP and MAC addresses**, the internet does this using Address Resolution Protocol (ARP).

ARP sits between the network-layer and the link-layer.

#### Sending Frames Within a Subnet

Whenever a host wants to send frames to another host on the same subnet, it must have it's MAC address. To find out the receiver's MAC address, the sender gives it's network adapter the receiver IP address, and the ARP module resolves that IP address into a MAC address, with the IP, and the MAC address, the sender can now send the data.

The ARP module on an adapter resolves the MAC address by either looking at it's ARP table, where it keeps a list of IP address mapped to MAC address, and if it's not there, it then broadcasting and ARP packet through the subnet, the receiver seeing that the ARP packet contains it's IP address, it sends back an ARP packet to the sender with it's MAC address. This broadcast process is equivalent to someone shouting out at work: "What's the social security number of the person who lives at address X?"

#### Sending Frames Outside a Subnet

To send frames outside of the subnet, the host must set the MAC address to the **gateway router of the subnet**, not to the receiving host (note that the IP address is still the receiver address). Once the frame reaches a router, the datagram is extracted from the frame, and gets processes by the router's network layer by checking against forwarding table, and sending the datagram to the correct output network adapter, the network adapter then frames the datagram again, and moves it forward. This happens until the destination is reached (or not!).

## Ethernet

Ethernet is the protocol (actually a standard of many protocols, but for simplicity...) that embodies the topics discussed above.

It can be said that Ethernet has been for local networks, what the internet has been for global networks.

It provides a connectionless data transfer between nodes, and it uses CSMA/CD protocol for shared broadcast channels. which is a random access protocol.

### Ethernet Frame Structure

![Ethernet Frame Structure](/img/docs/ethernet-frame.jpeg)

- _Preamble_: a sequence of bytes meant to "wake up" the receiving adapters.
- _Addresses_: self-explanatory.
- _Type_: used to specify the service at the layer above, which most of the time it's IP. This is similar to the IPv4 protocol field, glueing together the link and network layers
- _Data_: payload (46 to 1500 bytes).
- _CRC_: used for Cyclic Redundancy Check (error detection). Once the receiver gets the data, it checks CRC to see if the frame was corrupted, if it was it simply drops the packet, never warning the receiver (as mentioned before, on the internet the reliability gets implemented on the transport layer).

## Link-Layer Switches

Link-layer switches are used in LANs. They're very similar to routers, but while routers act on the network-layer forwarding datagrams (using IP addresses), link-layer switches forward, and filter link-layer frames (using MAC addresses).

This switches maintain a self-learning table mapping MAC addresses to it's own network interfaces. Once it receives a frame from a sender it stores the sender's MAC address + the interface the frame came into into it's switch table, and then it does one the following:

- If the destination address is in the switch table, and the interface where the frame came from it's the same where it's supposed to go to, it drops the frame.
- If the destination address is in the switch table (and it's not the interface it came from), it forwards the frame to the receiver's respective interface.
- If the destination address is not in the switch table, it broadcasts the frame to all interfaces except the one it received the frame from.

Link layer switches are useful because they're self-learning, the switch tables are built on the go, requiring less manual setup, being **plug-and-play**. Another appealing benefit are:

- _Elimination of Collision_: because the switcher have buffers, and manage the frames, it avoids collisions on it's interfaces, improving the local network's performance considerably
- _Heterogeneous Links_: switches allow links of different bandwidth to be used together, being ideal for mixing up legacy equipment with new equipment
- _Management_: in addition to providing enhanced security, link-layer switches can detect to some extent malfunctioning interfaces, and simply disconnect them, avoiding the network manager to have to do that manually.

In general, a link-layer switch will suffice for small LAN's, but for bigger LAN's with thousands of hosts, routers + additional link-layer switches will be required.
