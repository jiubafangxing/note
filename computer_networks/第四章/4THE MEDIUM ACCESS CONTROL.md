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

















