# Racer block 2


## Memory location and layout

There's one memory block for each race participant. The blocks seem to be of size 0x760 for human racers, and 0x820 for CPU racers. The blocks come one after the other.
 
Calculation for the first block's address:

- Pointer = \[[Start of racer block 1 array](racer_block_1.md) - 0x20\]
  
- First block's address = Start address + Pointer - 0x80000000

Block order in races with multiple machines: TODO


## Block items

In general, this block isn't documented as well as [Racer block 1](racer_block_1.md).

Item | Offset | Bytes | Format | Notes
--- | --- | --- | --- | ---
Pointer to 0xE0 | 0x0 | 4 | Address
| - | 0x4 | - | -
Checkpoint number | 0x74 | 4 | Integer
Checkpoint number at intersections | 0x78 | 4 | Integer
| - | 0x7C | - | -
Checkpoint number | 0xD0 | 4 | Integer
Checkpoint number at intersections | 0xD4 | 4 | Integer
| - | 0xD8 | - | -
Pointer to 0x1C0 | 0xE0 | 4 | Address
Pointer to 0x0 | 0xE4 | 4 | Address
| - | 0xE8 | - | -
Checkpoint number | 0x154 | 4 | Integer
Checkpoint number at intersections | 0x158 | 4 | Integer
| - | 0x15C | - | -
Checkpoint number | 0x1B0 | 4 | Integer
Checkpoint number at intersections | 0x1B4 | 4 | Integer
| - | 0x1B8 | - | -
Pointer to 0x2A0 | 0x1C0 | 4 | Address
| - | 0x1C4 | - | -
Checkpoint number | 0x234 | 4 | Integer
Checkpoint number at intersections | 0x238 | 4 | Integer
| - | 0x23C | - | -
Checkpoint number | 0x290 | 4 | Integer
Checkpoint number at intersections | 0x294 | 4 | Integer
| - | 0x298 | - | -
Pointer to 0x380 | 0x2A0 | 4 | Address
| - | 0x2A4 | - | -
Checkpoint number | 0x314 | 4 | Integer
Checkpoint number at intersections | 0x318 | 4 | Integer
| - | 0x31C | - | -
Pointer associated with current track piece? | 0x340 | 4 | Address
| - | 0x344 | - | -
Track width | 0x350 | 4 | Float
| - | 0x354 | - | -
Checkpoint number | 0x370 | 4 | Integer
Checkpoint number at intersections | 0x374 | 4 | Integer
| - | 0x378 | - | -
Pointer to 0x540 | 0x380 | 4 | Address
| - | 0x384 | - | -
Pointer associated with current track piece? | 0x3A4 | 4 | Address
Pointer associated with current track piece? | 0x3A8 | 4 | Address
Pointer associated with current track piece? | 0x3AC | 4 | Address
Pointer associated with current track piece? | 0x3B0 | 4 | Address
Pointer associated with current track piece? | 0x3B4 | 4 | Address
| - | 0x3B8 | - | -
Pointer to next racer's block | 0x540 | 4 | Address
Pointer to 0x380 | 0x544 | 4 | Address
| - | 0x548 | - | -
Rightward vector at center of track, X | 0x560 | 4 | Float
Up vector at center of track, X | 0x564 | 4 | Float
Backward vector at center of track, X | 0x568 | 4 | Float
Center of track, X | 0x56C | 4 | Float
Rightward vector at center of track, Y | 0x570 | 4 | Float
Up vector at center of track, Y | 0x574 | 4 | Float
Backward vector at center of track, Y | 0x578 | 4 | Float
Center of track, Y | 0x57C | 4 | Float
Rightward vector at center of track, Z | 0x580 | 4 | Float
Up vector at center of track, Z | 0x584 | 4 | Float
Backward vector at center of track, Z | 0x588 | 4 | Float
Center of track, Z | 0x58C | 4 | Float
Track width | 0x590 | 4 | Float
200 or 400 in BBO, <= 200 in SOSS | 0x594 | 4 | Float
200 or 400 in BBO, <= 200 in SOSS | 0x598 | 4 | Float
| - | 0x59C | - | -
Center of track | 0x5A4 | 12 | Float 3D vector
Forward vector at center of track | 0x5B0 | 12 | Float 3D vector
Up vector at center of track | 0x5BC | 12 | Float 3D vector
Track width | 0x5C8 | 4 | Float
Always 1? | 0x5CC | 4 | Float
Center of track | 0x5D0 | 12 | Float 3D vector
Intersection indicator | 0x5DC | 4 | ?
| - | 0x5E0 | - | -
Track width | 0x5E4 | 4 | Float
| - | 0x5E8 | - | -
Pointer to 0x618 | 0x5F0 | 4 | Address
Pointer to 0x628 | 0x5F4 | 4 | Address
| - | 0x5F8 | - | -
Checkpoint number | 0x5FC | 4 | Integer
Checkpoint number at intersections | 0x600 | 4 | Integer
Checkpoint number at intersections | 0x604 | 4 | Integer
| - | 0x608 | - | -
Checkpoint number, sometimes behind | 0x618 | 4 | Integer
Checkpoint number at intersections | 0x61C | 4 | Integer
Checkpoint number at intersections | 0x620 | 4 | Integer
| - | 0x624 | - | -
Checkpoint fraction | 0x628 | 4 | Float
Checkpoint fraction at intersections | 0x62C | 4 | Float
Checkpoint fraction at intersections | 0x630 | 4 | Float
| - | 0x634 | - | -
Checkpoint, air only | 0x638 | 4 | Integer
| - | 0x63C | - | -
Checkpoint fraction | 0x648 | 4 | Float
| - | 0x64C | - | -
Track distance covered over all laps | 0x658 | 4 | Float
Track distance of one lap | 0x65C | 4 | Float | See [Course distances page](/miscellaneous/course_distances.md)
Track-distance position in this lap | 0x660 | 4 | Float
Orientation (yaw) relative to track | 0x664 | 2 | Integer
| - | 0x666 | - | -
Lateral position from checkpoint | 0x668 | 4 | Float
| - | 0x66C | - | -
Reverse status | 0x66F | 1 | Binary
| - | 0x670 | - | -
Out-of-reverse bit | 0x673 | 1 | Binary
Reverse indicator timer | 0x674 | 1 | Integer
| - | 0x675 | - | -
Lap number (latest) | 0x678 | 4 | Integer
Lap number (current position) | 0x67C | 4 | Integer
Checkpoint number, ground | 0x680 | 4 | Integer
Checkpoint number, ground, at intersections | 0x684 | 4 | Integer
Checkpoint number, ground, at intersections | 0x688 | 4 | Integer
| - | 0x68C | - | -
Checkpoint fraction | 0x690 | 4 | Float
Checkpoint fraction at intersections | 0x694 | 4 | Float
Checkpoint fraction at intersections | 0x698 | 4 | Float
| - | 0x69C | - | -
Checkpoint number, ground | 0x6A0 | 4 | Integer
Checkpoint fraction | 0x6A4 | 4 | Float
Position; only updates on ground | 0x6A8 | 12 | Float 3D vector
Lap number (latest), ground | 0x6B4 | 4 | Integer
Lap number (current position), ground | 0x6B8 | 4 | Integer
| - | 0x6BC | - | -
Time, current lap, frames | 0x6C0 | 4 | Integer
Time, current lap, fraction of frame | 0x6C4 | 4 | Float
Time, current lap, minutes | 0x6C8 | 1 | Integer
Time, current lap, seconds | 0x6C9 | 1 | Integer
Time, current lap, milliseconds | 0x6CA | 2 | Integer
Time, 1 lap ago, same format as above | 0x6CC | 12 | Time
Time, 2 laps ago | 0x6D8 | 12 | Time
Time, 3 laps ago | 0x6E4 | 12 | Time
Time, 4 laps ago | 0x6F0 | 12 | Time
Time, 5 laps ago | 0x6FC | 12 | Time
Time, 6 laps ago | 0x708 | 12 | Time
Time, 7 laps ago | 0x714 | 12 | Time
Time, 8 laps ago | 0x720 | 12 | Time
Time, best lap | 0x72C | 12 | Time
Time, sum of completed laps | 0x738 | 12 | Time
Time, total | 0x744 | 12 | Time
| - | 0x750 | - | -


## Notes

### Pointer associated with current track piece? (0x340, 0x3A4, 0x3A8, 0x3AC, 0x3B0, 0x3B4)

This changes when you drive from a straight piece of track to a turn, onto a piece of track where the track width starts to change, going out of a tunnel, and so on.

Mainly tested in SOSS. 0x3AC, 0x3B0, and 0x3B4 don't update in some parts of SOSS. 
