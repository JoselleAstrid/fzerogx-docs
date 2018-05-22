# Save file GCI file format

The first 0x20A0 bytes are covered in: [gci.md](gci.md)

This page describes fields from offset 0x20A0 to the end of the GCI file.

Address | Item | Number of bytes | Format | Notes
--- | --- | --- | --- | ---
0x20A0 | Not yet determined | 448
0x2260 | Encrypted area? | 21346 | | Updating a single Story Mode time makes almost every byte in this section change.
0x75C2 | File name | 8 | String | This is the default name used when you set a top 10 record in Time Attack. If the name is shorter than 8 characters, the remaining bytes get 00.
0x75CA | Not yet determined | ? | | Contents seem to include last-used machine settings and machine IDs.
