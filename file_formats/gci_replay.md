# Replay GCI file format

The first 0x20A0 bytes are covered in: [gci.md](gci.md)

This page describes everything from offset 0x20A0 to the end of the GCI file.

Every data field described on this page is read and written on a bit basis (not a byte basis). Additionally, the bits are reversed to go between the actual value and the GCI value (111001 becomes 100111).

The largest fields are the Replay Input Array (1 block roughly every 22-30 seconds, depending on how frequently controller inputs change) and the Emblem Array for custom machines (about 4 blocks, 1 for each emblem, regardless of how many emblems are actually applied). For reference, one block is 8192 (0x2000) bytes.

Much of this page's info is thanks to hosaka-corp, who reverse-engineered the replay decoding process using Dolphin's debugger, and replicated the process in the [fgx-re project on GitHub](https://github.com/hosaka-corp/fgx-re). The decoding process revealed the bit boundaries of each field (except the fields within Custom Machine Data), and the conditions for each field to be present.

See [this fork of fgx-re](https://github.com/yoshifan/fgx-re/tree/master/py) for a GUI program that shows the replay format, and allows editing some fields. This program may be subject to change or possibly move, but as of 2018/05/08, you can run it by installing Python 3.6+, installing PyQt5, and running `python gui.py`.


## Top-level Fields

Not all fields are present in every GCI. The 'Condition' column shows any conditions that need to be true for the field to be present.

Item | Number of bits | Format | Condition | Notes
--- | --- | --- | --- | ---
Lower byte from a timestamp | 8 | Integer |  | The timestamp is from a call to OsGetTick()
Racer Array type | 7 | Integer |  | Always 5?
Course ID | 6 | Integer |  | See [table of course IDs](/miscellaneous/ids.md#courses)
Unknown | 32
Unknown | 32 |  |  | First 2 bytes are frequently (but not always) CA E8
Racer Array element count | 5 | Integer |  | 1 in Time Attack replays, 30 in Grand Prix replays
Grand Prix difficulty | 3 | Choice |  | Novice 0, Standard 1, Expert 2, Master 3. Time Attack gets 1.
Game mode | 2 | Choice |  | Grand Prix 1, Time Attack 2
Unknown | 1 |  |  | Always 0?
Lap count | 7 | Integer |  | Always 3. When a machine completes this number of laps, the AI takes over the controls (regardless of whether the Replay Array is finished), and the Game Camera no longer follows behind that machine.
Racer Array | Varies |  |  | See [Racer Array section](#racer-array)
Unknown | 1 |  | Racer Array type >= 5
Unknown | 2
Total frames | 20 | Integer | Racer Array type >= 5 | Measures time from the start of accepting player input (start of the 3-2-1 countdown, when the player can rev up the engine) to the end of the race (crossing the finish line). The start is 182 frames before the race timer starts counting. When this number of frames elapses, the replay fades to white.
Replay Checkpoint Array element count | 8 | Integer | Always 4
Replay Checkpoint Array | 4*441 |  |  | See [Replay Checkpoint Array section](#replay-checkpoint-array)
Replay Input Array element count, minus 1 | 14 | Integer | If this field's value is 6, then the array length is actually 7
Replay Input Array | Varies |  |  | See [Replay Input Array section](#replay-input-array)
| Zeros | Until the end of a block: 0x6040, 0x8040, ...


## Racer Array

This array has 1 element for each participant in the race. So, 1 for Time Attack, 30 for Grand Prix.

Just to be clear on terminology:

- A **custom machine** is a machine that you register in the Garage, and load from a memory card.
- An **original machine** is a custom machine that you build using custom parts: one body, one cockpit, and one booster.
- A **pilot-exclusive machine** is a machine where you can't change the pilot. It can be either a non-custom machine, or a custom machine that you apply emblems to.

Contents of each element:

Item | Number of bits | Format | Condition | Notes
--- | --- | --- | --- | ---
Human flag | 1 | Choice |  | Human 1, CPU 0
Machine ID | 6 | Integer |  | See [table of machine IDs](/miscellaneous/ids.md#machines); 50 is used for original machines
AI related | 5 |  | Racer Array type >= 4 | Time Attack: always 0; Dolphin gets invalid read/write warnings if changed to non-0, and as a result the track may not load properly. GP: when these numbers are changed (either for human or CPUs), AI behavior changes, and the replay may desync because of different human-CPU interactions. Numbers 0 to 29 are distributed between the racers. In the first track of a cup they are, in racer block order: 1, 2, 3, 4, 5, ..., 29, 0. In subsequent tracks the numbers are scrambled.
Acceleration/max speed setting | 7 | Integer | Racer Array type >= 3 | Only applies to non-custom machines. 0 with the slider all the way left, 100 all the way right, +/- 1 for each D-Pad movement
Color swap | 2 | Choice | Human flag == 1 | Default color is 0. Press L on the machine settings screen to go 0 -> 1 -> 2 -> 3 -> 0.
Unknown | 7 |  | Human flag == 1 AND Racer Array type <= 1 | Doesn't seem to be used in any replays
Custom machine flag | 1 | Choice | Human flag == 1
Custom Machine Data | 8*33216 |  | Custom machine flag == 1 | See [Custom Machine Data section](#custom-machine-data)


## Custom Machine Data

This entire data region is read from the GCI 8 bits at a time, so the field boundaries aren't as clear. (The replay decoder probably just passes this data to another module, and isn't responsible for discerning these fields.)

Item | Number of bytes (Number of bits * 8) | Format | Notes
--- | --- | --- | ---
Unknown | 5 |  | Always C0 00 00 00 00 for original machines, and 80 00 00 00 00 for pilot-exclusive machines
Machine ID | 1 | Integer | Same value as Racer Array's Machine ID
Color swap related | 1 |  | Value is 1 or 2; changing this manually changes the color swap of the machine, at least for pilot-exclusive machines
Emblem count | 1 | Integer | Number of emblem slots used; 0 to 4
Unknown | 7 |  | Always 03 00 41 56 20 20 20 for original machines, and 01 00 41 56 20 20 20 for pilot-exclusive machines
Acceleration/max speed setting | 7 | Integer | Same as the Racer Array's setting, but this setting is the only one that affects custom machines
Unknown | 16 |  | Always 0?
Emblem Array | 4*8288 |  | See [Emblem Array section](#emblem-array)
Pilot ID | 4 | Integer | Each pilot gets the same ID as their pilot-exclusive machine, e.g. Captain Falcon and Blue Falcon both get 6. The actual ID is in the first byte, and the last 3 bytes seem to be unused. This value is present for both original and pilot-exclusive custom machines.
Body ID | 4 | Integer | See [table of custom parts](/miscellaneous/ids.md#custom-machine-parts). The actual ID is in the first byte, and the last 3 bytes seem to be unused. Pilot-exclusive machines get 0.
Body color | 4 | First 3 bytes are Red, Green, Blue. 4th byte is always 1. For original machines, color swapping in the Machine Settings screen IS taken into account. All 0s for pilot-exclusive machines.
Cockpit ID | 4 | Integer | Format is the same as Body ID
Cockpit color | 4 | Integer | Format is the same as Body color
Booster ID | 4 | Integer | Format is the same as Body ID
Booster color | 4 | Integer | Format is the same as Body color
Unknown | 4 |  | Always 0?


## Emblem Array

This array has 4 elements, 1 for each emblem slot, regardless of how many emblems are actually applied. The first element corresponds to the leftmost emblem slot, the second element corresponds to the slot right of that, and so on. For empty emblem slots, every value is zero except for the two Base position values.

Contents of each element:

Item | Number of bytes (Number of bits * 8) | Format | Notes
--- | --- | --- | ---
Custom part | 2 | Choice | Body 0, Cockpit 1, Booster 2
Unknown | 2
Unknown | 4 | Float
Rotation, vertical | 2 |  | Default and maximum 3FFF, minimum 0800
Rotation, horizontal | 2 |  | Default and minimum 0000, maximum probably FFFF. 45 degrees left ~= E06E, 90 degrees right ~= 400E, 180 degrees left or right ~= 807C
Unknown | 4
Base position 1? | 4 | Float | Seems to depend on the part you're applying to? Needs more testing.
Base position 2? | 4 | Float | Seems to depend on the part you're applying to? Needs more testing.
Unknown | 16
Position related | 4 | Float
Position related | 4 | Float
Unknown | 4 | Float | Always 5.0?
Position related | 4 | Float
Position related | 4 | Float
Unknown | 4
Size, horizontal | 4 | Float | Emblem menu's range is 0.35 (largest and default) to 0.05 (smallest). Only manual editing can adjust horizontal and vertical size separately (thus stretching the emblem), and get to more extreme values than normal (<0.05, >0.35).
Size, vertical | 4 | Float
Unknown | 24
Pixel data | 8192 |  | Same format as in an emblem GCI.



## Replay Checkpoint Array

There are three ways that the screen can fade to white during a replay:

- 'Total frames' is reached. If the replay is not tampered with, this should occur when crossing the finish line.
- The player presses Start and chooses to exit the replay.
- One of the Replay Checkpoints is reached, and the actual position doesn't match the checkpoint position exactly. This is probably meant as a failsafe to exit the replay early in case of a desync.

Here's how a Replay Checkpoint works: it saves the machine's position at a specific frame. When the replay is played back, and this specific frame is reached, it checks if the machine's position matches the saved position. If it doesn't match, the replay fades to white. If it does match, the replay continues. Each replay has 4 Replay Checkpoints.

This array has 4 elements, and for some reason each element actually saves 4 positions, but only the first position is checked. Thus, there are 4*1 = 4 checkpoint positions which are actually checked.

The first checkpoint is always at frame 182: at "Go!", when the race timer starts, but just before the machine moves out of the starting gate. Note that the checkpoint position corresponds to the center of the machine. So, even before getting out of the starting gate, the Y position (vertical) will vary depending on the machine's size.

Contents of each element:

Item | Number of bits | Format | Notes
--- | --- | --- | ---
Frame number 1 | 14 | Integer | Like 'Total frames', the beginning of the 3-2-1 countdown is 0, and the race timer starts at 182. The 1st array element always has 182 here. The 2nd-4th array elements seem randomly placed within the middle of the race. The max number here is 16383, so the latest it can be in a race is about 4'30. This number can be manually changed to something below 182, in which case the checkpoint will still work, but the fade to white will be delayed until frame 182.
Frame number 2 | 14 | Integer | Often same as Frame number 1, other times 1 to ~50 frames larger. Making this smaller than Frame number 1 seems to disable the entire checkpoint element (meaning it can never cause the replay to fade to white).
Unknown | 4 |  | These unknown fields vary more in GP replays
Unknown | 5
Unknown | 5
Unknown | 5
Unknown | 5
Unknown | 5
Position 1, X | 32 | Float | Corresponds to Frame number 1 + the player's machine. This is the only checkpoint position that can actually make the replay fade to white.
Position 1, Y | 32 | Float
Position 1, Z | 32 | Float
Position 2, X | 32 | Float | Corresponds to Frame number 2 + the player's machine
Position 2, Y | 32 | Float
Position 2, Z | 32 | Float
Position 3, X | 32 | Float | Corresponds to Frame number 1 + the player's machine in Time Attack, or the CPU at racer index 1 in Grand Prix
Position 3, Y | 32 | Float
Position 3, Z | 32 | Float
Position 4, X | 32 | Float | Corresponds to Frame number 2 + the player's machine in Time Attack, or the CPU at racer index 1 in Grand Prix
Position 4, Y | 32 | Float
Position 4, Z | 32 | Float


## Replay Input Array

This array has one element for every time input changes, including stick and L/R pressure changes. A typical race may have roughly 1 element per 1.5 frames. The maximum possible is 1 element per frame.

Contents of each element:

Item | Number of bits | Notes
--- | --- | ---
Buttons | 8 | 0x04 with nothing, 0x14 with L+R, 0x44 with boost, 0x84 with side attack
Strafe | 8
Accel | 7
Brake | 7
Frame count on this set of inputs, minus 1 | 8
Steer X | 8
Steer Y | 8

Related: [Replay inputs in RAM](/addresses/replay_inputs.md)
