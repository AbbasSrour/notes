# Data Link Layer
The data link layer is the second layer in the [[Layered Architecture|OSI Model]], this layer receives  a packets from the [[Network Layer]] and encapsulates it into a frame before sending it to the [[Physical Layer]]. The Data Link Layer encapsulates a packet by adding the MAC Address Of the Source and the Mac Address of the destination and a trailer to the packet making turning it into a frame.

## Data Link Sub-Layers
Data link layer is divided into two sublayers:
### Logical Link Control (LLC)
Communicates with the network layer and tells it which network layer protocol is being used for the frame. It also allows multiple [[Network Layer]] protocols, such as IPv4 and IPv6, to utilize the same network interface and media. And it is implemented in software.

### Media Access Control (MAC)
Defines the media access processes performed by the hardware, and provides the data link layer addressing and access to various network technologies. It also communicates with [[Ethernet]] to send and receive frames over copper or fiber-optic cable and with wireless technologies such as WiFi and Bluetooth. The MAC is implemented in hardware and is usually stored in the network card.

The MAC has two primary responsibilities, Data Encapsulation for Frame delimiting, Addressing and Error Detection. The second primary responsibility is [[Media Access Control]] which is responsible for the placement and removal of frames from the media.

![](https://subnetbytes.com/wp-content/uploads/2021/05/Datalinklayer-b.png)

## Frame
Each frame type has three basic parts: Header,Data, Trailer. Structure of the frame and the fields contained in the header and trailer depend on [[Network Layer]] protocol. In fragile environments like Satellite connections, the header and the trailer fields are larger for more control over the data, this done to ensure reliable delivery. The header and the trailer of the frame are different depending on the topological medium the frame is traveling through.

### Frame Components
* **Frame Start and Stop Indicator Flags:**  Identifies the beginning and end limits of the frame.
* **Addressing:** Indicates the source and destination nodes.
* **Type:**  Identifies the [[Network Layer]] protocol in the data field.
* **Control:** Identifies special flow control services such as QoS.
* **Data:** Contains the frame payload (i.e., packet header, segment header, and the data).

![](https://i0.wp.com/networkustad.com/wp-content/uploads/2019/06/Datal-link-layer-frame-fields.png)


## Data Link Addresses 
The purpose of the data link address is to deliver the data link frame from one network interface to another network interface on the same network. As the frame travels from source to destination the frame is de-encapsulated and re-encapsulated with source and destination MAC addresses. More on this in the [[Address Resolution Protocol]].

### Same Network Addressing
Devices on the same network send and receive data by directly setting the destination MAC address in the frame for the targeted device.

### On A Remote Network
For a remote network the frame cannot be sent directly to the remote destination host, therefore the frame is sent to the default gateway. The router the removes the received [[Data Link Layer]] information and adds new data link information before forwarding out the exit interface.
