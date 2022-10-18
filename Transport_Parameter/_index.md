---
title: "3. 传输参数"
anchor: "3_Transport_Parameter"
weight: 300
rank: "h1"
---

对**数据报帧**的支持是通过某个QUIC传输参数（名为`max_datagram_frame_size`，ID为`0x20`）来告知对端的。
传输参数`max_datagram_frame_size`是一个整型值（用可变长度整型来表示），它表示着**数据报帧**的最大尺寸。

默认情况下，该参数的值为0，这表示终端不支持**数据报帧**。
大于0的值则表示终端支持**数据报帧**并且愿意在此连接中接收**数据报帧**。

除非终端在握手期间（或上一次握手期间，如果使用了0-RTT）接收到了非零的传输参数`max_datagram_frame_size`，否则它{{< req_level MUST_NOT >}}发送**数据报帧**。
终端发送的**数据报帧**尺寸{{< req_level MUST_NOT >}}超过它从对端接收到的`max_datagram_frame_size`值。
没有通过传输参数表明支持**数据报帧**就接收到**数据报帧**的终端{{< req_level MUST >}}使用类型为`PROTOCOL_VIOLATION`（协议违背）的错误终止连接。
类似地，如果终端接收到的**数据报帧**尺寸超过了它发送的传输参数`max_datagram_frame_size`的值，那么它{{< req_level MUST >}}使用类型为`PROTOCOL_VIOLATION`的错误终止连接。

对于大多数**数据报帧**的使用场景，{{< req_level RECOMMENDED >}}用值为`65535`的传输参数`max_datagram_frame_size`来表明终端愿意接受所有能够放进QUIC数据包的**数据报帧**。

传输参数`max_datagram_frame_size`是一个单向的限制，并且表明着对**数据报帧**是否支持。
使用**数据报帧**的应用协议{{< req_level MAY >}}选择仅在单一方向上协商与使用这种帧。

当客户端使用0-RTT时，它们{{< req_level MAY >}}存储来自服务器的传输参数`max_datagram_frame_size`的值。
这么做使得客户端可以在0-RTT数据包中发送**数据报帧**。
当服务器决定接收0-RTT数据时，它们发送的传输参数`max_datagram_frame_size `的值{{< req_level MUST >}}大于等于它们曾在发送了`NewSessionTicket`消息的连接中发送给客户端的值。
如果客户端存储了传输参数`max_datagram_frame_size`的值和它们的0-RTT状态数据，那么它们{{< req_level MUST >}}验证服务器在握手时新发送的传输参数`max_datagram_frame_size`的值，确保它大于等于客户端存储的旧值；如若不然，客户端{{< req_level MUST >}}使用类型为`PROTOCOL_VIOLATION`的错误终止连接。

使用数据报的应用协议{{< req_level MUST >}}定义在缺失传输参数`max_datagram_frame_size`时的行为。
如果对数据报的支持对于应用至关重要，那么应用协议在传输参数`max_datagram_frame_size`缺失时可以使握手失败。
