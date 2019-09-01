# 4 THE MEDIUM ACCESS CONTROL SUBLAYER 

In any broadcast network, the key issue is how to determine who gets to use  the channel when there is competition for it.

They form the contents of this chapter. In the literature, broadcast channels are sometimes referred to as multiaccess channels or random access channels.

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



**CSMA with Collision Detection **(带冲突检测的载波侦听)

