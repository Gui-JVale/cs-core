---
sidebar_position: 4
---

# ICMP

## Overview

ICMP is a reporting protocol that allows hosts, and routers to communicate throughout the network. It sits just above IP, as it is an IP payload (just as a TCP/UDP segment).

ICMP was designed with the idea of congestion control in mind, whenever a router is congested, it would send an ICMP message to the host sending the packets, to slow the data rate down, however today's internet's congestion control is mostly handled by TCP congestion control, not ICMP. In practice, ICMP is mostly used for **error reporting**.

## ICMP Message Types

![ICMP message types](/img/docs/icmp-messages.png)
