---
sidebar_position: 2
---

# Error Detection & Correction

As stated above, the link-layer can provide error detection, and correction services, it's time to talk in more practical terms to see how these get actually implemented

## Parity Check

This is a very simple way (but not 100% effective) to detect if data was corrupted. It can simply calculate the parity of 1s in the data, and store it on the frame's header. If the parity doesn't match on the receiving link, the data must've gotten corrupted somehow.

As you may have guessed, the flaw of this method is that data can get corrupted, and still maintain it's parity, which then it would go unnoticed (even worse!). A way to get around this is to calculate a more complex type of parity the **two-dimensional parity**. With this, the receiver can not only detect the errors more accurately, but also correct them.

## Checksum

Just as the network layer has the IP checksum, link layer frames also implement checksums to detect bit errors. As stated previously, this don't detect errors 100% of the times.

## Cyclic Redundancy Check

Cyclic redundancy check uses polynomial equations, and modulo arithmetic kung foo to detect errors on the data.
