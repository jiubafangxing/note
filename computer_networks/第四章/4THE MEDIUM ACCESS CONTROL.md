---
typora-root-url: ..\images
---

# 4 THE MEDIUM ACCESS CONTROL SUBLAYER 

​	In any broadcast network, the key issue is how to determine who gets to use  the channel when there is competition for it.

​	They form the contents of this chapter. In the literature, broadcast channels are sometimes referred to as multiaccess channels or random access channels.

### 4.1.2 Assumptions for Dynamic Channel Allocation 

信道分配需要注意的五个关键点

1. Independent Traffic.
2. Single Channel 
3. Observable Collisions 
4. Continuous or Slotted Time. 
5. Carrier Sense or No Carrier Sense 



## 4.2 MULTIPLE ACCESS PROTOCOLS

### 4.2.2 Carrier Sense Multiple Access Protocols 

**1-persistent  CSMA (Carrier Sense Multiple Access)**

​	The protocol is  called 1-persistent because the station transmits with a probability of 1 when it  finds the channel idle.

**nonpersistent CSMA **

​	 However, if the channel is already in  use, the station does not continually sense it for the purpose of seizing it immediately upon detecting the end of the previous transmission. Instead, it waits a  random period of time and then repeats the algorithm.

**p-persistent CSMA **

"P-坚持"算法的规则如下：  （1）如果介质空闲，则以P概率发送数据（注意，只是一种概率，而不是马上发送数据），而以（1-P）的概率延迟一个时间单位t，t等于最大信号传播时延的两倍。  （2）站点的发送已被延迟一个时间单位t后，则重复上述步骤（1），当然这时的P值可能不一样。  （3）如果介质是忙的，继续侦听直到介质处于空闲状态，然后重复上述步骤（1）。 



**CSMA with Collision Detection **(CSMA/CD 带冲突检测的载波侦听，或者叫总线型拓扑 )

CSMA/CD媒体访问控制方法的工作原理，可以概括如下：

先听后说，边听边说；

一旦冲突，立即停说；

等待时机，然后再说；

注：“听”，即监听、检测之意；“说”，即发送数据之意

这里的冲突检测不就是我们日常谈论的锁吗？



**4.2.3 Collision-Free Protocols **

何其相似，无锁编程？

**A Bit-Map Protocol(基本位图协议)**

​	In our first collision-free protocol, the basic bit-map method, each contention period consists of exactly N slots. If station 0 has a frame to send, it transmits a 1 bit during the slot 0. No other station is allowed to transmit during this slot. Regardless of what station 0 does, station 1 gets the opportunity to transmit a 1 bit during slot 1, but only if it has a frame queued.

**Token Passing (令牌传递)**

​	The essence of the bit-map protocol is that it lets every station transmit a  frame in turn in a predefined order. Another way to accomplish the same thing is  to pass a small message called a token from one station to the next in the same  predefined order. The token represents permission to send. If a station has a  frame queued for transmission when it receives the token, it can send that frame  before it passes the token to the next station. If it has no queued frame, it simply  passes the token.

**Binary Countdown(二进制倒计数)**

​	To avoid conflicts, an arbitration rule must be applied: as soon as a station sees that a high-order bit position that is 0 in its address has been overwritten with a 1, it gives up. For example, if stations 0010, 0100, 1001, and 1010 are all trying to get the channel, in the first bit time the stations transmit 0, 0, 1, and 1, respectively. These are ORed together to form a 1. Stations 0010 and 0100 see the 1 and know that a higher-numbered station is competing for the channel, so they give up for the current round. Stations 1001 and 1010 continue. 

### 4.2.4 Limited-Contention Protocols（有限竞争协议）

​	Obviously, it would be nice if we could combine the best properties of the  contention and collision-free protocols, arriving at a new protocol that used contention at low load to provide low delay, but used a collision-free technique at  high load to provide good channel efficiency. Such protocols, which we will call  **limited-contention protocols**, do in fact exist, and will conclude our study of carrier sense networks. 

**The Adaptive Tree Walk Protocol (自适应树遍历协议)**

​	One particularly simple way of performing the necessary assignment is to use the algorithm devised by the U.S. Army for testing soldiers for syphilis during World War II (Dorfman, 1943). In short, the Army took a blood sample from N soldiers. A portion of each sample was poured into a single test tube. This mixed sample was then tested for antibodies. If none were found, all the soldiers in the group were declared healthy. If antibodies were present, two new mixed samples were prepared, one from soldiers 1 through N/2 and one from the rest. The process was repeated recursively until the infected soldiers were determined. 

### 4.2.5 Wireless LAN Protocols（无限局域网协议） 

**difference between wireless LANs and wired LANs**

1. We have already remarked that wireless systems cannot normally detect a collision while it is occurring.
2. A station on a wireless LAN may not be able to transmit frames to or receive frames from all other stations because of the limited radio range of the stations.

 The problem of a station not being able to detect a potential competitor for the medium because the competitor is too far away is called **the hidden terminal problem(隐藏终端问题).** 

 We want a MAC protocol that prevents this kind of deferral from happening because it wastes bandwidth. The problem is called **the exposed terminal problem.（暴露终端问题） **

An early and influential protocol that tackles these problems for wireless LANs is MACA (**Multiple Access with Collision Avoidance避免冲突的多路访问**) (Karn, 1990). 

## 4.3 ETHERNET 

### 4.3.1 Classic Ethernet Physical Layer 

​	Each version of Ethernet has a maximum cable length per segment (i.e., unamplified length) over which the signal will propagate. To allow larger networks, multiple cables can be connected by **repeaters（中继器）**. 

**4.3.2 Classic Ethernet MAC Sublayer Protocol（经典MAC网子层协议)**

![经典网络mac子层协议](/forth/经典网络mac子层协议.jpg)

**CSMA/CD with Binary Exponential Backoff (二进制指数回退的CSMA/CD)**

​	Let us now see how the random interval is determined when a collision  occurs, as it is a new method. The model is still that of Fig. 4-5. After a collision,  time is divided into discrete slots whose length is equal to the worst-case round trip propagation time on the ether (2τ). To accommodate the longest path allowed by Ethernet, the slot time has been set to 512 bit times, or 51.2 μsec.  After the first collision, each station waits either 0 or 1 slot times at random  before trying again. If two stations collide and each one picks the same random  number, they will collide again. After the second collision, each one picks either  0, 1, 2, or 3 at random and waits that number of slot times. If a third collision  occurs (the probability of this happening is 0.25), the next time the number of  slots to wait is chosen at random from the interval 0 to 2^(3 − 1).

​	In general, after i collisions, a random number between 0 and 2^(i − 1) is chosen,  and that number of slots is skipped. However, after 10 collisions have been  reached, the randomization interval is frozen at a maximum of 1023 slots. After  16 collisions, the controller throws in the towel and reports failure back to the  computer. Further recovery is up to higher layers.

​	If there is no collision, the sender assumes that the frame was probably successfully delivered. That is, neither CSMA/CD nor Ethernet provides acknowledgements. This choice is appropriate for wired and optical fiber channels that have low error rates. Any errors that do occur must then be detected by the CRC and recovered by higher layers. For wireless channels that have more errors, we will see that acknowledgements are used.

### 4.3.4 Switched Ethernet 

However, if the cable is half duplex, the station and the port must contend for  transmission with CSMA/CD in the usual way. （why????）

### 4.3.5 Fast Ethernet 

### 4.3.6 Gigabit Ethernet 

### 4.3.7 10-Gigabit Ethernet 

### 4.3.8 Retrospective on Ethernet 

## 4.4 WIRELESS LANS 

### 4.4.1 The 802.11 Architecture and Protocol Stack 

802.11 networks can be used in two modes:

1. In infrastructure mode, each client is associated with an AP (Access Point) that is in turn connected to the other network
2. The other mode, shown in Fig. 4-23(b), is an ad hoc network(自组织网络). 

![2modelsOfWirelessNetwork](/forth/2modelsOfWirelessNetwork.jpg)



### 4.4.2 The 802.11 Physical Layer 

### 4.4.3 The 802.11 MAC Sublayer Protocol 

​	Instead, 802.11 tries to avoid collisions with a protocol called CSMA/CA (CSMA with Collision Avoidance). This protocol is conceptually similar to Ethernet’s CSMA/CD, with channel sensing before sending and exponential back off after collisions.

​	Compared to Ethernet, there are two main differences. First, starting backoffs early helps to avoid collisions. The second problem is that the transmission ranges of different stations may be different.

​	CSMA/CA with physical and virtual sensing is the core of the 802.11 protocol. However, there are several other mechanisms that have been developed to go with it. Each of these mechanisms was driven by the needs of real operation, so we will look at them briefly. 

1. The first need we will look at is reliability.  
2. The second need we will discuss is saving power.  **beacon frames **  **APSD (Automatic Power Save Delivery)**
3. The third and last need we will examine is quality of service 



![间隔时间定义](/forth/间隔时间定义.jpg)



### 4.4.4 The 802.11 Frame Structure 

​	The 802.11 standard defines three different classes of frames in the air: data, control, and management.

![802.11数据帧结构](/forth/802.11数据帧结构.jpg)



### 4.4.5 Services 

​	The 802.11 standard defines the services that the clients, the access points, and the network connecting them must be a conformant wireless LAN. These services cluster into several groups.

1. **The association service (关联服务)** is used by mobile stations to connect themselves to APs.
2. **Reassociation(重新连接)** lets a station change its preferred AP 
3. Once frames reach the AP, the **distribution service** determines how to route them.
4. Data transmission is what it is all about, so 802.11 naturally provides a **data delivery service** .
5. Wireless is a broadcast signal. For information sent over a wireless LAN to  be kept confidential, it must be encrypted. This goal is accomplished with a  **privacy service** that manages the details of encryption and decryption.
6. To handle traffic with different priorities, there is a **QOS traffic scheduling  service**.
7. Finally, there are two services that help stations manage their use of the spectrum. The transmit power control service gives stations the information they  need to meet regulatory limits on transmit power that vary from region to region.  The dynamic frequency selection service give stations the information they need  to avoid transmitting on frequencies in the 5-GHz band that are being used for  radar in the proximity.

## 4.8 数据联络层交换

网桥通过泛洪算法(Flooding Algorithm) 以及后向学习法对带来的帧进行路由。

网桥的路由转换方式被称为直通式交换（Cut-through switching）或虫孔路由（wormhole routing）

网桥之间的通讯通过生成树解决环路问题

























