---
title: "2. 动机"
anchor: "2_Motivation"
weight: 200
rank: "h1"
---

Transmitting unreliable data over QUIC provides benefits over existing solutions:

通过QUIC传输不可靠数据，比起现有的方案，具有以下优势：

* Applications that want to use both a reliable stream and an unreliable flow to the same peer can benefit by sharing a single handshake and authentication context between a reliable QUIC stream and a flow of unreliable QUIC datagrams. This can reduce the latency required for handshakes compared to opening both a TLS connection and a DTLS connection.

* 想要面向同一个对端同时使用可靠流和不可靠流的应用能够在可靠的QUIC流和不可靠的QUIC数据报流间共享相同的握手和认证上下文，从而从中受益。比起既要打开TLS连接又要打开DTLS连接的方案，这能够降低握手过程的延迟。

* QUIC uses a more nuanced loss recovery mechanism than the DTLS handshake. This can allow loss recovery to occur more quickly for QUIC data. 

* QUIC使用的丢包重传机制比起DTLS握手更加敏感。这使得QUIC数据在遭遇丢包后能更快地开始重传。

* QUIC datagrams are subject to QUIC congestion control. Providing a single congestion control for both reliable and unreliable data can be more effective and efficient. 

* QUIC数据报受限于QUIC的拥塞控制。为可靠的和不可靠的数据共用拥塞控制是更加有效且高效的。

These features can be useful for optimizing audio/video streaming applications, gaming applications, and other real-time network applications.

这项特性对于优化音频/视频流应用、游戏应用和其他实时网络应用会很有用。

Unreliable QUIC datagrams can also be used to implement an IP packet tunnel over QUIC, such as for a Virtual Private Network (VPN). Internet-layer tunneling protocols generally require a reliable and authenticated handshake followed by unreliable secure transmission of IP packets. This can, for example, require a TLS connection for the control data and DTLS for tunneling IP packets. A single QUIC connection could support both parts with the use of unreliable datagrams in addition to reliable streams.

不可靠的QUIC数据报还可以被用来实现一种基于QUIC的IP数据包隧道，例如虚拟专用网（VPN）。基于互联网的隧道协议在安全地传输不可靠的IP数据包前通常需要进行可靠且经认证的握手。这可能就需要用到，比如说，一条用于控制数据的TLS连接和用于隧道传输IP数据包的DTLS连接。只要使用不可靠的数据报和可靠的流，那么仅用单条QUIC连接就能够同时满足这两部分要求。
