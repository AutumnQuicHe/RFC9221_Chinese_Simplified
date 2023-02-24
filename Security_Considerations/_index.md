---
title: "6. 关于安全性的考量"
anchor: "6_Security_Considerations"
weight: 600
rank: "h1"
---

**数据报帧**与在同一QUIC连接中发送的其他数据共享相同的安全属性，并且都适用于《[RFC9000](../RFC9000_Chinese_Simplified)》中描述的安全性上的考量。
所有用**数据报帧**传输的应用数据都，像**流帧**一样，{{< req_level MUST >}}受到0-RTT或1-RTT密钥的保护。

允许在0-RTT中发送**数据报帧**的应用协议需要定义0-RTT的使用范围；详见《[RFC9001](../RFC9001_Chinese_Simplified)》的[第5.6章](../RFC9001_Chinese_Simplified/#5.6_Use_of_0-RTT_Keys)。

路径上的有能力丢弃数据包的中间设备可以检测到**数据报帧**的使用与否。
由于**数据报帧**不需要使用传输层的重传，因此**数据报帧**对待数据包丢包的与众不同的响应行为可能令使用了该帧的连接被区分出来。
