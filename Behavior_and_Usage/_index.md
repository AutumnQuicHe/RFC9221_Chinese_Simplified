---
title: "5. 行为与用法"
anchor: "5_Behavior_and_Usage"
weight: 500
rank: "h1"
---

When an application sends a datagram over a QUIC connection, QUIC will generate a new DATAGRAM frame and send it in the first available packet. This frame SHOULD be sent as soon as possible (as determined by factors like congestion control, described below) and MAY be coalesced with other frames.

当应用通过QUIC连接发送数据报时，QUIC会创建一个新的**数据报帧**并将它放在首个可用的数据包中发送。这个帧**应该**被尽快发送（主要由拥塞控制等其他因素控制，如下文所述），并且**可以**和其他帧一起被合并。

When a QUIC endpoint receives a valid DATAGRAM frame, it SHOULD deliver the data to the application immediately, as long as it is able to process the frame and can store the contents in memory.

当某个QUIC终端接收到一个合法的**数据报帧**时，只要它有能力处理这个帧并且能够将内容存储在内存中，它就**应该**将数据立即传递给应用。

Like STREAM frames, DATAGRAM frames contain application data and MUST be protected with either 0-RTT or 1-RTT keys.

就像**流帧**一样，**数据报帧**包含着应用数据并且**必须**收到0-RTT或1-RTT密钥的保护。

Note that while the max_datagram_frame_size transport parameter places a limit on the maximum size of DATAGRAM frames, that limit can be further reduced by the max_udp_payload_size transport parameter and the Maximum Transmission Unit (MTU) of the path between endpoints. DATAGRAM frames cannot be fragmented; therefore, application protocols need to handle cases where the maximum datagram size is limited by other factors.

注意，传输参数`max_datagram_frame_size`限制了**数据报帧**的最大尺寸，该限制值可能被传输参数`max_udp_payload_size`和终端间路径的最大传输单元（MTU）进一步限制。**数据报帧**不能被分段；因此，应用协议需要处理最大数据报尺寸被其他因素限制的情况。
