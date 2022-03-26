---
sidebar_position: 3
---

# Voice-Over-IP

## Introduction

Voice-Over-IP, also known as **internet telephony**, is used by applications to achieve results similar regular cell phone calls.

Analog audio is encoded/digitalized, then sent over the network, and once in it's destination it gets decoded back to analog audio.

As said previously, audio doesn't have high bit rates compared to videos, and so it doesn't face the challenges originated by that which we went over in the previous section. However, because humans are much more sensitive to audio delay or corruption then video, this class of multimedia applications faces it's own set of challenges.

## Limitations of Best-Effort IP Service

As we've seen, the internet's network-layer provides a best-effort delivery services, this means it's unreliable, and data can get lost, or corrupted, packets may arrive out of order as well. This unreliability provides a real challenge for voice-over-IP applications, specially due to end-to-end delay, and packet loss.

On the end-to-end delay bit, the amount of delay acceptable in this kinds of application is very small, imagine trying to talk with somebody, and the response keeps lagging out, it would be a very poor experience.

Maybe even worse than high delay, would be missing audio bits through the conversation. Users are not very tolerant when it comes to this aspect as well, and so packet loss becomes a big deal in voice-over-IP applications.

Another limitation is the varying times that it takes from packets to get from source to destination, causing a non-linear receiving of data, this **jitter** can make the received audio messed up, and not comprehensible.

With all of this challenges, one may wonder how can there be voice-over-IP applications that run over IP's unreliable best-effort delivery service?

Well there are some techniques in place to try to mitigate as much as possible this IP limitations, let's take a quick look.

### Jitter removal

At the receiver's end, it's possible to remove jitter using clever techniques like delaying the play of the audio to form a linear packet flow. These can be done using timestamps on the packets, and choosing a delay value. Packets arriving after this delay would be discarded.

### Forward Error Detection

This technique basically implements error recovery by introducing redundancy in the packets, augmenting reliability at the cost of higher transmission rates.

### Error Concealment

Error concealment tries to recover from packet loss by filling up the gaps on the fly based on the near by packets. Because consecutive audio bits are similar, it's possible to get by with this technique.

## Protocols

In the internet, there are two protocols that handle voice-over-IP: **RTP**, and **SIP**.

RTP runs on top of UDP, and specifies the packet header structure. It uses some of the techniques above.

SIP protocol for initiating sessions between callers, it specifies how streams should be setup, and teared down.
