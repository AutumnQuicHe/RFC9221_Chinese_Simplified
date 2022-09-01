---
title: "3. 传输参数"
anchor: "3_Transport_Parameter"
weight: 300
rank: "h1"
---

Support for receiving the DATAGRAM frame types is advertised by means of a QUIC transport parameter (name=max_datagram_frame_size, value=0x20). The max_datagram_frame_size transport parameter is an integer value (represented as a variable-length integer) that represents the maximum size of a DATAGRAM frame (including the frame type, length, and payload) the endpoint is willing to receive, in bytes.

对**数据报帧**的支持是通过某个QUIC传输参数（名为`max_datagram_frame_size`，ID为`0x20`）来告知对端的。传输参数`max_datagram_frame_size`是一个整型值（用可变长度整型来表示），它表示着**数据报帧**的最大尺寸。

The default for this parameter is 0, which indicates that the endpoint does not support DATAGRAM frames. A value greater than 0 indicates that the endpoint supports the DATAGRAM frame types and is willing to receive such frames on this connection.

默认情况下，该参数的值为0，这表示终端不支持**数据报帧**。大于0的值则表示终端支持**数据报帧**并且愿意在此连接中接收**数据报帧**。

An endpoint MUST NOT send DATAGRAM frames until it has received the max_datagram_frame_size transport parameter with a non-zero value during the handshake (or during a previous handshake if 0-RTT is used). An endpoint MUST NOT send DATAGRAM frames that are larger than the max_datagram_frame_size value it has received from its peer. An endpoint that receives a DATAGRAM frame when it has not indicated support via the transport parameter MUST terminate the connection with an error of type PROTOCOL_VIOLATION. Similarly, an endpoint that receives a DATAGRAM frame that is larger than the value it sent in its max_datagram_frame_size transport parameter MUST terminate the connection with an error of type PROTOCOL_VIOLATION.

除非终端在握手期间（或上一次握手期间，如果使用了0-RTT）接收到了非零的传输参数`max_datagram_frame_size`，否则它**必须不**发送**数据报帧**。终端发送的**数据报帧**尺寸**必须不**超过它从对端接收到的`max_datagram_frame_size`值。没有通过传输参数表明支持**数据报帧**就接收到**数据报帧**的终端**必须**使用类型为`PROTOCOL_VIOLATION`（协议违背）的错误终止连接。类似地，如果终端接收到的**数据报帧**尺寸超过了它发送的传输参数`max_datagram_frame_size`的值，那么它**必须**使用类型为`PROTOCOL_VIOLATION`的错误终止连接。

For most uses of DATAGRAM frames, it is RECOMMENDED to send a value of 65535 in the max_datagram_frame_size transport parameter to indicate that this endpoint will accept any DATAGRAM frame that fits inside a QUIC packet.

对于大多数**数据报帧**的使用场景，**推荐**用值为`65535`的传输参数`max_datagram_frame_size`来表明终端愿意接受所有能够放进QUIC数据包的**数据报帧**。

The max_datagram_frame_size transport parameter is a unidirectional limit and indication of support of DATAGRAM frames. Application protocols that use DATAGRAM frames MAY choose to only negotiate and use them in a single direction.

传输参数`max_datagram_frame_size`是一个单向的限制，并且表明着对**数据报帧**是否支持。使用**数据报帧**的应用协议**可以**选择仅在单一方向上协商与使用这种帧。

When clients use 0-RTT, they MAY store the value of the server's max_datagram_frame_size transport parameter. Doing so allows the client to send DATAGRAM frames in 0-RTT packets. When servers decide to accept 0-RTT data, they MUST send a max_datagram_frame_size transport parameter greater than or equal to the value they sent to the client in the connection where they sent them the NewSessionTicket message. If a client stores the value of the max_datagram_frame_size transport parameter with their 0-RTT state, they MUST validate that the new value of the max_datagram_frame_size transport parameter sent by the server in the handshake is greater than or equal to the stored value; if not, the client MUST terminate the connection with error PROTOCOL_VIOLATION.

当客户端使用0-RTT时，它们**可以**存储来自服务器的传输参数`max_datagram_frame_size`的值。这么做使得客户端可以在0-RTT数据包中发送**数据报帧**。当服务器决定接收0-RTT数据时，它们发送的传输参数`max_datagram_frame_size `的值**必须**大于等于它们曾在发送了`NewSessionTicket`消息的连接中发送给客户端的值。如果客户端存储了传输参数`max_datagram_frame_size`的值和它们的0-RTT状态数据，那么它们**必须**验证服务器在握手时新发送的传输参数`max_datagram_frame_size`的值，确保它大于等于客户端存储的旧值；如若不然，客户端**必须**使用类型为`PROTOCOL_VIOLATION`的错误终止连接。

Application protocols that use datagrams MUST define how they react to the absence of the max_datagram_frame_size transport parameter. If datagram support is integral to the application, the application protocol can fail the handshake if the max_datagram_frame_size transport parameter is not present.

使用数据报的应用协议**必须**定义在缺失传输参数`max_datagram_frame_size`时的行为。如果对数据报的支持对于应用至关重要，那么应用协议在传输参数`max_datagram_frame_size`缺失时可以使握手失败。
