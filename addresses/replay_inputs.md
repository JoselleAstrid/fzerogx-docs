# Replay inputs


## Memory location and layout

There's one memory area which is active in the Time Attack, Grand Prix, and Replay modes. It contains replay inputs for the current race.

The main part of this memory area is an array of replay inputs. Each array element consists of 7 bytes, and specifies a set of inputs - steering values, strafe value, accelerator and boost input, and so on.

Before the array, there are two 2-byte numbers which are the current array index and the last array index.

In a live race, the array starts empty. When "3" on the countdown is reached, one array element is created. For the remainder of the race, when input changes, a new array element is created, and the current/last array indexes increment.

In a replay, the array is already filled with inputs as the replay starts. The only thing that is updated during the replay is the current array index, which increases according to the replay's progress.

Memory locations:

- Pointer = \[[Reference pointer](index.md#base-addresses-and-pointers) + 0x239058\]

  - Pointer is 0 if not in a race in Time Attack, Grand Prix, or Replay.
  
- Current array index (2 byte integer) = Start address + Pointer - 0x80000000 + 0xA0
  
- Last array index (2 byte integer) = Start address + Pointer - 0x80000000 + 0xA2
  
- Array start = Start address + Pointer - 0x80000000 + 0xA4

To find the array without going through the pointers, have at least one part of the race with Accel input only, and scan for the array of hex bytes `04 00 00 00 64`. Or, you can try checking the address 0x300F0DEA4 in Time Attack mode and Dolphin 5.0.


## Array element items

Item | Offset | Bytes/Bits | Format
--- | --- | --- | ---
Side attack button (1 if pressed, 0 otherwise) | 0x0, 1st bit | 1 bit | Binary
Boost button | 0x0, 2nd bit | 1 bit | Binary
Spin attack button | 0x0, 3rd bit | 1 bit | Binary
1 when both strafe inputs are non-zero | 0x0, 4th bit | 1 bit | Binary
- | 0x0, 5th bit | 4 bits | -
Steer X, range -100 to 100 | 0x1 | 1 | Signed integer
Steer Y, range -100 to 100 | 0x2 | 1 | Signed integer
Right strafe minus left strafe, range -100 to 100 | 0x3 | 1 | Signed integer
Accel, range 0 to 100 | 0x4 | 1 | Integer
Brake, range 0 to 100 | 0x5 | 1 | Integer
Number of frames on this set of inputs, minus 1 | 0x6 | 1 | Integer


## Notes

- Replays don't save the full strafe input information. It only saves right strafe minus left strafe, and whether both strafe values are non-zero. So as far as replays are concerned, these are the same:

  - L 1% / R 1%
  - L 50% / R 50%
  - L 100% / R 100%
  
  And these are the same:
  
  - L 1% / R 21%
  - L 50% / R 70%
  - L 80% / R 100%
  
  But these are different:
  
  - L 0% / R 20%
  - L 1% / R 21%
  
  We can probably also conclude that GX physics make no distinction between 1%/1% and 100%/100%, and so on.

- Steering and strafe values are post-calibration. Stick steering, for example, accounts for the range and deadzone you've specified in the [calibration settings](https://docs.google.com/document/d/1lhPvUVT9MO0J5U-bF9S9y3okGtPYD7UGvXNMCctJ3-4/edit?usp=sharing). Strafing with L and R only uses part of the range of L/R inputs: Pressing L/R a very small amount does not register anything, and you don't have to pass the highest-pressure point to get a full strafe.

- When Accel and Brake are assigned to simple buttons (as they usually are), the only possible values are 0 (not pressed) and 100 (pressed). If they are assigned to analog input such as the shoulder buttons, they can take on values from 1 to 99 as well.

- A saved replay file does not use the same format as the input array described here. It's possible that it contains a compressed version of the array, though.
