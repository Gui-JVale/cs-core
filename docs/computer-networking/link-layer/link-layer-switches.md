---
sidebar_position: 6
---

# Link-Layer Switches

Link-layer switches are used in LANs. They're very similar to routers, but while routers act on the network-layer forwarding datagrams (using IP addresses), link-layer switches forward, and filter link-layer frames (using MAC addresses).

This switches maintain a self-learning table mapping MAC addresses to it's own network interfaces. Once it receives a frame from a sender it stores the sender's MAC address + the interface the frame came into into it's switch table, and then it does one the following:

- If the destination address is in the switch table, and the interface where the frame came from it's the same where it's supposed to go to, it drops the frame.
- If the destination address is in the switch table (and it's not the interface it came from), it forwards the frame to the receiver's respective interface.
- If the destination address is not in the switch table, it broadcasts the frame to all interfaces except the one it received the frame from.

Link layer switches are useful because they're self-learning, the switch tables are built on the go, requiring less manual setup, being **plug-and-play**. Another appealing benefit are:

- _Elimination of Collision_: because the switcher have buffers, and manage the frames, it avoids collisions on it's interfaces, improving the local network's performance considerably
- _Heterogeneous Links_: switches allow links of different bandwidth to be used together, being ideal for mixing up legacy equipment with new equipment
- _Management_: in addition to providing enhanced security, link-layer switches can detect to some extent malfunctioning interfaces, and simply disconnect them, avoiding the network manager to have to do that manually.

In general, a link-layer switch will suffice for small LAN's, but for bigger LAN's with thousands of hosts, routers + additional link-layer switches will be required.
