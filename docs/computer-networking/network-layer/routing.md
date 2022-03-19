---
sidebar_position: 5
---

# Routing

## Overview

In this section we'll talk about how packets get routed, and how the internet does it. How does a packet get from point A to point B? This can be tricky to think about, because there isn't a centralized entity coordinating all packets on a network in live time, having an eagle vision of every node. Instead, packets get forwarded by routers on the network according to their forwarding tables, and so each router just knows about it's interfaces, and at each hop the packet (hopefully) gets closer to it's destination.

**Routing algorithms** are used to route packets through the network.

A good abstraction to think about a network is a graph, where each device on the network are the nodes, the hosts being the leaves, and the edges being the connections between those devices. With that in mind, you can imagine that **routing algorithms are essentially graph algorithms**.

The are basically two classes of routing algorithms, **centralized algorithms**, and **decentralized algorithms**.

## Algorithms

### Centralized

On centralized algorithms, a main host/device must have knowledge (global state information) of all devices (nodes) on the network, as well as their connections (edges), and the weights of those connections. It then runs a graph algorithm (usually [Dijkstra's algorithm](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm)) to figure out routes on the network. In practice, this is the **Link-State Routing Algorithm (LS)**.

### Decentralized

On decentralized algorithms, devices on the network talk to each other, and in a distributed, and iterative manner, end up building routes with this type communication. In practice, this is the **Distance-Vector Routing Algorithm (DV)**.

:::note
For further details on this algorithms see Computer Networks: A top-down approach.
:::

In practice, both algorithms are used in the internet.

## Hierarchical Routing

There are a couple of issues when trying to just LS or DV to route an entire network. As the amount of the routers on the network grows, it becomes prohibitive to use LS, and also the overhead of DV becomes impractical. Alongside with this **scalability issue**, there's a much more practical **administrative issues** which must be accounted for, like some organizations don't want others to route packets through their routers.

With this, what happens in practice is, the network is divided into a bunch of **Autonomous Systems (AS)**, a group of routers typically under the same administrative control. Each AS can implement the routing algorithms that it sees fit to route it's own routers, and it must have a **gateway router**, that connects the AS with the rest of the network.

## Routing in the Internet

Routing in the internet is divided into intra-AS routing, and inter-AS routing.

### Intra-AS Routing

An intra-AS routing protocol is used to determine how routing is done inside of an AS. In the internet, two routing protocol have been used extensively for that, the **Routing Information Protocol (RIP)**, and the **Open Shortest Path First (OSPF)**

RIP uses a decentralized routing algorithm like DV, while OSPF uses the centralized link-state algorithm.

### Inter-AS Routing: BGP

An inter-AS routing protocol is used to find routes through multiple ASs. In the internet, **the standard inter-AS routing protocol is the Border Gateway Protocol (BGP)**

BGP is extremely complex, and won't be covered in depth here, but it basically provides a way for an AS to discover it's neighbors ASs.

## Broadcast and Multicast Routing

All routing approaches viewed so far where unicast routing, that is routing between a host to only one other host. This doesn't satisfy all networks routing requirements, we must also have a way of broadcasting, and multicasting packets.

### Broadcast

For broadcasting, one host must send the a packet to all other hosts on it's network. A naive approach would be to leverage unicast routing, and just send N copies of the packet to all the other hosts using their IP addresses, while this may seems like a solution, it is not, first because it's not performant at all, and the most important reason is that the sender may not know the address of all the hosts on it's network. So we must take another approach.

#### Uncontrolled Flooding

On uncontrolled flooding, a host sends the packet to all it's neighbors, which in turn sends it to all it's own neighbors (expect the one it received it from), and so on, if the graph is connected, eventually all nodes will get the packet. While this approach may seem fine, it has deadly flaws. First if the graph has cycles, packets will loop indefinitely, at some point render the network useless. Another flaw is that a host may receive duplicate packets, and so this approach is not an option.

#### Controlled Flooding

A key to avoiding the flaws of uncontrolled flooding, is for a node to judiciously choose when to flood a packet, and when not to flood a packet. This require nodes to keep some sort of state for each broadcast packet, and make this decision based on that.

#### Spanning Tree Broadcast

Another approach to broadcasting, is to create a spanning tree of the network graph, and then send the packets through this tree. This ensures that all nodes will receive the packets (assuming the original graph was connected in the first place), and there will be packets infinite looping.

### Multicast

While broadcast sends a packet from a source to all nodes in a network, multicast sends packets from one source to a **subset of nodes** in the network. This has a lot of real world applications, such as multiplayer gaming, bulk data transfers, live streaming data, live shared data, etc.

The two immediate problems that arise in multicasting packets are how to know who are the receivers of the data, and how to address the packets that will be sent to theses receivers. To solve this problems, multicast uses **indirect addressing**, that is a single identifier is used for a group of receivers, and so the sender addresses the data to this **multicast group** which has it's own IP address, and then each participant of the group gets a copy of the packet.

Multicasting in the internet is accomplished with IGMP protocol, and multicast routing algorithms.

#### IGMP

The internet uses **Internet Group Management Protocol** to specify how hosts join, and leave groups.

#### Multicast Routing Algorithms

The goal of multicast routing algorithms is to find a tree of links that connects all of the routers with attached hosts. In the internet the protocols that are in place to do this are **Distance-Vector Multicast Routing Protocol (DVMRP)** (the older one), and the most widely used one **Protocol-Independent Multicast (PIM)**.
