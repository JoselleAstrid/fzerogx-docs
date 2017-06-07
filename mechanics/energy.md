# Energy

## Note on Energy versus Body

- Energy and Body are two different things. A machine's body determines how much energy they lose on collisions, land mines, etc. All machines (except certain ones in Story) start with the same energy, but different machines have different body ratings (e.g. Fat Shark has very strong body, Twin Noritta has very weak body).
- Body doesn't determine how much energy is lost from a boost. Having more energy both lets you take more hits, and lets you boost more.

## Energy amounts


| | Energy | Notes
--- | --- | ---
Full bar | 100 | Certain CPU racers in Story Mode have different amounts of energy
Slow red flashing | Less than 25 | CPUs with more starting energy still have the same red-flashing thresholds
Fast red flashing | Less than 15 |
Can't boost anymore | 1 or less |
Exhausted all energy by boosting | 0.01 |
Broken down | 0 |
Restore after breaking down | 50 |

## Energy gains and losses

| | Gain/Loss | Notes
--- | --- | ---
Boost | -0.1666... per frame | You'll go from full to empty energy in 600 frames (10 seconds) worth of boosts
Pit area | +1.111... per frame | You'll go from empty to full energy in 90 frames (1.5 seconds). If you're boosting as you go through the refiller, then the energy refill AND the boost's energy depletion happen at the same time, meaning your energy is refilled more slowly: at a rate of +0.9444... per frame.
Destroy another machine | +6.666... |
After end of race | +1.111... per frame | This is why it's rare to break down after crossing the line
Collision with another machine | -(Unknown base damage) * Body stat (* 1.95 if CPU) | Both machines receive the same base damage, regardless of weight or speed. The CPU multiplier means that if you and a CPU have the same Body, and you collide, the CPU still takes 1.95 times more damage than you. The base damage is probably calculated from the difference of the machines' velocity vectors, or something similar.
Spin attack from another machine | (Unknown formula) Capped at -20 for human players (tested in Vs. Battle and Story) | Doing a spin attack gives you some extra defense
Side attack from another machine | (Unknown formula) Capped at -20 for human players (tested in Vs. Battle and Story) | Chapter 4, Blue Falcon P1 vs. Wild Boar CPU: A fairly solid attack is around -180 to -240 at non-boosted speeds (he has 600 energy on Very Hard). Chapter 7, Blue Falcon P1 vs. Black Bull CPU at race start: A solid attack is about -75 without strafe, -105 if you strafe into the side attack (he has 180 energy). Don't know if there is a * 1.95 multiplier.
Wall hit | -0.01 * (speed in km/h) * (factor related to collision angle). Capped at -20 for human players | The collision angle relation is unknown, but it's close to 1.0 for a head-on collision, and close to 0.5 for 45 degrees. Very small damage amounts like 0.005 are possible, and it's possible to tap the wall so lightly that you don't lose any energy.
Mine hit | -20 * Body stat. Capped at -20 for human players | Human players with Body stat 1 or higher get -20. No * 1.95 multiplier for CPUs
Other obstacle hit | Some deal damage, some don't. [Example: FFU's pipes](https://www.youtube.com/watch?v=i9VdU-WbQTs) |
Drive over lava | -0.333... * Body stat, per frame | No * 1.95 multiplier for CPUs
Drive over a mine's remains | -0.333... * Body stat, per frame | No * 1.95 multiplier for CPUs
Drive through a laser (LHP) | -0.333... * Body stat, per frame | 2 frames of damage is typical at around 1000 km/h. No * 1.95 multiplier for CPUs
Drive against the underside of a track | -0.333... * Body stat, per frame |
Get stuck sideways on a rail | -0.333... * Body stat, per frame |
Chapter 2 boulder hit | These deal more damage than wall hits. -20 is possible at speeds as low as 550 km/h with Blue Falcon (Body 0.85). Capped at -20 for human players (not capped for CPU Fire Stingray) |
Chapter 5 capsule, Normal | +30 |
Chapter 5 capsule, Hard | +25 |
Chapter 5 capsule, Very Hard | +20 |
  

## Granularity of the energy bar display

- 4:3 aspect ratio: the energy bar has 128 visible chunks. This means you can visibly see your energy go down after each 0.78125 energy lost.
- 16:9 aspect ratio: the energy bar has only 96 visible chunks, despite appearing to be the same width. You can visibly see your energy go down after each 1.041777... energy lost.
- To determine how many energy chunks are visible, the game rounds your energy to the nearest multiple of 0.78125 for 4:3, or multiple of 1.041777... for 16:9. So for 4:3, your energy looks completely empty when less than 0.390625. For 16:9, it looks completely empty when less than 0.5208333....


## Memory location

Offset 0x184 in [Racer block 1](/addresses/racer_block_1.md).
