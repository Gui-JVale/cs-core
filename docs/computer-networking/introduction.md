---
sidebar_position: 1
---

# Introduction

The content of this section is based on the book Computer Networking: A Top-Down Approach by James F. Kurose and Keith W. Ross.

## What is the Internet?

The internet is everywhere. Phones, desktop computers, laptops, tablets, smart watches, smart cars... the list goes on and on, but what is the internet itself? This thing that enables computers (and hence people) to communicate all over the globe?

The Internet is nothing but a (very complex) computer network that connects the entire world. It's not only a simple network, but a network of networks (recursion!), and as such, it must ensure that different hosts, routers, computers, operating systems, hardwares etc. all communicate with each other in a meaningful way. Now that's a daunting task, how would such a system deal with all the complexity that is connecting billions of diverse hosts around the world? Well, the internet's answer to the interoperability, and scalability that comes with the task can be summed up in two words: Layers and Protocols.

## A Layered Architecture

Layers and Protocols are the glue that holds the internet together, tackling all this complexity.

The internet can be divided into 4 layers:

1. Application Layer
2. Transport Layer
3. Network Layer
4. Link Layer

And each of this layers have their own set of protocols, and, for the most part, don't care much about the layer below.

On separate hosts that are communicating through the network, each layer talks with the layer at the same level, and each payload from the layer above gets encapsulated in the layer below. So a datagram from the Network Layer doesn't really know that it's carrying as it's payload a segment from the Transport Layer, and it doesn't care, it just provides it's services and moves own.

This design improves interoperability, while also making it versatile, a layer can provide different kinds of services (and guarantees) based on what the application's needs. For example on the Transport Layer, a application can choose between having a reliable connection with congestion and flow control using TCP, or a connection-less data transfer with not that many guarantees using UDP.

## The Network's Edge

At the internet's edges there are access point networks (local networks) that connects end hosts with the internet.

These local networks can be small, such as a residency network, consisting of only a few hosts and one router that connects the local network with the 'outside world', or it can be a much more complex network, such as a university network, for example, that has thousands of hosts and many routers.

The end hosts connect themselves to the routers, either through a physical link (cable) or a virtual link (WiFi), using protocols, and then are able to send and receive packets through the router(s) from the outside world.

Internet Companies are the ones who provide access to the internet, and they are called Internet Service Providers(ISP). ISPs are organized in a hierarchical fashion, there are regional ISPs, who provided services to the region, but must consume the services of a higher level ISP (such as a nation-wide ISP), and even those must consume the services of a global ISP.

## The Network's Core

At the network's core there are packet and circuit switches (routers), who take care of forwarding packets to their destinations

## Delay, Loss, and Throughput

### Delays

Delays in a network can be summarized by:

1. router delays:

- nodal processing delay
- queueing delay
- transmission delay
- propagation delay

2. Round-Trip Time(RTT), and the amount of congestion on the network

### Throughput

Throughput can be summarized by the amount of bytes per second that routers in the network can take, as well as the end hosts.

### Packet Loss

Loss happens when a queue of packets becomes too big in a router, overwhelming it's memory and causing the router to simply drop the packets.
