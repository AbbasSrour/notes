# NICs
Before network communication can occur, a physical connection to a local network must be established. A physical connection can be a wired connection using a cable or a wireless connection using ratio waves.

**NICs** or Network Interface Cards connect a device to a network, they are used for wired connections. While Wireless Local Area **WLAN** are used for wireless connection.

# Copper Cables
Copper wires transmit bits as electrical pulses.
## Coaxial Cable
Coax consists of a copper conductor used to transmit the electronic signals, a layer of flexible plastic insulation surrounding the copper conductor, a woven copper braid or metallic foil that acts as the second wire in the circuit and as a shield for the inner conductor, and a cable jacket that covers the entire to prevent minor physical damage. UTP cable has essentially replaced coaxial cable in modern Ethernet installations, but it's still being used in *Wireless Installations,* like connecting antennas to wireless devices and *Cable Internet Installations*.

## UTP And STP
### Problems
* **Attenuation:** Which is that the longer the signal travels the more it deteriorates. The maximum distance of a copper wire is 100 meters before needing a repeater, with 70 meters being the sweet spot. 
* **Radiation:** *Electromagnetic Interface(EMI)* and *Radio Frequency Interface(RFI)* are radiations that distort and corrupt the signals carried by copper wires which is why some copper wires counter that by being wrapped in shielding. 
* **Crosstalk:** Disturbance caused by the electric or magnetic fields of a signal on one wire to the signal in an adjacent wire, and to cancel that copper wires with opposing circuit are wrapper together in pairs.

### Unshielded Twisted Pair
 UTP cabling is the most common networking media,  used for interconnecting network hosts with networking devices such as switches. UTP consists of four pairs of color-coded wires that have been twisted together to help protect against signal interference from other wires, with color codes to aid in cable termination.
 
### Shielded Twisted Pair
 STP provides better noise protection than UTP, but at the cost of being significantly more expensive and difficult to install. It combines the techniques of shielding to counter EMI and RFI, and wire twisting to counter crosstalk.  Similar to UTP, it consists of four pairs of wires, each wrapped in a foil shield, which are then wrapped in an overall metallic braid or foil.
 
### Standards
   UTP cabling conforms to the standards established by TIA/EIA, which stipulates the cabling standards for LAN installations. The generations of UTP/STP cables:
   * Cat 3 Cable: Used for voice communication like phone lines.
  * Cat 5 and 5e Cable: Which is used for data transmission, with Cat5 supporting a recommended maximum bandwidth of 100 Mb/s upto an unrecommended 1000Mb/s, with
   Cat5e supporting upto 1000 Mb/s.
   * Cat 6 Cable: Used also for data transmission with an added separator between each pair of wires allowing it to function at higher speeds, support a bandwidth between 1000 Mb/s – 10 Gb/s, with 10 Gb/s is being unrecommended.

### Connectors
UTP cable terminated with a male component called the RJ-45 connector. which is crimped at the end of the cable. The Socket is the female component of a network device, wall, cubicle partition outlet, or patch panel. It is that Essential that all copper media terminations be of high quality to ensure optimum performance with current and future network technologies.


# Fiber Optics
Transmits data over longer distances and at higher bandwidths, with the signals being less prone to attenuation and completely immune to EMI and RFI. Fiber optics are used to interconnect network devices. They consist of flexible, but extremely thin, transparent strand of very pure glass, not much bigger than a human hair, with the sent through them being encoded on the fiber as light pulses.

Light can only travel in one direction over optical fiber, two fibers are required to support the full duplex operation.
## Connectors
* **Straight Tip (STP):** One of the first connector types used, locks securely with a “twist-on/twist-off”.
* **Subscriber Connector(SC):** -   Referred to as square or standard connector, uses a push-pull mechanism to ensure positive insertion, and has multimode and single-mode fiber, where multimode allows the sending multiple lights with increases speed but decreases range.
* **Lucent Connector(LC):** Smaller version of SC and popular due to its size.
* **Duplex Multimode LC:** Similar to LC but uses a duplex connector, which allows sending and receiving data.

Fiber patch cords are required for interconnecting infrastructure devices, where
Yellow jacket is for single-mode fiber cables and orange (or aqua) for multimode fiber cables. Fiber cables should be protected with a small plastic cap when not in use.

# Wireless Media 
Wireless media carry electromagnetic signals that represent the binary digits of data communications using radio or microwave frequencies. Wireless areas of concern:
- **Coverage Area:** Construction materials used in buildings and structures, and the local terrain, will limit the coverage.
- **Interference:** Disrupted by such common devices as fluorescent lights, microwave ovens, and other wireless communications.
- **Security:** Devices and users, not authorized for access to the network, can gain access to the transmission.
- **Shared Medium:** Only one device can send or receive at a time and the wireless medium is shared among all wireless users.

## Types
- **WiFi Standard IEEE 802.11:** Uses Carrier/Sense Multiple Access/Collision Avoidance (CSMA/CA). Wireless NIC must wait till channel is clear. WiFi is a type of WLAN.
- **Bluetooth Standard IEEE 802.15:** It uses Wireless Personal Area Network (WPAN) for pairing and sharing data with a device pairing process for distances 1 to 100 meters
- **WiMAX Standard IEEE 802.16:** Worldwide Interoperability for Microwave Access, it allows for wireless broadband access. Similar to 4G networks.
- **WLAN:** Wireless local area networking, also known as WLAN or wireless LAN, is a term for using wireless digital signals to connect computers and other devices.  It requires a   *Wireless Access Point (AP)* which concentrates the wireless signals from users and connects to the existing copper-based network infrastructure, such as Ethernet, and a *Wireless NIC adapters* which provides wireless communication capability to each network host.