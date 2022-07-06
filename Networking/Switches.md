# Switches
A [[Data Link Layer]] Ethernet switch makes its forwarding decisions based only on the [[Data Link Layer]] Ethernet MAC addresses. A switch has a *MAC Address Table*, also called *Content Addressable Memory Table (CAM)* which is empty at first.

## Building MAC Address Table
The switch dynamically builds the MAC address table, where the switches examine all incoming frames for new source MAC address, if it receives one it adds it to the table along with the port number. If the source MAC address does exist, the switch updates the refresh timer for that entry. By default, most Ethernet switches keep an entry in the table for 5 minutes.

## Forwarding Frames
If the destination MAC address is a broadcast or a multicast, the frame is sent to all ports except the incoming port. If the destination MAC address is a unicast address, the switch will look for a match in its MAC address table, if the destination MAC address is in the table, it will forward the frame out the specified port, If  not the switch will forward the frame to all the ports except the incoming port. 

### Frame Forwarding Methods
#### Store And Forward
A store and forward switch receives the entire frame, and checks if the frame data is not corrupted, if its not corrupted the switch will look up the destination MAC address in the table then forwards it to the correct port.

#### Cut-Through
The switch will forward the frame without checking it or storing it once the frame starts arriving at the switch. There are two types of Cut-Though Forwarding.
##### Fast-Forward
Once the switch reads the destination MAC address the switch will start forwarding the frame. Which offers the lowest level of latency.
##### Fragment Free
The switch will buffer the first 64 bytes of the frame before it starts forwarding the frame to its destination.

## Filtering Frames
As a switch receives frames from different devices, it is able to populate its MAC address table by examining the source MAC address of every frame. When the switch’s MAC address table contains the destination MAC address, it is able to filter the frame and forward out a single port.

## Memory Buffering
An Ethernet switch may use a memory buffering technique to store frames before forwarding them, or when the destination port is busy due to congestion until it can be transmitted latter.

There are two types of memory buffering techniques:
* **Port-Based Memory:** Frames are stored in queues that are linked to specific incoming and outgoing ports.
* **Shared Memory:** All frames are deposited into a common buffer which is shared by all ports on the switch.

## Duplex And Speed Settings
Most devices use auto-negotiation which enables two devices to automatically information about speed and duplex capabilities and choose the highest performance mode. **Duplex Mismatch** is common cause of performance loss where a device at one end will operate at full duplex mode while the other will operate at half duplex mode.

## Auto-MDIX
Connection between specific devices such as switch-to-switch, switch-to-host.... require a specific cable type (crossover or straight-through). Most switches now support the automatic medium dependent interface crossover feature which automatically detect the type of cable attached to the port and configures the interface accordingly.
