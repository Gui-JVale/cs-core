---
sidebar_position: 2
---

# Routers

## A Good Analogy

Before diving into technical terms, lets have a look at a good analogy as to how routers work:

Imagine a roundabout where a lot of cars come, and go. Now lets make a small change on the workings of that roundabout, instead of each car just entering the roundabout when traffic permits, the cars must stop at the roundabout entry, and talk to the "roundabout police", the driver must inform them it's final destination, and then the officer will tell the driver which exit of the roundabout he should take to get there, the car can enters the roundabout (which may have other cars in it), and leaves at it's prescribed exit.

You may imagine that lines of cars may form on the entries of the roundabout, as well as on the exits.

With this analogy:

- roundabout entries = router inputs
- inside the roundabout = fabric switch
- roundabout exits = router outputs

## What's Inside a Router?

Routers are **network layer packet switches**, and their job is to **take a packet, and forward it to another interface**.

One may wonder how it does that, and what a router actually is. A router is nothing but a special type of computer, who was a very specific task (that of forwarding packets on the network), and because of that, **most of it's functionality can be implemented in hardware**, which is a lot faster.

Inside of a router there are inputs (where the forwarding tables reside), a switch fabric, outputs, and a processor.

Naturally, packets arrive at the inputs (where they get queued if needed), and based on the forwarding tables on these inputs, each packet gets forwarded, through the switch fabric, to it's respective output. On the output, packets can also get queued before leaving.

The router processor executes the routing protocols, maintains the input's forwarding tables, and performs network management functions.

![Router Architecture](/img/docs/router-architecture.png);

## Input Processing

The input implements network, and link layer functionalities.

It's here that the lookup on the forwarding table is made, that's so crucial for the network layer. It does so using a **longest prefix match** algorithm.

### Longest Prefix Match

Based on the IP address of the destination, the router's input looks up the forwarding table, and tries to match the address of the packet with the longest match on it's forwarding table, it then handles the packet of to the fabric switch to forward it to it's respective output.

The forwarding table is computed, and maintained by the router processor via a separate bus.

This lookup process, because of the need for performance, is implemented in hardware.

## Fabric Switch

The switch fabric is at the heart of the router, connecting the inputs with the outputs (a network inside of a network device!).

There are mostly three techniques for switching packets. _Switching in memory_, _switching via a bus_, and _switching via an interconnection network_. See those below:

![Three Router Switching Techniques](/img/docs/switching-techniques.png);

### Switching Via Memory

In this technique, essentially the packet is copied from the input, to the output memory.

Many modern routers use this technique.

### Switching Via a Bus

In this technique, a shared bus sits between inputs, and outputs, and all the packets go through to end up on their correct outputs. A limitation of this technique is the switching is only as fast as the bus speed.

### Switching Via an Interconnection Network

This is a way of overcoming the limitation of a single shared bus, where inputs and outputs are connected through crossbars (looking kinda like a grid). This allows packets to be forwarded in parallel (only when two packets' output port destination are different).

## Output processing

Outputs also implements network, and link layer functionalities, this includes selecting and de-queueing packets for transmission, and performing the needed link-layer and physical layer transmission functions.
