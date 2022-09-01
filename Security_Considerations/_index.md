---
title: "6. 安全性上的考量"
anchor: "6_Security_Considerations"
weight: 600
rank: "h1"
---

The DATAGRAM frame shares the same security properties as the rest of the data transmitted within a QUIC connection, and the security considerations of [RFC9000] apply accordingly. All application data transmitted with the DATAGRAM frame, like the STREAM frame, MUST be protected either by 0-RTT or 1-RTT keys.

**数据报帧**与在同一QUIC连接中发送的其他数据共享相同的安全属性，并且都适用于《[RFC9000]()》中描述的安全性上的考量。所有用**数据报帧**传输的应用数据都，像**流帧**一样，**必须**受到0-RTT或1-RTT密钥的保护。

Application protocols that allow DATAGRAM frames to be sent in 0-RTT require a profile that defines acceptable use of 0-RTT; see Section 5.6 of [RFC9001].

允许在0-RTT中发送**数据报帧**的应用协议需要定义0-RTT的使用范围；详见《[RFC9001]()》的[第5.6章]()。

The use of DATAGRAM frames might be detectable by an adversary on path that is capable of dropping packets. Since DATAGRAM frames do not use transport-level retransmission, connections that use DATAGRAM frames might be distinguished from other connections due to their different response to packet loss.

路径上的有能力丢弃数据包的中间设备可以检测到**数据报帧**的使用与否。由于**数据报帧**不需要使用传输层的重传，因此**数据报帧**对待数据包丢包的与众不同的响应行为可能令使用了该帧的连接被区分出来。
