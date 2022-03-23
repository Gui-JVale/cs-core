---
sidebar_position: 2
---

# Wireless Networks & WiFi

## Overview

As stated in this section's overview, wireless networks are composed of wireless hosts, wireless links, base station(s), and the network infrastructure.

Wireless links connect wireless hosts to base stations, which are access points to the larger network.

On the network-layer side, things are handled quite the same as in wired networks (thank you layered architecture!), the main changes reside on the link-layer, so that's where we'll focus on.

The nature of wireless links make them more susceptible to data lost, or corruption, this leads to wireless link-layer protocols needing to implement more powerful CRC checks, and reliable data transfer techniques (viewed on the transport layer section).

The 802.11 standard, or WiFi is a set of standardized protocols for sending/receiving frames on a local wireless network.

### CDMA

As with the wired Ethernet standard, wireless protocols must also implement [multiple access links protocols](/cs-core/computer-networking/link-layer/overview#multiple-access-links-and-protocols). Most of wireless protocols implement Code Division multiple access (CDMA), which can be classified as a **channel partitioning protocol**. In this protocol, data from different senders are encoded using different codes, and then get decoded on the receiving side. Assuming good codes were used to encode the data in the first place, the receiver is able to decode data even when they get overlapped with each other.

## 802.11 (WiFi)

### Architecture

The basic WiFi architecture is the **Basic Service Set (BSS)**, and is composed of one **access point (AP)**, that is connected to a gateway router (which grants access to the internet), and one or more wireless hosts. Note that a subnet may have multiple BSSs, and those can share the same gateway router.

The wireless hosts associate with the AP, and then through this wireless link they're able to reach the router.

#### Channels and Association

When a network administrator installs an AP, it assigns a one or two-word **Service Set Identifier (SSID)**, this is the name of the hotspot. The administrator must also assign a channel number to the AP, these channels range from 2.4 GHz to 2.485 GHz, within this range, WiFi defines 11 partially overlapping channels.

Let's look at the concept of a **WiFi jungle**, which you most certainly have experienced in practice. This happens when multiple AP's coverage area overlap with each other, and so the wireless host can choose which one it wants to connect to.

To gain internet access, your wireless station needs to join exactly one of the subnets, and hence needs to associate with exactly one of these APs. Associating means that your wireless station creates a virtual wire between itself and the AP.

How do wireless hosts recognize APs to associate with? Through the use of **beacon frames**. APs keep broadcasting beacon frames through a channel, which hosts can passively, or actively listen for. This beacon frames contain the AP's SSID, and MAC address.

After learning about the AP's SSID, and MAC address your host can choose which AP to associate with, and then it sends an association request to the AP, getting and association response from the AP, then the virtual link is formed.

The host can then send a DHCP request through the AP to the DHCP server in the router to get an IP address.

Authentication may be required to associate with the AP, one way to do that is to provide authentication based on the hosts MAC address. Another is to use the typical username, password scheme.

### MAC Protocol

WiFi, inspired by Ethernet, uses the multiple access protocol **CSMA with collision avoidance (CSMA/CA)**, which is a random access protocol. CSMA stands for carrier sense multiple access, meaning that each station sense the channel before transmitting. The may difference between the Ethernet MAC protocol, and the WiFi one is that collision avoidance part. Ethernet uses collision detection (CSMA/CS), so when a station is transmitting frames, and detects that another station has also started transmitting it on the same channel, it backs of, waits a random interval, and starts transmitting again. WiFi uses collision avoidance techniques, and because of the unreliable nature of wireless links, it also implements **link-layer acknowledgements**.

In link-layer acknowledgement, when the destination receives the frame, it runs a CRC check, if ok it responds with an ACK frame to the source. If the source doesn't receive an ACK after a period of time (timeout), it sends the frame again. If the frame never gets acknowledge after some tries, the source discards the frame.

So how does collision avoidance works? It's actually pretty simple, a wireless station X broadcasts a special frame, which is indirectly addressed to the AP, this special frame is a request to reserve the channel for a bit to send 80211data. The AP then, upon receiving the request, broadcasts another special frame, telling everybody associated with the IP that the channel is reserved for a bit, then X can send it's data. This reservation mechanism can add a lot of overhead, so it's used mostly when a station wants to send a lot of data at once.

### IEEE 802.11 Frame

![IEEE 802.11 Frame](/img/docs/80211-frame.png)

- _Payload & CRC_: at the heart of the frame is the payload, the actual data being sent. CRC achieves the same purpose of error detecting here as on the Ethernet frame.
- _Addresses_: one thing that at first glance may seem weird, is the fact that an 802.11 frame has 4 MAC address fields. Those are used for inter-networking among AP, the fourth address is used for _ad hoc_ networks, but since we're focus on the wireless networks with infrastructure, which uses only three address, let's focus on those:
  - _Address 1_: this is the MAC address of the wireless station that is to receive the frame.
  - _Address 2_: this is the MAC address of the wireless station sending the frame. So if mobile wireless station is transmitting a frame to an AP, address 1 is the MAC address of that AP, and address 2 is the MAC address of the sending wireless station.
- _Address 3_: to understand address 3, let's quickly review 802.11's architecture (BSS), it's composed of a subnet with at least one AP, a gateway router, and one or more wireless hosts. Address 3 should be the MAC address of the gateway router's interface. Note that there can be 2 APs (or more) connected to this gateway router. Let's go through an example go see this in practice: imagine a subnet BSS with one AP, a router R, and many wireless hosts. A datagram with the destination host in this subnet, say H1, arrives at the router R. R then uses ARM to find out the MAC address of H1 from the IP address on the arriving datagram. It then sends the Ethernet frame to the AP. The AP now must convert the Ethernet frame received by R to an 802.11 frame, so it can send it to H1. To do that, it puts H1 MAC address, it's own MAC address, and R's MAC address, respectively on address 1, 2, and 3. It then sends the 802.11 frame to H1. Now let's say H1 wants to send data outside the subnet through R, it creates an 802.11 frame, with the MAC address of the AP, it's own MAC address, and R's MAC address, respectively. Once this frame arrives at the AP, the AP must convert the 802.11 frame into an Ethernet frame, and so address 3 is needed for that. After the conversion, it sends the now Ethernet frame to R, which in turn, forwards it outside the subnet.

- _Sequence Number_: as stated previously, 802.11 uses acknowledgements. Because those can also get lost on the way, a sequence number is needed, so the receiver knows when it's receiving the same frame multiple times.
- _Duration Field_: recall that with CSMA/CA, a mechanism of channel reservation is used for a wireless station to get the channel for a duration of time, the purpose of this field is to specify that duration.
- _Frame Control_: we won't go in depth into those, but the most important fields in frame control for this discussion are _Type_, and _Subtype_, which are used to distinguish frames like ACK, special reservation frames, etc.

### Mobility Within the same IP Subnet

Although mobility is the topic of the next section, let's get our feet wet with the much simpler task of handling mobility within the same IP subnet.

Universities, or companies may use multiple BSSs within the same subnet to support the amount of wireless hosts they have. This leads to a question: what happens when a host H1 moves from BSS1 to BSS2 while on a TCP connection? Well, the thing that really makes it easy here is that when H1 moves from BSS1 to BSS2, its IP address will remain the same, which consequently will keep his TCP connection going. What really happens in practice though? Well, when H1 starts to move away from the range of AP1, it starts to detect the weakening of the signal, and so it disassociates with AP1, and associates with AP2. This raises a new question, how would the switch that forwards frames to AP1, and AP2, know that H1 moved, and it should know send frames destined to H1 to AP2, instead of AP1? Remember that switches are self-learning, and so eventually it will pick up the change, however, a hacky way to speed this is up is for H1, once connected to AP2, send a frame addressed to itself, this will cause the switch to update it's switch table.

## Personal Area Networks: Bluetooth & Zigbee

### Bluetooth

802.15.1 (Bluetooth) is a short range, low-power, and low-cost personal area network used mostly for mobile devices to communicate with each other, essentially providing a replacement for a physical link in short ranges. It works in ad hoc mode, that is, there's no infrastructure, or "access".

In a bluetooth setting with many devices, a **piconet** is formed with up to 8 devices. One of this devices is assigned a master, dictating the communication, and the other slaves (active) devices. There can also be up to 255 parked devices, who aren't allowed to communicate until the master changes their state to active.

### Zigbee

While Bluetooth provides a "cable replacement", Zigbee operates at an even lower-power, lower-data-rate, lower-duty-cycle fashion.
