## The Physical Layer
The Physical Layer provides the means to transport the bits that make up a data link layer frame across the network media. It accepts a complete frame from the data link layer and encodes it as a series of signals that are transmitted onto the local media. Encoded bits that comprise a frame are received by either an end device or an intermediate device.

### Physical Layer Medias
There are three types of physical layer medias: [[Network Media#Copper Cables|Copper Wires]], [[Network Media#Fiber Optics|Fiber Optic cables]], and [[Network Media#Wireless Media|Wireless]].

### Functions
The physical layer is responsible for encoding messages from stream of data bits into a predefined signals. It is also responsible for signaling which is the method of representing the bits, the physical layer standards must define what type of signal represents a 1 and what type represents a 0. 

### Bandwidth
The bandwidth is the capacity of a medium to carry data, digital bandwidth measures the amount of data that can flow from one place to the another in a given amount of time. Bandwidth is sometimes thought of as the speed of bits traveling through the wire but this is inaccurate.

The time needed for data to be transmitted is measured by dividing the file size with the bandwidth: $$T_{Transmition} = \frac{F_{file\hspace{0.5mm}size}(bit)} {BW(bit/s)}$$
While the time need for the data to travel from one place to the other:$$T_{prop} = \frac{d(m)}{S(m/s)}$$
### Throughput
Throughput is the measure of the transfer of bits across the media over a given period of time, it usually doesn't match the bandwidth of the physical media carrying the data due to multiple reasons (Amount of allowed traffic by the ISP, Latency, Type of Traffic...) 
*Goodput* is the throughput minus the traffic overhead for establishing sessions, acknowledgments, and encapsulation.