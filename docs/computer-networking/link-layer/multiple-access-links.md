---
sidebar_position: 3
---

# Multiple Access Links

## Introduction

Multiple access links are links which multiple routers share, and so there must be a way to mediate how much each router gets to use the link, while optimizing resources, and performance. A good analogy for this is a busy cocktail party, where people are talking (sending data, and the medium would be the air). Multiple Access Protocols can be divide into three categories:

## Channel Partitioning Protocols

On channel partitioning protocols, the link is divided between the nodes either using time slots, or bandwidth. Each node gets a period of time to send data. In the cocktail party analogy, this would be equivalent to everybody having a fixed amount of time to speak while others listen (or pretend to do so).

This way seems very appealing because it avoids collisions, and seems very fair. However, there are two major drawbacks to this approach. First, a node is limited to the time slot even when is the only one who has data to send. Second, a node must always wait for it's turn on the transmission sequence. This can lead to a lot of unused resources. Following the analogy, this would be a party where only one person has a whole lot to say, and all the others just want to lister, having periods to talk on this scenario wouldn't work very well.

## Random Access Protocols

On random access protocols, when nodes sense there's no flow of packets going through the channel, they start sending their packets after some random interval. Note that because nodes wait for the channel to be free before starting sending data, the randomness gets a node to start first most of the times, and so the others keep waiting.

If a collision between two nodes happen, they both stop sending, wait a random interval, and then resend their frames again, one of the nodes is going to start sending data first, which will lead the other to wait for the channel to be free again.

This leads to better resource usage then channel partitioning methods, as the nodes enjoy the full bandwidth of the channel.

## Taking-Turns Protocols

On taking-turns protocols, each node is scheduled to have the channel to transmit a maximum amount of frames. If the node doesn't have any frames to send, then is passes it's turn to the next one.
