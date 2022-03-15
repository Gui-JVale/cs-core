---
sidebar_position: 4
---

# DNS

Domain Name System is, in a nutshell, **a way to translate human friendly names (like google.com), to computer friendly names (like 192.186.92.0)**. It's also an application layer service that allows hosts to **query IP addresses** based on hostnames.

Different then HTTP, FTP, and SMTP, DNS uses **UDP** under the hood. The simplicity, and improved performance of UDP, allows DNS to fulfill it's requirements better.

Whenever a computer needs to request, or send data to another computer through the internet, it must have it's _IP Address_ which, for IPv4 looks something like this: 192.186.92.0. However this kind of naming convention is not very practical for humans, it's way easier to remember a name, then to remember a big number, and because of that, hosts use DNS to get an **IP address based on a domain name**.

## A Distributed Database

DNS is basically **the biggest distributed database in the world**. It's distributed because there isn't one main server, who keeps all the records for IP addresses, and domains, such design would be extremely flawed due to having one big point of failure, receives ridiculous loads of traffic, and also there's no way of having one point that's close to everybody, leading to poor performance across the internet. Instead, DNS records are kept in many DNS servers around the globe.

Knowing that, one may wonder how are all this records organized across so many servers. And the answer is using hierarchy.

## A Hierarchical Database

DNS Servers are divided into three classes: **Root DNS serves, Top-Level domain (TLD) servers, and Authoritative servers**.

### Root DNS Servers

This is where the query starts. A host sends a DNS query to a root DNS server, depending on whether the query is made iteratively, or recursively, the root server will either return the IP Address of the corresponding TLD server (iteratively), or forward the query to the TLD server (recursively).

### Top-Level Domain (TLD) Servers

This servers are responsible for handling top level domains, such as _.com_, _.org_, _.gov_, _.edu_, etc. They return the return the IP address of the Authoritative Server that has the DNS records.

### Authoritative DNS Servers

Every company with publicly available hosts must have their DNS records on an Authoritative DNS server. An organization can have their own Authoritative DNS Server, or pay another company to keep their DNS records there.

_See page 160 of Computer Networks for DSN hierarchy graph._

## DNS Caching

DNS caching is very simple, once a DNS server receives a DNS reply, it can keep the translation in memory so that the next time the same query is made, it doesn't have to go down the DNS chain again. End hosts can also keep a cache file with mappings of domain names to IP addresses.

## DNS Records

DNS records are structured in the following way:

`(Name, Value, Type, TTL)`

The type of the DNS record can be one of the following:

### Type A records

Name is a hostname, and Value is an IP address. These records reside on the authoritative DNS server for the domain.

`(relay1.bar.foo.com, 192.186.92.0, A)`

### Type NS records

Name is a domain (foo.com), and Value is the hostname of the authoritative DNS server. Note that if a DNS server has a type NS record, it must also have a Type A record that maps the authoritative server hostname to it's IP address.

`(foo.com, dns.foo.com, NS)`

### Type CNAME records

Name is a hostname, and Value is a canonical name (such as relay1.bar.foo.com).

`(foo.com, relay1.bar.foo.com, CNAME)`

### Type MX records

Name is a hostname, and Value is a canonical name for a _mail server_ (such as mail.bar.foo.com).

`(foo.com, mail.bar.foo.com, MX)`
