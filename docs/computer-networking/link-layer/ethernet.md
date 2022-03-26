---
sidebar_position: 5
---

# Ethernet

Ethernet is the protocol (actually a standard of many protocols, but for simplicity...) that embodies the topics discussed above.

It can be said that Ethernet has been for local networks, what the internet has been for global networks.

It provides a connectionless data transfer between nodes, and it uses CSMA/CD protocol for shared broadcast channels. which is a random access protocol.

## Ethernet Frame Structure

![Ethernet Frame Structure](/img/docs/ethernet-frame.jpeg)

- _Preamble_: a sequence of bytes meant to "wake up" the receiving adapters.
- _Addresses_: self-explanatory.
- _Type_: used to specify the service at the layer above, which most of the time it's IP. This is similar to the IPv4 protocol field, glueing together the link and network layers
- _Data_: payload (46 to 1500 bytes).
- _CRC_: used for Cyclic Redundancy Check (error detection). Once the receiver gets the data, it checks CRC to see if the frame was corrupted, if it was it simply drops the packet, never warning the receiver (as mentioned before, on the internet the reliability gets implemented on the transport layer).
