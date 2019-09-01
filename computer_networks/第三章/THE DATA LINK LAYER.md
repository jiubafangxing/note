## 3.1 DATA LINK LAYER DESIGN ISSUES 

1. 向网络层提供一个定义良好的服务接口

2. 处理传输错误

3.  Regulating the flow of data so that slow receivers are not swamped 

   by fast senders.

To accomplish these goals, the data link layer takes the packets it gets from the  network layer and encapsulates them into frames for transmission. Each frame contains a frame header, a payload field for holding the packet, and a frame  trailer

### 3.1.1Services Provided to the Network Layer 

The data link layer can be designed to offer various services 

1. Unacknowledged connectionless service. 
2. Acknowledged connectionless service. 
3. Acknowledged connection-oriented service. 

When connection-oriented service is used, transfers go through three distinct phases. In the first phase, the connection is established by having both sides initialize variables and counters needed to keep track of which frames have been received and which ones have not. In the second phase, one or more frames are actually transmitted. In the third and final phase, the connection is released, freeing up the variables, buffers, and other resources used to maintain the connection. 

### 3.1.2 Framing

A good design must make it easy for a receiver to find the start of new frames while using little of the channel bandwidth. We will look at four methods:

1. Byte count. 
2. Flag bytes with byte stuffing. (This situation would interfere with the framing. One way to solve this problem is to have the sender’s data link layer insert a special escape byte (ESC) just before each ‘‘accidental’’ flag byte in the data.)
3. Flag bits with bit stuffing. (If the user data contain the flag pattern, 01111110, this flag is transmitted as 011111010 but stored in the receiver’s memory as 01111110.)
4.  Physical layer coding violations.

### 3.1.3 Error Control 

The whole issue of managing the timers and sequence numbers so as to ensure  that each frame is ultimately passed to the network layer at the destination exactly  once, no more and no less, is an important part of the duties of the data link layer  (and higher layers). 

### 3.1.4 Flow Control 

**feedback-based flow control **

**rate-based  flow control**

## 3.2 ERROR DETECTION AND CORRECTION 

One strategy is to include enough redundant information to enable the receiver to deduce what the transmitted data must have been. The other is to include only enough redundancy to allow the receiver to deduce that an error has occurred (but not which error) and have it request a retransmission.

**error type**

1. One model is that errors are caused by extreme values of thermal noise that  overwhelm the signal briefly and occasionally, giving rise to isolated single-bit errors.
2. Another model is that errors tend to come in bursts rather than singly. This  model follows from the physical processes that generate them—such as a deep  fade on a wireless channel or transient electrical interference on a wired channel.
3. Sometimes, the location of an error will be  known, perhaps because the physical layer received an analog signal that was far  from the expected value for a 0 or 1 and declared the bit to be lost. This situation  is called an erasure channel

### 3.2.1 Error-Correcting Codes 

We will examine four different error-correcting codes: 

1. Hamming codes. 
2. Binary convolutional codes.
3. Reed-Solomon codes
4. Low-Density Parity Check codes

## 3.5 EXAMPLE DATA LINK PROTOCOLS

### 3.5.1 Packet over SONET

1. A framing method that unambiguously delineates the end of one frame and the start of the next one. The frame format also handles error detection.
2. A link control protocol for bringing lines up, testing them, negotiating options, and bringing them down again gracefully when they are no longer needed. This protocol is called **LCP** (Link Control Protocol).
3. A way to negotiate network-layer options in a way that is independent of the network layer protocol to be used. The method chosen isto have a different **NCP** (**Network Control Protocol**) for each network layer supported.