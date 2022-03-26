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
