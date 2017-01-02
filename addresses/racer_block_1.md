# Racer block 1


## Memory location and layout

There's one memory block for each race participant. The blocks are of size 0x620 and come one after the other.
 
Calculation for the first block's address:

- Pointer = \[[Reference pointer](index.md#base-addresses-and-pointers) + 0x227878\]

  - Pointer is 0 if a race is not active.
  
  - Pointer becomes available during the black screen before the camera pans around the track.
  
- First block's address = Start address + Pointer - 0x80000000

Block order in races with multiple machines:

- Story Mode, Grand Prix, Practice: Player machine = 1st block. CPU that starts in 1st = 2nd block. CPU that starts in 2nd = 3rd block, and so on. (TODO: Haven't checked for Story Mode Chapter 6.)

- VS Battle: Player 1 machine = 1st block. Player 2 machine = 2nd block, and so on. CPU machines seem to be in reverse order: in 2P with CPU on, the CPU starting in 2nd = 3rd block, and the CPU starting in 1st = 4th block.


## Block items

Item | Offset | Bytes | Format
--- | --- | --- | ---
General state | 0x0 | 4 | Binary
Race entrant ID | 0x4 | 2 | Integer
Machine ID | 0x6 | 2 | Integer
Weight | 0x8 | 4 | Float
Grip 1 stat | 0xC | 4 | Float
Turn tension stat | 0x10 | 4 | Float
Turn movement stat | 0x14 | 4 | Float
Strafe turn stat | 0x18 | 4 | Float
Strafe stat | 0x1C | 4 | Float
Turn reaction stat | 0x20 | 4 | Float
Grip 2 stat | 0x24 | 4 | Float
Grip 3 stat | 0x28 | 4 | Float
Drift accel stat | 0x2C | 4 | Float
Body stat | 0x30 | 4 | Float
Camera reorienting stat | 0x34 | 4 | Float
Camera repositioning stat | 0x38 | 4 | Float
Machine name | 0x3C | 64? | String
Position, center | 0x7C | 12 | Float 3D vector
Position, center, 1 frame behind | 0x88 | 12 | Float 3D vector
Velocity, world coordinates | 0x94 | 12 | Float 3D vector
Unknown; rapidly changing floats ranging in hundreds | 0xA0 | 12 | Float x3
(Derived) Weight * 3.25 | 0xAC | 4 | Float
(Derived) Weight * 2.8125 | 0xB0 | 4 | Float
(Derived) Weight * 3.25 | 0xB4 | 4 | Float
Velocity, machine coordinates | 0xB8 | 12 | Float 3D vector
Unknown, collision related | 0xC4 | 4 | Float
Unknown, speed related | 0xC8 | 4 | Float
Unknown, might be stability related | 0xCC | 4 | Float
- | 0xD0 | 4 | -
(Dupe) Velocity, machine coordinates, Z | 0xD4 | 4 | -
Max speed in km/h | 0xD8 | 4 | Float
Unknown, related to race start and restoring | 0xDC | 4 | Float?
- | 0xE0 | 12 | -
Machine orientation, world coordinates | 0xEC | 12 | Float 3D vector
- | 0xF8 | 4 | -
Up vector? | 0xFC | 12 | Float 3D vector
- | 0x108 | 4 | -
Machine orientation, current gravity coordinates | 0x10C | 12 | Float 3D vector
- | 0x118 | 4 | -
(Dupe) Machine orientation, world coordinates | 0x11C | 12 | Float 3D vector
- | 0x128 | 4 | -
(Dupe) Up vector? | 0x12C | 12 | Float 3D vector
- | 0x138 | 4 | -
(Dupe) Machine orientation, current gravity coordinates | 0x13C | 12 | Float 3D vector
- | 0x148 | 4 | -
(Dupe) Machine orientation, world coordinates | 0x14C | 12 | Float 3D vector
Position, center, vertically oscillating, X | 0x158 | 4 | Float
(Dupe) Up vector? | 0x15C | 12 | Float 3D vector
Position, center, vertically oscillating, Y | 0x168 | 4 | Float
(Dupe) Machine orientation, current gravity coordinates | 0x16C | 12 | Float 3D vector
Position, center, vertically oscillating, Z | 0x178 | 4 | Float
Speed in km/h | 0x17C | 4 | Float
Aerial tilt | 0x180 | 4 | Float
Energy | 0x184 | 4 | Float
- | 0x188 | 2 | -
Boost frame countdown, for energy boosts and dash plates | 0x18A | 1 | Integer
Boost frame countdown, for energy boosts only | 0x18B | 1 | Integer
Unknown, boost effect related? | 0x18C | 4 | Float
- | 0x190 | 4 | -
Frame counter from machine crash to restore | 0x194 | 4 | Integer
Unknown, stability and out-of-bounds plane related | 0x198 | 36 | Float x9?
Track orientation | 0x1BC | 12 | Float 3D vector
Unknown, related to ground contact or gravity | 0x1C8 | 4 | Float
Checkpoint number | 0x1CC | 4 | Integer
Fraction of distance to next checkpoint | 0x1D0 | 4 | Float
Position, bottom | 0x1D4 | 12 | Float 3D vector
(Dupe) Position, 1 frame behind | 0x1E0 | 12 | Float 3D vector
Strafing input, range +/- 32 | 0x1EC | 4 | Float
Strafing input, range +/- 1.6 | 0x1F0 | 4 | Float
Up/Down steering input, range +/- 1 | 0x1F4 | 4 | Float
Strafing input, range +/- 1 | 0x1F8 | 4 | Float
Left/Right steering input, range +/- 1 | 0x1FC | 4 | Float
Accelerator input | 0x200 | 4 | Float
Air brake input | 0x204 | 4 | Float
Unknown, always 200 | 0x208 | 4 | Float
(Dupe) Left/Right steering input, range +/- 1 | 0x20C | 4 | Float
Score, increases when you go fast or retire rivals | 0x210 | 2 | Integer
Spin attack kill indicator, 0 or 1 | 0x212 | 1 | Binary
Wall hit and out-of-bounds plane hit count, max 180 | 0x213 | 1 | Integer
Frame countdown during restore | 0x214 | 2 | Integer
Unknown, collision or knockback related | 0x216 | 1 | Integer
Number of boosts used | 0x217 | 1 | Integer
Terrain state | 0x218 | 1 | Binary
- | 0x219 | 3 | -
Split paths indicator | 0x21C | 4 | ?
Acceleration stat | 0x220 | 4 | Float
Base speed | 0x224 | 4 | Float
Unknown, boost effect related | 0x228 | 4 | Float
Max speed stat | 0x22C | 4 | Float
Boost strength stat | 0x230 | 4 | Float
Boost duration stat | 0x234 | 4 | Float
Turn decel stat | 0x238 | 4 | Float
Drag stat | 0x23C | 4 | Float
- | 0x240 | 7 | -
Grip and air state | 0x247 | 1 | Binary
- | 0x248 | 4 | -
Tilt stat, front right, width | 0x24C | 4 | Float
Tilt stat, front right, height | 0x250 | 4 | Float
Tilt stat, front right, length | 0x254 | 4 | Float
Position, front right corner | 0x258 | 12 | Float 3D vector
Position, front right corner (B) | 0x264 | 12 | Float 3D vector
Up vector of track? (A1) | 0x270 | 12 | Float 3D vector
Up vector of track? (A2) | 0x27C | 12 | Float 3D vector
Slope rate of change (A), relevant for jumps/SBs | 0x288 | 4 | Float
Unknown tilt related thing, always 1.7 (A) | 0x28C | 4 | Float
Unknown, machine orientation related? (A) | 0x290 | 16 | Float x4
- | 0x2A0 | 3 | -
(Dupe) Grip and air state | 0x2A3 | 1 | Binary
- | 0x2A4 | 4 | -
Tilt stat, front left, width | 0x2A8 | 4 | Float
Tilt stat, front left, height | 0x2AC | 4 | Float
Tilt stat, front left, length | 0x2B0 | 4 | Float
Position, front left corner | 0x2B4 | 12 | Float 3D vector
Position, front left corner (B) | 0x2C0 | 12 | Float 3D vector
Up vector of track? (B1) | 0x2CC | 12 | Float 3D vector
Up vector of track? (B2) | 0x2D8 | 12 | Float 3D vector
Slope rate of change (B), relevant for jumps/SBs | 0x2E4 | 4 | Float
Unknown tilt related thing, always 1.7 (B) | 0x2E8 | 4 | Float
Unknown, machine orientation related? (B) | 0x2EC | 16 | Float x4
- | 0x2FC | 3 | -
(Dupe) Grip and air state | 0x2FF | 1 | Binary
- | 0x300 | 4 | -
Tilt stat, back right, width | 0x304 | 4 | Float
Tilt stat, back right, height | 0x308 | 4 | Float
Tilt stat, back right, length | 0x30C | 4 | Float
Position, back right corner | 0x310 | 12 | Float 3D vector
Position, back right corner (B) | 0x31C | 12 | Float 3D vector
Up vector of track? (C1) | 0x328 | 12 | Float 3D vector
Up vector of track? (C2) | 0x334 | 12 | Float 3D vector
Slope rate of change (C), relevant for jumps/SBs | 0x340 | 4 | Float
Unknown tilt related thing, always 1.7 (C) | 0x344 | 4 | Float
Unknown, machine orientation related? (C) | 0x348 | 16 | Float x4
- | 0x358 | 8 | -
Tilt stat, back left, width | 0x360 | 4 | Float
Tilt stat, back left, height | 0x364 | 4 | Float
Tilt stat, back left, length | 0x368 | 4 | Float
Position, back left corner | 0x36C | 12 | Float 3D vector
Position, back left corner (B) | 0x378 | 12 | Float 3D vector
Up vector of track? (D1) | 0x384 | 12 | Float 3D vector
Up vector of track? (D2) | 0x390 | 12 | Float 3D vector
Slope rate of change (D), relevant for jumps/SBs | 0x39C | 4 | Float
Unknown tilt related thing, always 1.7 (D) | 0x3A0 | 4 | Float
Unknown, machine orientation related? (D) | 0x3A4 | 16 | Float x4
Wall collision stat, front right, width | 0x3B4 | 4 | Float
Wall collision stat, front right, height | 0x3B8 | 4 | Float
Wall collision stat, front right, length | 0x3BC | 4 | Float
Position, front right corner (C) | 0x3C0 | 12 | Float 3D vector
Position, front right corner (D) | 0x3CC | 12 | Float 3D vector
Unknown, collision related (A) | 0x3D8 | 12 | Float x3
Wall collision stat, front left, width | 0x3E4 | 4 | Float
Wall collision stat, front left, height | 0x3E8 | 4 | Float
Wall collision stat, front left, length | 0x3EC | 4 | Float
Position, front left corner (C) | 0x3F0 | 12 | Float 3D vector
Position, front left corner (D) | 0x3FC | 12 | Float 3D vector
Unknown, collision related (B) | 0x408 | 12 | Float x3
Wall collision stat, back right, width | 0x414 | 4 | Float
Wall collision stat, back right, height | 0x418 | 4 | Float
Wall collision stat, back right, length | 0x41C | 4 | Float
Position, back right corner (C) | 0x420 | 12 | Float 3D vector
Position, back right corner (D) | 0x42C | 12 | Float 3D vector
Unknown, collision related (C) | 0x438 | 12 | Float x3
Wall collision stat, back left, width | 0x444 | 4 | Float
Wall collision stat, back left, height | 0x448 | 4 | Float
Wall collision stat, back left, length | 0x44C | 4 | Float
Position, back left corner (C) | 0x450 | 12 | Float 3D vector
Position, back left corner (D) | 0x45C | 12 | Float 3D vector
Unknown, collision related (D) | 0x468 | 12 | Float x3
- | 0x474 | 2 | -
Unknown, responds to mashing A or a low speed dash plate | 0x476 | 1 | Binary
Unknown machine stat, base stat block equivalent is 0x48 | 0x477 | 1 | Integer
Unknown, speed related | 0x478 | 4 | Float
Frame count since start or restore | 0x47C | 4 | Integer
Side attack frame countdown | 0x480 | 1 | Integer
Frame count since start or restore (B) | 0x481 | 1 | Integer
Skull count | 0x482 | 1 | Integer
Air time frame count | 0x483 | 1 | Integer
- | 0x484 | 4 | -
Unknown, pointers? | 0x488 | 24 | Address x6
Position, behind and above | 0x4A0 | 12 | Float 3D vector
Energy lost on previous hit | 0x4AC | 4 | Float
Strafe effect | 0x4B0 | 2 | Signed integer
Dash plate hit count | 0x4B2 | 1 | Integer
Machine crash bit | 0x4B3 | 1 | Binary
Unknown, stability related? | 0x4B4 | 4 | Float?
- | 0x4B8 | 8 | -
Frame countdown since approaching another machine | 0x4C0 | 1 | Integer
Last other machine approached | 0x4C1 | 1 | Integer
Restore count | 0x4C2 | 1 | Integer
- | 0x4C3 | 1 | -
Frame countdown after collision with another machine | 0x4C4 | 2 | Integer
Boost delay frame timer | 0x4C6 | 2 | Integer
(Dupe) Position, center, 1 frame behind | 0x4C8 | 12 | Float 3D vector
Turn reaction input | 0x4D4 | 4 | Float
Turn reaction effect | 0x4D8 | 4 | Float
Boost energy usage factor | 0x4DC | 4 | Float
Unknown, setting to nonzero immobilizes you | 0x4E0 | 2 | Integer
- | 0x4E2 | 2 | -
Unknown, nonzero when 0x4E0 is activated | 0x4E4 | 24 | Float x6
- | 0x4FC | 1 | -
Terrain state 2 | 0x4FD | 1 | Binary
- | 0x4FE | 2 | -
Collision response | 0x500 | 12 | Float 3D vector
Split paths indicator 2 | 0x50C | 1 | Integer
Machine model detail | 0x50D | 1 | ?
- | 0x50E | 1 | -
Unknown, gets set to 0 on every frame | 0x50F | 1 | ?
Unknown, always 2 | 0x510 | 4 | Float?
Unknown, different before race + sometimes during restore | 0x514 | 4 | ?
Restore distance progress | 0x518 | 4 | Float
Unknown, restore related | 0x51C | 4 | Float
Restore coordinates | 0x520 | 96 | Float x24
Turning related | 0x580 | 4 | Float
Obstacle collision stat | 0x584 | 4 | Float
Track collision stat | 0x588 | 4 | Float
- | 0x58C | 3 | -
General state 2 | 0x58F | 1 | Binary
Restore completion flag | 0x590 | 1 | Binary
Frame counter from retiring another machine | 0x592 | 1 | Integer
Break down frame countdown | 0x593 | 1 | Integer
Restore coordinates 2 | 0x594 | 48 | Float x12
Unknown, could be relevant to stats | 0x5C4 | 20 | Float x5
Post-restore countdown | 0x5D8 | 1 | Integer
- | 0x5D9 | 1 | -
Max energy | 0x5DA | 2 | Integer
- | 0x5DC | 4 | -
Unknown, more coordinates | 0x5E0 | 48 | Float x12
Side attack indicator 1 | 0x610 | 4 | Float
Side attack indicator 2 | 0x614 | 1 | Signed byte
- | 0x615 | 7 | -
Ground/air flag | 0x61C | 1 | Binary?
- | 0x61D | 3 | -
