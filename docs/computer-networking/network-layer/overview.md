---
sidebar_position: 1
---

# Overview

## Introduction

The network layer is arguably **the most complex layer** on the stack. While the transport layer is concerned with providing logical communication between two processes on two end hosts, the network layer is responsible for providing this **communication between the two end hosts** (not a trivial task at all!). Unlike the transport layer, there's a piece of the network layer in every device on the network, not only on the end hosts.

Thus, the network layer is comprised of end hosts, packet switches (routers), and routing algorithms (that are used in routing protocols). This layer is responsible for **forwarding, and routing packets**.

## Forwarding and Routing

**Forwarding** means moving a packet from one router interface to the next, making sure that this hop on the network is getting the packet closer to it's destination. In practice this happens through forwarding tables kept by inside of each router.

**Routing** is more concerned with the bigger picture, routing a packet from host A to host B. In practice, this gets done by fancy routing (graph) algorithms.

As you imagine, these two go hand in hand.

## Network Service Models

The network layer can provide countless services. Here are a few of them:

- Guaranteed delivery
- Guaranteed delivery with bounded delay
- In order packet delivery
- Guaranteed minimal bandwidth
- Guaranteed maximum jitter
- Security services

The Internet is a best-effort delivery service, so it provides none of these services out-of-the-box. However more complex networks, like ATM, do provide these services

## Virtual Circuits (VC) Networks vs Datagram Networks

The network layer be classified into being a VC network, or a datagram network.

VC networks are stateful, because the maintain a virtual circuit between two hosts. Parallels can be draw with the TCP transport layer protocol.

First it establishes a virtual circuit between two hosts by setting up a connection, then the data exchange happens, and at a last a connection teardown.

Datagram networks are stateless, they don't setup and teardown connections. By using routing algorithms, and forwarding tables, the network routes the datagrams from host A to host B. Note that here, datagrams going from host A to host B can take different paths through the network.

As you may have imagined, VC networks are more complex to implement, while datagram networks are simpler. This is a big reason why the Internet is a datagram network, it was built with simplicity in mind.
