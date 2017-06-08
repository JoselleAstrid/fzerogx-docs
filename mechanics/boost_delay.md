# Boost delay

When you use boost power or hit a dash plate, you enter boost state. After boost power, boost state lasts as long as your machine's [boost duration stat](https://docs.google.com/spreadsheets/d/133Xsq-KV3lpfk9SS4_L84WV-JuXHOR8_GlFZRnskkSU/edit#gid=17). After a dash plate, boost state lasts for half the boost duration stat. For example, Fat Shark is in boost state for 2 seconds after boost power, and for 1 second after a dash plate.

However, when boost state ends, you typically have a delay of several frames until you can use boost power again.

The number of boost delay frames depends on your speed when your boost state ends:

Speed on last frame of boost state (km/h) | Boost delay frames
--- | ---
x < 1260 | 0
1260 <= x < 1320 | 1
1320 <= x < 1380 | 2
1380 <= x < 1440 | 3
1440 <= x < 1500 | 4
1500 <= x < 1560 | 5
1560 <= x < 1620 | 6
1620 <= x < 1680 | 7
1680 <= x < 1740 | 8
1740 <= x < 1800 | 9
1800 <= x | 10

See detailed test results [here](tests/boost_delay.md) if you're interested.

If you press the boost button during these boost delay frames, you don't boost. You have to wait until the boost delay frames are over before using boost power again.

## Boost delay and MT boosting

Boost delay is the biggest reason why MT boosting is useful, especially at higher speeds.

Generally when you're doing consecutive boosts, you gain or maintain speed in boost state, and you drop speed rapidly when not in boost state.

Boost delay forces some frames of non-boost state, so you want to MT (release the accelerator) during those boost delay frames to minimize speed loss, then press accelerator + boost together once the boost delay is over. Using MT between consecutive boosts is known as MT boosting.

The table above shows that the timing of consecutive boosts changes as you gain speed, so you must adjust your boost and MT timing accordingly.

Boost delay and MT boosting apply to dash plates as well. However, dash plates give a small boost effect even after boost state ends, so MT may not help after dash plates at lower speeds. The phenomenon is known as residual effect on [this spreadsheet](https://docs.google.com/spreadsheets/d/1fWJuCwwAKniUjdT64H8s0akdmBRo9r5XlLrkuWOIY4I/edit#gid=0).

## CPUs

CPU racers do not experience boost delay. They can always chain boosts consecutively with no gaps in boost state, and they often do in practice.

## Possible additional delay from pressing boost too early

If you press the boost button at a time when you can't boost, your next opportunity to boost might get a small additional delay of up to 6 frames.

This generally isn't a big deal, because a GX controller position isn't suited to mashing boost once per 6 frames (0.1 of a second). However, for completeness, we'll describe how the additional delay works. First, we'll need to understand exactly how the boost delay frame timer works:

- The boost delay frame timer is 0 to start.
- If the timer is more than 0, the timer counts down by 1 per frame until it reaches 0 again.
- If you press the boost button and the timer is 0 or 1, the timer becomes 6 on the next frame, then it keeps counting down as normal.
- If you press the boost button and the timer is 2 or more, the timer stays at its current value on the next frame, then it keeps counting down as normal.
- When boost state ends, the boost delay frame timer is set to a value X depending on your km/h speed, as detailed above... unless X is lower than the timer's current value.

Here are some example scenarios where the boost button is pressed at different times:

Status when pressing the boost button | Does a boost happen? | Boost delay progression on next frames | Boost delay progression if you hadn't pressed boost | Frame difference
--- | --- | --- | --- | ---
0 boost delay frames left | Yes | 6, 5, 4, 3, 2, 1, 0 | - | -
1 boost delay frame left | No | 6, 5, 4, 3, 2, 1, 0 | 0 | 6
2 boost delay frames left | No | 2, 1, 0 | 1, 0 | 1
3 boost delay frames left | No | 3, 2, 1, 0 | 2, 1, 0 | 1
1 boost state frame left, 1000 km/h | No | 6, 5, 4, 3, 2, 1, 0 | 0 | 6
1 boost state frame left, 1500 km/h | No | 6, 5, 4, 3, 2, 1, 0 | 5, 4, 3, 2, 1, 0 | 1
1 boost state frame left, 1800 km/h | No | 10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0 | 10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0 | 0
4 boost state frames left, 1000 km/h | No | 6, 5, 4, 3, 2, 1, 0 | (0, 0, 0), 0 | 3
4 boost state frames left, 1500 km/h | No | 6, 5, 4, 5, 4, 3, 2, 1, 0 | (0, 0, 0), 5, 4, 3, 2, 1, 0 | 0
4 boost state frames left, 1800 km/h | No | 6, 5, 4, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0 | (0, 0, 0), 10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0 | 0

Also, you must be holding the accelerator on the boost-button frame in order for the boost to happen. Otherwise, you'll start a 6 frame countdown without actually boosting. This happens when you press the boost button 1 frame before pressing the accelerator, even if you hold both buttons down afterward.

## Memory location

[Racer block 1](/addresses/racer_block_1.md), offset 0x4C6.

See also: Boost frame countdown at offset 0x18A, Speed in km/h at offset 0x17C.
