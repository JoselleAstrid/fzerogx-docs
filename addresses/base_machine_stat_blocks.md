# Base machine stat blocks


## Memory locations and layout


### Primary location

There's one memory block for each non-custom machine and custom part. The blocks are of size 0xB4 and come one after the other.
 
First block's address = Start address + 0x1554000

Block order:

- Machine numbers 01 (Red Gazelle) to 30 (Black Bull)
- Dark Schneider
- Machine numbers 31 (Fat Shark) to 40 (Rainbow Phoenix)
- All 25 body parts in Garage order, Brave Eagle to Liberty Manta
- All 25 cockpit parts in Garage order, Wonder Worm to Energy Crest
- All 25 booster parts in Garage order, Euros -01 to Triple -Z

When you change these base stat values, the corresponding derived stat values in [Racer block 1](racer_block_1.md) also change.

Reference points: Custom parts start at Start address + 0x1555F04. After the custom parts are strings like AC-D1, GC-E1, AC-B1, etc.


### Secondary location for non-custom machines
 
First block's address = [Reference pointer](index.md#base-addresses-and-pointers) + 0x195584

Block order: Same as the primary location.

When you change these base stat values, the corresponding derived stat values do not change.

Reference point: Machine names as strings are located just before this.


### Secondary location for custom parts

First block's address = [Reference pointer](index.md#base-addresses-and-pointers) + 0x1B3A54

Block order: Same as the primary location, except that there are 24 bytes of other stuff between the body and cockpit blocks, and 16 bytes of other stuff between the cockpit and booster blocks.

When you change these base stat values, the corresponding derived stat values do not change.

Reference point: Strings such as AC-D1, GC-E1, AC-B1, etc. are just before this.


## Block items

Item | Offset | Bytes | Format
--- | --- | --- | ---
Machine name pointer | 0x0 | 4 | Address
Weight | 0x4 | 4 | Float
Acceleration | 0x8 | 4 | Float
Max speed | 0xC | 4 | Float
Grip 1 | 0x10 | 4 | Float
Grip 3 | 0x14 | 4 | Float
Turn tension | 0x18 | 4 | Float
Drift accel | 0x1C | 4 | Float
Turn movement | 0x20 | 4 | Float
Slide turn | 0x24 | 4 | Float
Strafe | 0x28 | 4 | Float
Turn reaction | 0x2C | 4 | Float
Grip 2 | 0x30 | 4 | Float
Boost strength | 0x34 | 4 | Float
Boost duration | 0x38 | 4 | Float
Turning deceleration | 0x3C | 4 | Float
Drag | 0x40 | 4 | Float
Body | 0x44 | 4 | Float
Unknown, possibly grip related stat | 0x48 | 1 | Integer
Unknown stat + Drift camera | 0x49 | 1 | Binary
- | 0x4A | 2 | -
Camera reorienting | 0x4C | 4 | Float
Camera repositioning | 0x50 | 4 | Float
Tilt, front right, width | 0x54 | 4 | Float
Tilt, front right, height | 0x58 | 4 | Float
Tilt, front right, length | 0x5C | 4 | Float
Tilt, front left, width | 0x60 | 4 | Float
Tilt, front left, height | 0x64 | 4 | Float
Tilt, front left, length | 0x68 | 4 | Float
Tilt, back right, width | 0x6C | 4 | Float
Tilt, back right, height | 0x70 | 4 | Float
Tilt, back right, length | 0x74 | 4 | Float
Tilt, back left, width | 0x78 | 4 | Float
Tilt, back left, height | 0x7C | 4 | Float
Tilt, back left, length | 0x80 | 4 | Float
Wall collision, front right, width | 0x84 | 4 | Float
Wall collision, front right, height | 0x88 | 4 | Float
Wall collision, front right, length | 0x8C | 4 | Float
Wall collision, front left, width | 0x90 | 4 | Float
Wall collision, front left, height | 0x94 | 4 | Float
Wall collision, front left, length | 0x98 | 4 | Float
Wall collision, back right, width | 0x9C | 4 | Float
Wall collision, back right, height | 0xA0 | 4 | Float
Wall collision, back right, length | 0xA4 | 4 | Float
Wall collision, back left, width | 0xA8 | 4 | Float
Wall collision, back left, height | 0xAC | 4 | Float
Wall collision, back left, length | 0xB0 | 4 | Float
