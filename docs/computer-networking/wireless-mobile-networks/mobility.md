---
sidebar_position: 4
---

# Mobility

## Introduction

While wireless networks are cool, and practical, they introduce a new problem: mobility. What happens if a wireless host moves from one network to another? Well, with all that we discussed so far, it would be logical to assume that his IP address would change, and so any connection he had would be completely disrupted, not so good huh?

What is mobility in the first place? This term gets thrown around everywhere in the networking world. For our purposes we consider a mobile host one that moves throughout networks. The level of mobility needed varies, but it can be divided into two classes:

- Being able to move through networks without having the need to maintain a connection. An example of this is a student in a university who moves from the library to the dorm with his laptop, not needing to be online in between. As seen in the network layer, this gets taken care of already with DHCP.
- Being able to move through networks while maintaining a connection. Now this one is definitely more complex, imagine a user who's on a train going 200km/h while still on watching a movie on netflix.

To understand mobility principles better, let's take a look at a good analogy.

## A Good Analogy

Think about a young adult who just moved out of his parents home, and it's now going from dorm to dorm, his address always changing up. How would an old friend contact this person, not knowing at all what his address is at the moment? Well, one solution for this is for the old friend to talk to his family who have a stable home address. His friend can reach out to them, and then the family can either pass along the message, or tell where he currently is, and so his friend can reach him directly.

This represents with accuracy one way to implement mobility in networks. The young adult it the mobile host, the dorms are the networks, his family's home it's the mobile host **home network**.

## Mobility in Practice

Now understanding the bigger picture, let's go a bit more practical and technical on how mobility works on networks. So there's a mobile host, who has a home network, and who moves from foreign network to foreign network. In the home network, there's a **home agent**, who's responsible for contacting and establishing connections with the mobile host. Similarly, in a foreign network, there's a **foreign agent** who's responsible for notifying the home agent which foreign network the mobile host is currently attached to.

In this manner, a connection establishment can happen like this: host A wants to connect with mobile host M. It sends packets to M's home network, the home agent of M then, because it received data from a foreign agent saying that M's currently in foreign network F, can forward the data to F.

This is known as indirect routing, because all the data goes through the home network. As you can imagine, in some cases this cannot be the most efficient way, specially when the hosts are close, the data would have to go through the home network regardless. Another approach is to use direct routing, with this the home agent wouldn't forward the data, but tell the other host where the mobile host currently is, and so a direct connection can be established. While this solves problems raised above, it brings complex drawbacks itself. With direct routing, how would the other host know that the mobile host has moved to another foreign network in the middle of the connection? Well, a protocol could be implemented to solve that, however it wouldn't be scalable at all to keep this sort of state with billions of mobile users nowadays, and so direct routing is more complicated than it seems.

### Mobile IP

In the internet, the embodiment of mobility is Mobile IP, which uses the principles discussed above. It uses indirect routing, and home/foreign agents.
