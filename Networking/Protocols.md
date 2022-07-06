# Protocols
Protocols are necessary for effective communication between devices and include an identified sender and receiver, speed and timing of delivery, confirmation or acknowledgment requirements. They also define message encoding, message delivery options, message formatting, message size, and message timing. 

## Protocol Responsibilities
### Message Encoding
Encoding between hosts must be in appropriate format for the media the message will be sent on. The message is first converted into bits and then the each bit is encoded into a pattern of sound, light waves, or electrical impulses based on the network media it is being sent on. And at the destination the host decodes the signal in order to interpret the message.

### Message Formatting And Encapsulation
Each computer message is encapsulated in a specific format, called a frame, before it is sent over the network. A frame acts like an envelop providing destination address and source address.

### Message Size
Messages are broken into smaller piece to travel over the network, each piece is sent in a separate frame, with each frame having its own addressing information. A receiving host will reconstruct multiple frames into the original message.

### Message Timing
Message timing is important to be defined in a protocol, it allows for definition of *Access Method* which allow the device to know when to begin sending a message and how to respond when collision occurs. *Flow Control* which allows the source and destination to negotiate the correct timing to avoid overwhelming the destination and ensure information is received. And *Response Timeout* which allow the devices to know how long to wait for responses and what actions to take if a response timeout occurs.

### Message Delivery Options
Their are three main options for message delivery options:
* *Unicast Message:* Which is a message sent from one device to another device on the network.
* *Multicast Message:* Which is a message sent from one device to multiple other devices on the network.
* *Broadcast Message:* Which is a message sent from one device to all the other devices on the network.

### De-Encapsulation
The de-encapsulation process works from bottom to top, de-encapsulation is the process used by a receiving device to remove one or more of the protocol headers. The data is de-encapsulated as it moves up the stack towards the end-user application.

### Message Segmentation
Large streams of data are divided into smaller, more manageable pieces to send over the network. By sending smaller pieces, many different conversations can be interleaved on the network, called multiplexing. Each piece must be labeled. If part of the message fails to make it to the destination, only the missing pieces need to be retransmitted.

## Protocol Standards
Protocols and standards are implemented by hosts and networking devices manufacturers. Protocols are viewed in terms of layers, with each higher level service depending on the functionality provided by the protocols shown in the lower levels.

Communication between a web server and a web client is a process of interaction between multiple protocols:
* **HTTP:** An application protocol that governs the way a web server and a client interact.
* **TCP:** Transport protocol that manages the individual conversations.
* **IP:** Encapsulates the TCP segments into packets and assigns addresses, and delivers to the destination host.
* **Ethernet:** Allows communication over a data link and the physical transmission of data on the network media.

### Protocol Suits
A protocol suite is a set of protocols that work together to provide a comprehensive network communication services. The TCP/IP suite is an open standard, the protocols are freely available, and any vendor is able to implement these protocols on their hardware or in their software.

## Protocol Data Units
As application data is passed down the protocol stack, information is added at each level. This is known as encapsulation. The form that the data takes at each layer is known as Protocol Data Unit.
* *Data:* Application Layer PDU.
* *Segment:* Transport Layer PDU.
* *Packet:* [[Network Layer]] PDU.
* *Frame:* [[Data Link Layer]] PDU.
* *Bits:* [[Physical Layer]] PDU.
