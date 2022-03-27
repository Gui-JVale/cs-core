---
sidebar_position: 1
---

# Introduction

Security is an important requirement of many systems, from banking to social media, it's of ultimate importance to keep data private, and ensure that only allowed users can access and manipulate the data.

Security is specially important on the internet, a public network of networks in which virtually anybody can access from anywhere in the world. Many network applications have strict security requirements, and data going through the internet can be visible to everybody. As we will see, there are many ways bad guys can temper with data, and even bring down networks. A famous attack is DDoS, in which a botnet (an army of distributed computers) brings down many servers by issues a large number of requests in short period of time, rendering them useless. Because it's distributed, it's hard to distinguish this attack from just regular users.

In a computer network, security can be implemented in all layers, and in many levels, from the network's edge to it's core. Because the Internet, by design, abides to the end-to-end principle (that is complexity and augmented functionality must be implemented on end systems), security practices resides mostly on end hosts.

So what is security? And what are it's properties? Let's take a closer look into that.

## Security Principles

Security is a measure of the system's ability to **protect data and information from unauthorized access** while still providing access to people and systems who are authorized.

The key properties of security are:

- _Confidentiality_: data and services are protected from unauthorized access.
- _Integrity_: data isn't subject to unauthorized manipulation.
- _Availability_: the system will be available for legitimate use.
- _Authentication_: identity verification from all parties in the transaction, ensuring they are who they claim to be.
- _Authorization_: grants a user the privileges to perform a task.
- _Non-Repudiation_: guarantee that once a user sends the message, it can't deny having sent the message, and the receiver can't deny having received the message.

At the heart of achieving these security properties in practice, is **cryptography**.

## Cryptography

Cryptography is a branch of applied mathematics concerned with developing practices for secure communication. It's heavily based on mathematical theory, specially number theory, and modular arithmetic.

Security on modern computers systems rely heavily in cryptography, many crypto algorithms being used on many levels of a system to ensure the properties above. For example, confidentiality can be achieved by encoding a message (encrypting) before sending it over, this way it will be more difficult for anyone who intercepts the message to understand it's content. To apply authentication, a host can have a digital certificate, which is cryptography based.
