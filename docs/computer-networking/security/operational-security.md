---
sidebar_position: 9
---

# Operational Security: Firewalls & IDSs

## Introduction

We've stated before that security is essentially composed of confidentiality, message integrity, authentication, and availability. While we went over (a lot!) confidentiality, message integrity, and authentication on all four layers, we haven't really touched **availability**. A system is said to have availability if it's available for use by legitimate users. In networks, this gets handled by operational security, more specifically **Firewalls**, and **Intrusion Detection Systems (IDSs)**.

This way of security checking has been employed for centuries, for example the guards at the entrance of the castle, filtering who should or shouldn't enter, the security at the entrance of gated communities, the security desk at the entrance of companies, and so on. In computer networks, this is done by a firewall.

## Firewalls

Firewalls are a mix of hardware and software that sits between a local network and the internet. They are essentially packet filters, allowing or disallowing certain packets to enter or leave the local network.

Firewalls have the following properties:

- All packets going in or out of the local network must go through the firewall
- Only authorized traffic, defined by the **local security policy**, will be allowed to continue.
- The firewall is immune to penetration. Meaning it can't be compromised, if not installed properly, the firewall can have security breaches.

Firewalls filter packets based on the local security policy, which is basically a table of rules that are based on packet parameters, such as source and destination IP address, if the packet is using TCP/UDP, if it's an ICMP message, source destination and port numbers, etc. With that the local network gains a lot of control over the packets that it allows to enter or leave.

Firewalls that use this static rule table are called **stateless packet filters**, meaning they don't keep any sort of state over packets, they just check the table and filter or not the current packet.

There are another class of Firewalls which are **stateful packet filters**, this firewalls can keep track of ongoing TCP connections between an outsider and a local host, and if it notices something weird that's not normal in a TCP connection, it can block the packets.

## Intrusion Detection Systems

IDS are much more complex than firewalls, their job is to try to detect **known attacks** that are occurring in the local network, such as a DDoS attack, and notify network administrators.

They do that by keeping a database of **known attack signatures**, and perform **deep packet inspection** to see it matches the signatures in their database. If something suspicious seems to be happening, they alert network administrators.
