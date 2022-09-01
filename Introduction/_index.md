---
title: "1. 介绍"
anchor: "1_Introduction"
weight: 100
rank: "h1"
---

The QUIC transport protocol [RFC9000] provides a secure, multiplexed connection for transmitting reliable streams of application data. QUIC uses various frame types to transmit data within packets, and each frame type defines whether the data it contains will be retransmitted. Streams of reliable application data are sent using STREAM frames.

QUIC传输协议（详见《[RFC9000]()》）为传输可靠应用数据的流提供了安全且可多路复用的连接。QUIC在数据包中使用各种不同的帧类型来传输数据，每种帧类型都定义了其中的数据是否需要被重传。可靠应用数据的流是使用**流帧**来发送的。

Some applications, particularly those that need to transmit real-time data, prefer to transmit data unreliably. In the past, these applications have built directly upon UDP [RFC0768] as a transport and have often added security with DTLS [RFC6347]. Extending QUIC to support transmitting unreliable application data provides another option for secure datagrams with the added benefit of sharing the cryptographic and authentication context used for reliable streams.

部分应用，尤其是那些需要传输实时数据的应用，倾向于传输无需可靠性的数据。在过去，这些应用都是直接基于UDP（详见《[RFC0768]()》）建立传输连接，并通常使用DTLS（详见《[RFC6347]()》）来增强安全性。扩展QUIC并使其支持不可靠应用数据的传输，则为安全传输数据报提供了另一种方案，而且还有着共享在可靠流中使用的加密和认证上下文的好处。

This document defines two new DATAGRAM QUIC frame types that carry application data without requiring retransmissions.

本文档定义了两种新的名为**数据报帧**的QUIC帧类型，它们能传递应用数据而无需重传。
