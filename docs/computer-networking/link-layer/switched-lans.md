---
sidebar_position: 4
---

# Switched Local Area Networks

Switched local networks switches work on the link-layer level, and they switch frames through the subnet, instead of datagrams. They don't recognize IP addresses, or network layer routing protocols, this means that there must be some other way of addressing this frames through the subnet.

## Link Layer Addressing

Enters link layer addresses, or **MAC addresses**. These work on the link layer level, each host and router in the network has a unique MAC address (being more precise, each network adapter/interface on the network has a unique MAC address). This can lead to some confusion, why are there two addresses, IP and MAC? Do we really need those two?

As you may imagine, we do need it, and a good analogy to think about them is to see the MAC address as a social security number, you can't really change it, while the IP address is equivalent to a home address. You may change your address, but you won't change your social security number. Following this analogy, the IP address of a host may change when he joins a different network, however his MAC address will not change.

MAC addresses are flat (as opposed to hierarchical as IP), and each network adapter gets a unique one. They look something like this: `49-BD-D2-C7-56-2A`.

## Address Resolution Protocol (ARP)

Because of these addressing situation, there's a need to **translate between IP and MAC addresses**, the internet does this using Address Resolution Protocol (ARP).

ARP sits between the network-layer and the link-layer.

### Sending Frames Within a Subnet

Whenever a host wants to send frames to another host on the same subnet, it must have it's MAC address. To find out the receiver's MAC address, the sender gives it's network adapter the receiver IP address, and the ARP module resolves that IP address into a MAC address, with the IP, and the MAC address, the sender can now send the data.

The ARP module on an adapter resolves the MAC address by either looking at it's ARP table, where it keeps a list of IP address mapped to MAC address, and if it's not there, it then broadcasting and ARP packet through the subnet, the receiver seeing that the ARP packet contains it's IP address, it sends back an ARP packet to the sender with it's MAC address. This broadcast process is equivalent to someone shouting out at work: "What's the social security number of the person who lives at address X?"

### Sending Frames Outside a Subnet

To send frames outside of the subnet, the host must set the MAC address to the **gateway router of the subnet**, not to the receiving host (note that the IP address is still the receiver address). Once the frame reaches a router, the datagram is extracted from the frame, and gets processes by the router's network layer by checking against forwarding table, and sending the datagram to the correct output network adapter, the network adapter then frames the datagram again, and moves it forward. This happens until the destination is reached (or not!).
