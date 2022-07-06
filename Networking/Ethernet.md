# Ethernet
Ethernet is the most widely used LAN technology today, it was defined in the IEEE 802.2 and 802.3 standards, where it supports data bandwidths from 10 Mb/s upto 100,000 Mb/s (100 Gb/s). Ethernet operates in the [[Data Link Layer]] and the [[Physical Layer]] and relies on the two separate sublayers of the data link layer to operate, the [[Data Link Layer#Logical Link Control LLC| LLC]] and the [[Data Link Layer#Media Access Control MAC|MAC]] sublayers.

## Ethernet Frame
The minimum Ethernet frame size from the Destination MAC address to FCS is 64 bytes and the maximum is 1518 bytes. Frames less than 64 bytes are called a “collision fragment” or “runt frame” and are automatically discarded by receiving stations, where as frames greater than 1500 bytes of data are considered “jumbo” or “baby giant frames”. If the size of a transmitted frame is less than the minimum or greater than the maximum, the receiving device drops the frame.

![](https://www.ionos.com/digitalguide/fileadmin/DigitalGuide/Screenshots_2018/EN-ethernet-frame-structure6.jpg)

## Ethernet MAC Addresses
An Ethernet MAC address is a 48-bit binary value expressed as 12 hexadecimal digits (4 bits per hexadecimal digit), stored in the NIC ROM. They were created to identify the actual source and destination. of data over the network. 

The MAC address rules are established by IEEE which assigns the vendor a 3-byte (24-bit) code, called the Organizationally Unique Identifier (OUI). The IEEE requires a vendor to follow two simple rules:
* All MAC addresses assigned to a [[Network Media#NICs|NIC]] or other Ethernet device must use that vendor's assigned OUI as the first 3 bytes.
* All MAC addresses with the same OUI must be assigned a unique value in the last 3 bytes.

### Unicast MAC Address
A unicast MAC address is the unique address used when a frame is sent from a single transmitting device to a single destination device. For a unicast packet to be sent and received, a destination IP address must be in the IP packet header and a corresponding destination MAC address must also be present in the Ethernet frame header.

### Broadcast MAC Address
A broadcast packet contains the destination IPv4 address that has all the bits being flipped to 1s at the host portion of the IP address(xxx.xxx.x.255), indicating that all devices on the local network will receive and process the packet. When the IPv4 broadcast packet is encapsulated in the Ethernet frame, the destination MAC address is the broadcast MAC address of FF-FF-FF-FF-FF-FF in hexadecimal (48 ones in binary). Broadcast is used in many network protocols such as DHCP, ARP...

### Multicast MAC Address
Multicast addresses allow a source device to send a packet to a group of devices. Devices in a multicast group are assigned a multicast group IP address in the range of 224.0.0.0 to 239.255.255.255, and ends with corresponding multicast MAC address that begins with 01-00-5E and ends in the value of the host part of the multicast IP in hexadecimal (if the multicast IP is 224.0.0.200, the MAC address will be 01-00-5E-XX-XX-C8 where 0xC8=200).