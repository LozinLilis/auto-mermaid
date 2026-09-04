# Packet Diagram

Syntax authority: the official default example below (`@mermaid-js/examples` 1.4.0, MIT; keyword `---`).

## Default example: TCP Packet

```mermaid
---
title: "TCP Packet"
---
packet
0-15: "Source Port"
16-31: "Destination Port"
32-63: "Sequence Number"
64-95: "Acknowledgment Number"
96-99: "Data Offset"
100-105: "Reserved"
106: "URG"
107: "ACK"
108: "PSH"
109: "RST"
110: "SYN"
111: "FIN"
112-127: "Window"
128-143: "Checksum"
144-159: "Urgent Pointer"
160-191: "(Options and Padding)"
192-255: "Data (variable length)"
```

## Fit

Bit ranges of protocol packets and binary layouts: fields, widths, order, meaning.

## Rules

- Bit ranges are contiguous and unambiguous; state whether numbering starts at 0 or 1.
- Field names, widths, endianness, reserved bits match the protocol spec.
- Line breaks for readability must not shift real offsets.

## Avoid

Do not draw field tables as flows; never adjust widths or drop reserved fields for cosmetics.
