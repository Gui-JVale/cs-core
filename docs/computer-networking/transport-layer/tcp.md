---
sidebar_position: 4
---

# TCP

## Overview

TCP is a connection-oriented transport layer protocol that provides reliable data transfer, flow control, and congestion control to the application layer.

To truly appreciate TCP, it must be stated that, the network layer provides a best-effort delivery service, meaning that packets may get lost, and may arrive out of order, also packets can be corrupted. Because of that, the internet's network layer service (in practice the IP protocol), is said to be **unreliable**. So TCP **provides a reliable service on top of an unreliable service**.

One may wonder how that's possible. This is where principles of reliable data transfer come in. By using a set of mechanisms, algorithms and techniques, TCP is able to provide a reliable service on top of a unreliable one. Of course, as is anything in Computer Science, nothing is free, everything has it's tradeoffs, and with TCP, it's no different. Reliable data transfer comes at the expense of more complexity, and less performance, tradeoffs which many applications have to make due to their requirements. This is one of the reasons why the end to end principle exists on the internet, meaning complexity must be implemented on the end systems, not on the internet's core (routers), the core must remain simple, and performant.

## Principles of Reliable Data Transfer

Before diving into how TCP provides reliable data transfer on top of an unreliable service, we must first go through the principles of reliable data transfer, then we'll be able to see how TCP puts those to practice.

Surprisingly (or not), reliable data transfer protocols share many similarities to the (implicit) protocols humans use for communicating, specially over the phone.

When a person is sharing something, we usually provide positive feedback between chunks of information (like "uhum"), or negative feedback (like "can you repeat that last part please?"), also, on the phone, if after we say something we hear a pause that's too long, we may ask if the person is still on the other end of the line, and we might even need to repeat what we just said last. Some parallels can be drawn between reliable data transfer, and human communication, and part of the reason for that is because some of the mechanisms were in fact inspired by it.

### Positive and Negative Acknowledgements

The concept of positive, and negative acknowledgements are pretty simple, when a host sends a packet to another host and waits, the receiving host sends back a positive acknowledgement to the sender, confirming that it, in fact, received the packet, the sender sends the next packet, and so forth. This is called stop-and-wait.

If the packet arrives corrupted (see below how that's detected), or if a packet is missing between two other packets, the receiver can send a negative acknowledgement, and then the sender can retransmit the data.

As you may have imagined, stop-and-wait isn't very performant, so usually hosts use a boosted version of stop-and-wait implementing a **pipelines**. The idea here is that, instead of just sending one packet, the sender sends _n_ packets, and then waits for the acknowledgements of those, retransmitting when necessary. Then it keeps sending these packets in groups.

This raises another question, what if the acknowledgement gets lost? Or what if it gets corrupted? This can be solved using timeouts (if the packet takes way to long), and checksums.

### Checksums

Checksums are a simple, and elegant mechanism. Before the sender sends the packet, it calculates a checksum of the payload, that is, it basically sums up the bits of the payload, and puts it in a special header field on the TPC segment. The receiver then, can calculate the checksum, and make sure that it matches with the header field, if it does, the packet is good (at list most of the time), if it isn't, then it got corrupted, and has to be retransmitted.

The flaw of checksums is that if two complementary bits get corrupted, they can end up generating the same checksum, which is not good. The probability of this happening is low, but it's still an issue.

### Sequence Numbers

Sequence numbers are a way of assuring the data is kept in order, while at the same time providing a way to practically have positive, and negative acknowledgements.

Before the sender sends the data, it puts a sequence number on the packet _n_, upon receiving it, the receiver can then send a packet to the sender with the payload of _n_ acknowledging that packet. The next packet gets sequence number _n + 1_, and so forth.

This also helps with detecting missing packets, for example, if the receiver gets packets n, and n + 2, it can detect that the packet with sequence number n + 1 is missing, and then can send a negative acknowledgement to the sender, so it can then retransmit it.

Upon receiving data out of order, the receiver can choose some ways of acting upon it. It can just reorder the data itself (which is more complex), or it can simply send negative acknowledgements on packets that arrive out of order, making the receiver retransmit them, this provides a simpler implementation on the end hosts, at the cost of more resources used on the network for retransmission.

### Timeouts

Timeouts are self-explanatory, basically if the sender sends a packet, and it doesn't hear back a positive acknowledgement from the receiver in a period of time, it assumes that the packet got lost, and it retransmits it.

This can get tricky, however. How does the sender knows the right timeout time? This can vary greatly depending on how far are the two hosts. The truth is that it can't really tell the ideal timeout time, most practical implementations use some kinda of probing to get closer to a good timeout time, that is a time that doesn't lead to the sender re-sending data without any need for it, while still recognizing lost packets in a reasonable time.

## TCP In Practice

### Establishing Connection

TCP is said to be connection oriented. The processes on two different end hosts maintain a logical connection (stream of bytes) through the internet. You may wonder how that's possible since the internet's core is packet switched and unreliable, meaning packets can take different routes to reach the same destination.

A TCP connection is called a **full-duplex**: process A can send data to process B through the network, and vice-versa. Also multicast (broadcasting data to many hosts) is not possible with a TCP connection.

This is largely due to how TCP sets up connections, and tears them down. Connections are established in TCP using a **three-way handshake**. The process goes like this between a client and a server:

1. Client sends a special TCP segment, called SYN, to the server, with no payload;
2. Server, upon receiving the SYN, sends back another special TCP segment, called SYN/ACK, to the client. with no payload;
3. Client upon receiving the SYN/ACK, send yet another special segment, ACK, back to the server, this segment may have payload.

That's the three-way handshake, and the TCP connection is now established. To tear it down, TCP uses another special segment, FIN, which is sent with acknowledgements as well.

### TCP Segment Structure

![TCP segment structure](/img/docs/tcp-segment.png)

Source and destination port numbers were already covered, they server for multiplexing and demultiplexing.

Sequence number, checksum, and acknowledge number are the principles of reliable data transfer discussed above in practice.

The flags URG, ACK, SYN... are to indicate the type of the TCP segment.

The Receive Window filed is used for **Flow Control**.

Options are optional fields that can be used by the processes, and that's why there's header length field, so options can be parsed.

### Calculating Timeout

TCP calculates timeout based on the average Round Trip Time (RTT), TCP keeps sampling the RTT, and uses a fancy formula to calculate it's timeout based on that.

### Reliable Data Transfer

TCP uses sequence numbers, ACK's (using pipelines), and timeouts to provide reliable data transfer. It does not implement negative acknowledgements, it lets the timeout take care of it.

### Flow Control

TCP provides flow control, that is, it ensures that the sender isn't flooding the receiver with more bytes that it can read. By keeping a receiver window header on the segments, TCP is able to control the flow of packets, sending that at the pace that the receiver is reading it.

### TCP Congestion Control

TCP congestion control mechanism must be implemented even though the transport layer doesn't get any congestion data from the network layer, that is, the network layer doesn't explicitly says: "Hey! I'm congested, send less packets". TCP must act as an attentive listener, and observer, and detect that if the network is currently congested or not.

To summarize TCP's congestion control mechanism, think about a child that asks his parents for candies. The child keeps, asking, and asking, and asking, and asking... until it hears 'ENOUGH!', then it stops asking for a bit, until it starts again at a slower pace.

The asking is equal sending packets. TCP keeps sending more, and more packets accelerating in an exponential manner, until it notices that packets are starting to get dropped. It then waits a bit, and starts sending packets accelerating in a linear manner. This behavior, when plotted into a graph, looks like a saw tooth. That's basically how it works.

### Bonus: TCP Finite State Machine

![TCP Finite State Machine](/img/docs/tcp-finite-state-machine.png)
