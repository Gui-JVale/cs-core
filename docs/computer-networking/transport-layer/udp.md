---
sidebar_position: 3
---

# UDP

## Overview

UDP is a **connectionless** transport layer protocol. It's extremely **minimal**, and doesn't provide many guarantees on top of the network layer best-effort delivery service. This means that data transfer between two hosts using UDP is **unreliable**. Packets may get lost, arrive out of order, and be corrupted.

So what's the point then? Well, as any transport layer protocol, it provides multiplexing, and demultiplexing, for process to be able to communicate with each other on different hosts. It also provides error checking through checksums.

It does just as little as a transport layer protocol can do, it doesn't maintain any state, this makes UDP way **simpler** than TCP, resulting in better **performance**.

Also UDP **doesn't provide flow, or congestion control**, so a host can just bombard another host (and by consequence, the network) with packets. UDP traffic can then block TCP traffic. Because of this, some firewalls block UDP packets altogether.

## UDP Segment Structure

![UDP Segment Structure](/img/docs/udp-segment.png)

- Source, and destination port numbers are used for multiplexing, and demultiplexing.
- Length is used for parsing the packet.
- Checksum is used for error checking

## Use Cases

You may wonder what kind of applications would use such a service, that provides so little. Here are a couple of factors that can make UDP more suited for an application then TCP:

- _Finer application-level control over when the data is sent_: TCP must first establish a connection, and it can throttle packets based on it's flow, and congestion control mechanists. UDP just sends packets as soon as it gets it.
- _No connection establishment_: TCP, before sending any data, must first establish a connection using a three-way handshake. UDP just sends data without any preliminaries, so there's no delay to establish the connection.
- _No connection state_: Because of it's simplicity, UDP doesn't need to keep track of any state. TCP on the other hand, every time a connection is established, both hosts must initialize TCP state variables.
- _Small packet header overhead_: While TCP segments have at a minimum 20 bytes, because of it's headers, UDP has only 8 bytes of overhead.
