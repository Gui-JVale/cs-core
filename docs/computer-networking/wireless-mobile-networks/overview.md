---
sidebar_position: 1
---

# Overview

## Introduction

Wireless networks are everywhere nowadays, from your home, to your local Starbucks, malls, gyms, theaters... you name it, but how does it actually works? Using it may seem somewhat magical, you just find a hotspot, connect your device to it, and boom! Internet access.

How about when you don't have WiFi available, but you still have internet access with you mobile data (like 4G)? And you can still use it while moving around, like on a car drive, or when riding the bus, or train, or going for a walk! What's up with that? It also may seem like magical workings. What if your

Throughout this section, we'll see the mechanisms behind wireless, and mobile networks, and hopefully demystify them a bit.

We've already covered in the link-layer section, how frames are sent/received on wired LANs using the Ethernet protocol. On this section, we'll take a look at the famous 802.11 protocol (WiFi!), and how it handles the sending, and receiving of frames (through the air!).

## Wireless Networks

On mobile network, there are a couple of player that are a part of the game, and those are:

- _Wireless Hosts_: hosts connected to a network through a wireless link
- _Wireless Links_: a link that connects hosts to a base station.
- _Base Station_: base stations have no obvious counterparts in wired networks, but the play the role of sending, and receiving data, connecting wireless hosts to the wired network. Base stations are access points, such as WiFi access points. When a wireless host is sending/receiving data through a base station, it's said to be **associated** with it. The process of moving from one base station to another is called **handoff**.
- _Network Infrastructure_: this is the larger network with which the wireless host wants to communicate.

It's good to point out that wireless links, from the standpoint of link-layer devices, can be seen just as any other physical link, the only difference being the medium, using the air as opposed a physical wire, this abstraction can help simplify things.

Another good thing to point out is that, while physical wires provide more reliability, and stability (meaning packets get lost, or corrupted at a low rate), wireless links are more unreliable, and unstable, **packets may get lost more easily**, and so any protocol that's used to send frames through this wireless links must account for that, providing recovery mechanisms to some extent.

## Mobility

It's good to note the importance of mobility in a network (something that's took for granted these days). Without mobile networks, it wouldn't be possible to have internet access on your smartphone while moving around (can you imagine that?). The challenge here is having a host that's moving through different networks, while still keeping an acceptable connection.

We've already seen that IP addresses are like postal addresses, not permanent, and move around with the host, but what happens if the host doesn't stay in place? What happens when the host keeps hopping from network to network? Does he get a new IP address every time? Well that might not work very well, imagine a host with IP address X receiving data, using TCP, from youtube servers. Then, because it's moving, it leaves one network, and hops into another network, and it's given a new IP address Y, how in the hell would the youtube servers know that the host changed it's IP address in the middle of a TCP connection? Well short answer, it would not! It would keep sending data to IP address X, and the connection would eventually get closed, and a new one would need to be formed (using IP address Y).

These are some of the challenges faced by mobile networks, and we'll see some mechanisms that allow mobile networks to be... well mobile.
