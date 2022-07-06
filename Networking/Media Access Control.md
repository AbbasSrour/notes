# Media Access Control
Media access control is the equivalent of traffic rules that regulate the entrance of motor vehicles onto a roadway., the absence of any media access control would lead in data collision, also different situation have different media access control rules.

## Topologies
### Physical Topology
Physical topology refers to the physical connections and identifies how end devices and infrastructure devices such as routers, switches, and wireless access points are interconnected.

### Logical Topology
Logical Topology refers to the way a network transfers frames from one node to the next, where the IP and Port connections are incorporated into the schema. These logical signal paths are defined by data link layer protocols.

### Wan Topologies
#### Point-to-Point 
Permanent link between two endpoints. 
##### P2P Physical Topology
Frames are placed on the media by the node at one end and taken from the media by the node at the other end of the point-to-point circuit. 
##### P2P Logical Topology
End nodes communicating in a point-to-point network can be physically connected via a number of intermediate devices.However, the use of physical devices in the network does not affect the logical topology. The logical connection between nodes forms what is called a virtual circuit.
#### Hub and Spoke
A central site interconnects branch sites using point-to-point links.
#### Mesh
Provides high availability, but requires that every end system be interconnected to every other system, a downside to mesh topology is that administrative and physical costs can be significant.

### LAN Topologies
#### Star
End devices are connected to a central intermediate device using Ethernet switches.
#### Extended Star
Additional Ethernet switches interconnect other star topologies, or in other words multiple star networks connected together.
#### Bus
Used in legacy networks where all end systems are chained to each other and terminated in some form on each end and switches are not required to interconnect the end devices. Bus topologies using coax cables were used in legacy Ethernet networks because it was inexpensive and easy to set up.
#### Ring
End systems are connected to their respective neighbor forming a ring, where unlike the bus topology, the ring does not need to be terminated. Ring topologies were used in legacy Fiber Distributed Data Interface (FDDI) and Token Ring networks.


## Duplexing
### Half Duplex Communication
 Both devices can transmit and receive on the media but cannot do so simultaneously. Used in legacy bus topologies, Ethernet hubs, and [[Network Media#Wireless Media|WLANs]].
### Full-Duplex Communication
Both devices can transmit and receive on the media at the same time. [[Data link layer]] assumes that the media is available for transmission for both nodes at any time. Ethernet switches operate in full-duplex mode by default, but can operate in half-duplex if connecting to a device such as an Ethernet hub.

## Methods
### Connection-Based Access
Nodes operate in half-duplex, where they compete for the use of the medium and only one device can send at a time. CBA uses Carrier Sense Multiple Access/Collision Detection(CSMA/CD) to resolve collision problems. 
#### CSMA/CD
Carrier Sense Multiple Access/Collision Detection If two devices transmit at the same time, a collision will occur, both devices will detect the collision on the network. Data sent by both devices will be corrupted and will need to be resent.
#### CSMA/CA
Uses a method to detect if the media is clear, it doesn't detect collisions but attempts to avoid them by waiting before transmitting. Ethernet LANs using switches do not use a contention-based system because the switch and the host NIC operate in full-duplex mode.
### Controlled Access
Each node has its own time to use the medium, Legacy Token Ring LANs are an example.

