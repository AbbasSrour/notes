# Address Resolution Protocol
To determine the MAC address of the destination device that the source device wants to connect with, it uses the AR Protocol. The ARP provides two functions, getting the IPv4 for a given MAC address and maintaining a table of mappings. 

The ARP sends a broadcast frame with the source and destination IP, with the source IP being the device's IP and the destination IP being the targeted device IP. In the [[Data Link Layer]] headers the device will put its MAC address in the source part and the broadcast MAC Address in the destination header. The frame will be sent to all devices in the network and the targeted device will respond to the request. The MAC address will be saved in the source device ARP table for around 2 minutes and the table can be accessed through the command `arp -a` on a windows host and `show ip arp` on a router.

## ARP Spoofing 
One type of ARP spoofing attack used by attackers is to reply to an ARP request for the default gateway.  Host A cam request the MAC address of the default gateway, which then the attacker replies to the ARP request with its IP and MAC address. Host A receives the reply and updates its ARP table. It now sends packets destined to the default gateway to the attacker. Enterprise level switches include mitigation techniques known as dynamic ARP inspection (DAI) to counter these attacks.
