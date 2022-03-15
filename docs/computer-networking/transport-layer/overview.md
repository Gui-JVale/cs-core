---
sidebar_position: 1
---

# Overview

The transport layer sits between the application layer, and the network layer. It provides the **abstraction of having logical process to process communication between two end hosts**, using with multiplexing, and demultiplexing with port numbers.

This layer can provide reliable data transfer, security, throughput, and timing guarantees.

Sitting on top of the network layer, it extends it's services. While the network layer provides host to host communication, the transport layer provides application layer process to process communication.

A transport layer payload is called a _segment_.

The transport layer (as the application layer), is **implemented on the end hosts, not on the network's core**. That means that **routers do not implement this layer**, their implementation go from the network layer to the physical layer. This also implies that the **transport layer segments is encapsulated inside a network layer payload** (called datagram).

## Transport Layer in the Internet

The two transport layer services available on the Internet are TCP, and UDP. A thing to keep in mind about the **network layer on the Internet is that it's a best-effort delivery service**, meaning that packets may be lost/dropped, and may also arrive out of order, or be corrupted.

### TCP

TCP is a connection-oriented protocol that provides reliable data transfer between two processes, control flow, and congestion control. Most of the applications use TCP, because of it's guarantees and services.

Observe that TCP provides reliable data transfer on top of a non-reliable service (the network layer).

All the added features provided by TCP don't come at no cost, TCP is less performant and way more complex to implement than UDP.

### UDP

UDP is connectionless protocol that doesn't provides many guarantees, and it doesn't really add much on top of the network layer, besides the logical communication between processes.

UDP doesn't guarantee data delivery (packets may get dropped, and won't be retransmitted), and packets may arrive out of order. However, it does provide error checking.

DNS uses UDP.
