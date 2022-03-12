---
sidebar_position: 1
---

# Introduction

The Application Layer is the upper most layer, and likely the layer that most software engineers will work on for the most part of the time.

The name gives away, but this is where the (network) application lives, and it uses the services that the bottom layer (the transport layer) provides to communicate with other hosts.

An application in this layer is software that will run in different end systems that will need to communicate with each other.

## Network Application Architecture

Network application architecture it's not software architecture (the latter specifying how different software components will interact with each other), it describes how different end systems will interact.

Popular example of Network Application Architectures are the **Client-Server Model** and the **P2P Architecture**.

## Processes Communicating

On Computer Networks, we're not worried how processes communicate with each other on the same end system (which is governed by rules of the OS), but how processes running on different end systems, with possibly different Operating Systems, can communicate.

Processes on different end hosts communicate with by sending messages to each other through the computer network.

In processes exchanging message, we generally label on as the **client** and the other one as the **server**. On a client-server model, is obvious who plays each part, but on a P2P architecture it's said the the host downloading the file is the client and the one serving the file is the server, note that the same process can (and probably will) act as a client and a server throughout it's life on a P2P architecture.

The software interface that allows processes on different hosts to talk to each other is called a **socket**, a process sends and receives data from a socket. Using an analogy, a process running in a host can be thought of as a house, and the socket would be the door, where it receives and sends messages to/from the outer world. **A socket serves as the API between the application layer and the transport layer**.

## Transport Services Available to Applications

Knowing that the application layer uses services provided by the transport layer, one might wonder what kinds of services that layer can provide for an application, so lets check them out. Keep in mind that these services are what the transport layer **can provide**, not necessarily what it does provide on the Internet.

### Reliable Data Transfer

The transport layer can provided reliable data transfer between to processes. That means the message will arrive from one process to another without losing data or being out of order.

### Throughput

The transport layer can provide guaranteed available throughput at a specified rate.

Also it can provide flow control so that when two processes that are on end systems with different throughput capabilities, they can still communicate without having to worry about one process sending too much data during a period of time (more than the other host can process).

### Timing

Transport layer can provide timing guarantees as to how long it will take for the data to be delivered.

### Security

The transport layer can also provide security through confidentiality, message integrity and authentication. This is mostly possible by the use of encryption techniques.

## Transport Services Provided By The Internet

The two transport layer services provided by the internet are **TCP** and **UDP**.

### TCP

TCP is a connection oriented service that provides reliable data transfer, flow and congestion control, and when paired with SSL can also provide security.

### UDP

UDP is a connection-less service that provides minimal guarantees, it doesn't guarantee that the data will be delivered, and that it will be in order. Also it does not provide any type of control or congestion flow. UDP just mostly provides error checking on top of the network layer.

## Protocols

The application layer (as all other layers) has it's own set of public (and proprietary) protocols. The most popular ones are **HTTP, SMPT, FTP and P2P**.

### HTTP

HTTP is used for client-server communication and it's pull protocol, meaning the client asks the server for data on demand.

### SMPT

SMPT is a mail-service protocol, that allows end hosts to exchange emails. It's a push protocol, because when a user sends an email, it pushes it's data to the receiver mail server.

### FTP

FTP is a File Transfer Protocol, which is very self-explanatory, and it also uses the client-server modal.

### P2P

P2P is used for the P2P architecture, and allows peer hosts to communicate with each other to transfer files in a distributed manner.
