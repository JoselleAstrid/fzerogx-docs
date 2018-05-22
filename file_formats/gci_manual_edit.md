# Manually editing a GCI file

## Checksum basics

The 2-byte checksum is located at 0x40 and 0x41. This is a checksum computed on every byte after 0x41 to the end of the GCI (including zero padding at the end).

A checksum is an error-checking mechanism. Due to the nature of how the checksum is computed, if any byte involved in the checksum computation is changed, the computed checksum is extremely likely to change as well. So if a byte value is changed by some outside force (faulty memory card, cosmic rays, or someone manually trying to change the files) and the checksum value remains the same, the game can detect the unauthorized change and declare the file as corrupt.

What does this mean for manual editing? It means if we make any changes after 0x41 in the GCI file, we need to then update the checksum as well. Otherwise, GX will almost certainly get an error when we try and load the edited GCI file.

## GCI editing steps

- In a hex editor, make any changes you want, and save your changes.
- Recompute the checksum using the below Python code. Let's say that the result is `['CA', '40']`.
- In a hex editor, change byte 0x40 to CA, and byte 0x41 to 40. Save your changes. Now your edited GCI should be ready to use.

## Checksum computation code

Here's how to compute the checksum using Python 3.x; you can enter these three code blocks one by one in IDLE, for instance. Be sure to replace `C:\path\to ...` with your own GCI file path:


```python
import struct
```


```python
def checksum(post_checksum_bytes):
    checksum = 0xFFFF
    generator_polynomial = 0x8408

    for byte_as_number in post_checksum_bytes:
        checksum = checksum ^ byte_as_number

        for i in range(8):
            if checksum & 1 == 1:
                checksum = (checksum >> 1) ^ generator_polynomial
            else:
                checksum = checksum >> 1

    # Flip all the bits
    checksum = checksum ^ 0xFFFF

    return bytearray(struct.pack(">H", checksum))
```


```python
with open(r'C:\path\to\8P-GFZE-f_zero.dat.gci', 'rb') as f:
    _ = f.seek(0x42)
    post_checksum_bytes = f.read()
    print([format(b, 'X') for b in checksum(post_checksum_bytes)])
```
