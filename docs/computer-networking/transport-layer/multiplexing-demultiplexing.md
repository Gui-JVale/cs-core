---
sidebar_position: 2
---

# Multiplexing & Demultiplexing

## Overview

Multiplexing and demultiplexing is responsible for the logical communication between process on two end hosts provided by the transport layer.

## A Good Analogy

A good analogy to understand this topic is to think of two families with 20 members, 10 living in house A, and 10 on B. The houses are far, far away. They must communicate with each other through the mail service. Assume that each family member on one house only sends letters to the same family member on the other house (for simplicity). Also assume that letters are gathered and dropped at the post office every Sunday (also for simplicity). With this scenario, let's say on house A, Ann and Frank are responsible, every Sunday, for gathering all letters from all the 10 members on the house, and dropping them at the post office, they also get all the incoming letters from house B, and give them to each respective family member. House B also has 2 family members that do the same thing.

In this analogy:

- Family Members = Processes
- Letters = Packets
- Ann & Frank = Transport Layer
- Post Office = Network Layer

Observe that the post office doesn't really care about which family member the letter is addressed to, it just cares delivering the letter to the right address. In the same fashion, Ann & Frank don't have to worry, or even know, how the letter got there, their job is only to get each letter to the right family member. That's a good way to think about the relationship between the network layer, and the transport layer.

## How it actually works

As stated in previous sections, data goes into/out of a process to/from the network through a **socket**. Knowing this, we can deduce that the data must flow from one process' unique socket to the other process' unique socket.

So then, the transport layer work of examining a received segment (using special header fields), and based on that, forwarding it to the correct socket, is called **demultiplexing**. Symmetrically, the transport layer process of chunking up the data into segments with this special header fields (that will be used in demultiplexing), and send those to the network layer, is called **multiplexing**.

Knowing this, we also know that the transport layer requires that (1) each socket must have unique identifiers, and (2) each transport layer segment must have special fields that indicate which socket that segment must be delivered to.

So how does this work? Using these special header fields called **source port number**, and **destination port number**.

Port numbers can range from 0 to 65535, the well-known port numbers range from 0 to 1023 and are reserved to well-known protocols (like HTTP, and SMTP). With this, you may think that it's just mapping a socket to a port number, and call it a day, UDP basically does that, but TCP is more subtle.

### TCP multiplexing/demultiplexing

As always, TCP is a little bit more complex. While UDP uses a tuple `(destination IP address, destination port number)` to identify it's socket, which results in basically a binding between one port number, and a socket, this means if two different process, in two different end hosts, send UDP segments to a destination 3rd end host in the same port number, they will be directed to the same process/socket. TCP goes a bit further, and identifies it's sockets by a four-tuple: `(source IP address, source port number, destination IP address, destination port number)`, this means that, different than UDP, two arriving segments with different source addresses, but same port destination, will be directed to two different sockets (the only exception to this is the port listening to establish a TCP connection).
