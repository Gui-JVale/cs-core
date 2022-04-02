---
sidebar_position: 8
---

# Securing Wireless LANs

## Introduction

We're now at the link-layer, and the big concern here are securing wireless LANs. Physical links provide a protected channel, and so we don't have to worry to much about it.

As we've seen 802.11 uses radio waves as a channel, and so basically anybody who's inside the coverage area can intercept 802.11 frames without much effort.

The original version of 802.11 provides virtually no security at all, there are many known ways, and even free software made to exploit it's weaknesses. A protocol that was created to tackle this is the Wired Equivalent Privacy (WEP) which uses symmetric key encryption. However, this protocol provides weak encryption, which isn't that hard to break, also it does not specify any way to exchange keys. For those reasons we won't cover it at all, and we'll focus our attention on the IEEE 802.11i protocol, which was officially released in 2004.

## IEEE 802.11i

This is the protocol used to provide security over Wireless LANs, providing confidentiality, message integrity (which is already handled by 802.11), and authentication.

This security protocol also uses symmetric and public key encryptions, message digests, and authentication mechanisms used by other layers that were already covered.

802.11i uses an authentication server that talk with the AP. Advantages of this is that APs can share the same authentication server, and it doesn't add more complexity over the AP. The protocol has the following phases:

1. _Discovery_: In this phase, the client and the AP are finding out about each other. Communication isn't confidential yet, because no encryption parameters were agreed upon, so this is were it happens. The AP advertises the types of encryption it supports, and the client answers with his choices for the session.
2. _Mutual Authentication and Master Key (MK) Generation_: Authentication happens between the wireless client and the authentication server, the AP acts basically as a relay on this phase, forwarding messages exchanged by them. Once encryption settings have been agreed upon, the wireless client and authentication server proceed to use public key encryptions, and message digest to authenticate each other, and derive a Master Key MK.
3. _Pairwise Master Key (PMK) generation_: After both the client and server have the MK, they both derive from it a PMK, and the authentication server sends the PMK over to the AP. This is what we wanted, now both the wireless client and the AP have shared secret keys.
4. _Temporary Key (TK) generation_: Then both client and AP can use their PMK to derive additional keys for secure communication, specially the Temporary Key, which will be used to provide link-layer level encryption of data sent over 802.11i.
