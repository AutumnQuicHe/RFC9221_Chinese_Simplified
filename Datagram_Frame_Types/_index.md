---
title: "4. 数据报帧的类型"
anchor: "4_Datagram_Frame_Types"
weight: 400
rank: "h1"
---

DATAGRAM frames are used to transmit application data in an unreliable manner. The Type field in the DATAGRAM frame takes the form 0b0011000X (or the values 0x30 and 0x31). The least significant bit of the Type field in the DATAGRAM frame is the LEN bit (0x01), which indicates whether there is a Length field present: if this bit is set to 0, the Length field is absent and the Datagram Data field extends to the end of the packet; if this bit is set to 1, the Length field is present.

**数据报帧**被用来以不可靠的方式传输应用数据。**数据报帧**中的类型字段使用`0b0011000X`的形式（或者说值`0x30`和`0x31`）。**数据报帧**的类型字段的最低有效位被称为`LEN`比特位（掩码为`0x01`），它表示着后方是否存在长度字段；如果该比特位被置为`0`，那么就不存在长度字段，并且数据报数据字段一路延伸至数据包的末尾；如果该比特位被置为`1`，那么就表示后方存在长度字段。

DATAGRAM frames are structured as follows:

**数据报帧**的结构如下：

DATAGRAM Frame {
Type (i) = 0x30..0x31,
[Length (i)],
Datagram Data (..),
}
Figure 1: DATAGRAM Frame Format

{{% block_ref
indx="Figure_1_DATAGRAM_Frame_Format"
title="图1：数据报帧格式" %}}

```
数据报帧 {
  类型 (i) = 0x30..0x31,
  [长度 (i)],
  数据报数据 (..),
}
```

{{% /block_ref %}}

DATAGRAM frames contain the following fields:

**数据报帧**包含着以下字段：

Length:
A variable-length integer specifying the length of the Datagram Data field in bytes. This field is present only when the LEN bit is set to 1. When the LEN bit is set to 0, the Datagram Data field extends to the end of the QUIC packet. Note that empty (i.e., zero-length) datagrams are allowed.

长度：

:   一个可变长度整型，标示着数据报数据字段以字节为单位的长度。只有当`LEN`比特位被置为`1`时，该字段才存在。当`LEN`比特位被置为`0`时，数据报数据字段一路延伸至QUIC数据包的末尾。注意，空数据报（也就是零长度）是被允许的。

Datagram Data:
The bytes of the datagram to be delivered.

数据报数据：

:   正在传递的数据报字节。
