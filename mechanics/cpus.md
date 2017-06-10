# Machine stats, rubberbanding, and other attributes of CPU racers


## Attributes of all CPUs

- CPU racers always use 50% settings (not leaning towards acceleration or max speed).
- CPU racers' steering and strafe controls don't have the same limits as human players do. CPUs can steer 1.35 times harder, and strafe 1.35 times harder.
  - This is why CPUs can typically survive a jump at the last turn of Phantom Road: Slim-Line Slits.
- CPU racers never experience [boost delay](/mechanics/boost_delay.md), so they can always boost again as soon as the previous boost has ended, unlike human players.


## About CPU rubberbanding

[Accelerator input is analog in GX](https://youtu.be/cEtneG44I_I). The minimum and maximum values for human players are 0.0 and 1.0. If the accelerator is mapped to a button, then pressing the button gives you 1.0, and not pressing it gives you 0.0. If the accelerator is mapped to a stick or analog trigger, then values between 0 and 1 can be used.

CPUs rubberband mainly by varying their amount of accelerator input. And they can go as high as 1.3, allowing them to go faster than human players can.

In the following sections, the accelerator input numbers generally aren't completely constant. CPUs may briefly vary them while dealing with hazards on the track, attempting a spin attack, and so on.


## Grand Prix and Practice modes

CPUs in these modes change their accelerator input gradually depending on how far ahead or behind they are compared to the human player. The cap for being ahead/behind is not that large, roughly a 1.5 second gap without boosting.

Difficulty | Lowest accel input when ahead of the player | Accel input when about even with the player | Highest accel input when behind the player
--- | --- | --- | ---
Novice | 0.45 | 0.85 | 0.98
Standard | 0.5 | 0.9 | 1.0
Expert | 0.6 | 0.94 | 1.02
Master | 0.7 | 0.96 | 1.03

Again, it adjusts gradually based on the exact distance ahead/behind. If the Master CPUs are only slightly behind, they use an accelerator input value somewhere between 0.96 and 1.03, such as 1.01.

The biggest difference between difficulties is how much the CPU uses boosts and spin attacks, but this has not been quantified.


## Vs. Battle

Accelerator input: Like Standard, but doesn't go above 0.9 (only tested with one human player passing the CPU). The handicap setting does not affect this.


## Story mode

Normal energy is 100. For CPUs with an amount of energy besides 100, that is their starting amount and also their cap (the highest amount they can get from pit areas). The thresholds for flashing red are still the same: 25 for slow flashing, 15 for fast flashing. Those thresholds are not percentages.

### Chapter 2 Fire Stingray

- Energy: 10000
  - Can fall off the cliff
- Acceleration stat: Normally 0.3 -> now 0.8
- Max speed stat: 0.15 -> 0.65

Accelerator input: Goes through three phases during the race. Accel input is constant during phase 1, slower when ahead of the player during phase 2, and as fast as possible during phase 3. Normal does not have a phase 3. The higher the difficulty, the longer phases 1 and 3 are.

Difficulty | Phase 1 accel input | Phase 2 start point | Phase 2 accel input | Phase 3 start point | Phase 3 accel input
--- | --- | --- | --- | --- | ---
Normal | 0.8 | ~8866m, start of second left curve | 0.5 if ahead of the player, 1.0 if behind the player | - | -
Hard | 0.85 | ~9920m, end of second left curve | 0.5 if ahead of the player, 1.0 if behind the player | ~19890m, last small right bend | 1.3
Very Hard | 0.9 | ~11005m, mid-straightaway after the second left curve | 0.5 if ahead of the player, 1.0 if behind the player | ~19340m, end of last left curve | 1.3

Boosting: In phase 1, boosts once or twice if you pass him. In phase 2, boosts constantly if you're ahead. In phase 3, doesn't boost.

Fire Stingray can actually be more troublesome on Normal. First, boulders slow him down significantly, but there are fewer boulders on Normal. Second, he doesn't have a non-boosting end phase on Normal; you generally have to time your boosts properly at the finish so he doesn't get enough time to boost back ahead.

### Chapter 3 CPUs

Accelerator input: Gradual changes depending on amount ahead of the player; similar to Grand Prix mode, except there is no gradual change when behind the player. Also, the CPUs alternate between two "modes" depending on which part of the track they're at.

Difficulty and mode | Lowest accel input when ahead of the player | Accel input when even with or behind the player
--- | --- | ---
Normal, mode 1 | 0.6 | 1.224
Normal, mode 2 | 0.75 | 1.3
Hard, mode 1 | 0.78 | 1.26
Hard, mode 2 | 1.1375 | 1.3
Very Hard, mode 1 | 0.9 | 1.296
Very Hard, mode 2 | 1.3 | 1.3

The track has 59 checkpoints. Here's where each mode is used:

Checkpoint ranges | 0-21 | 22-34 | 35 | 36-51 | 52-56 | 57-58
--- | --- | --- | --- | --- | --- | ---
Lap 1 | 2 | 1 | 2 | 1 | 1 | 2
Laps 2 and 3 | 2 | 1 | 2 | Random? | 1 | 2

The checkpoint-range boundary locations may be one checkpoint off. They may also vary slightly by difficulty; for example, the 56/57 boundary seems to be at 56 for Very Hard, roughly 56.5 for Hard, and 57 for Normal.

The main takeaway here is that the CPU difficulty progression is fairly large when they're ahead, but fairly small when they're behind.

Mad Wolf tends to be the fastest CPU, but he is also prone to retiring, particularly in Very Hard.

### Chapter 4 CPUs
  
Michael Chain:

- From start
  - Energy: 10000. Also gets reset to 10000 near the end of the pit area
  - Accelerator input:
    - 0.6 when you're far behind
    - 0.8 when you're not far behind, or ahead
    - 1.3 when you're in boost state
  - Boosts constantly when you're ahead or not far behind
- When he is 5000m distance from the goal, or all minions retired
  - Energy: Normal 300, Hard 450, Very Hard 600
  - Accelerator input:
    - 0.8 with brake tapping when you're behind, aiming to go about 800 km/h (regardless of your speed)
    - 1.3 when you're ahead or only about two car lengths behind

Minions:

- Energy: Normal 80, Hard 100, Very Hard 120
- The minions start by staying in formation with Michael Chain. They gradually break from the formation to go into attack mode when Michael Chain reaches certain distances. Here are the distances:
  - Machines 28-30: Immediately
  - 24-27: At about 3470m
  - 20-23: At about 5610m
  - 16-19: At about 7750m
  - 14-15: At about 9930m
  - 10-13: At about 12060m
  - 8-9: At about 15660m
  - 6-7: At about 18960m (shortly after the pit area)
  - 3-5: At about 20050m
  - This list of distances probably has a 50m margin of error, but it should give a general idea.
- Formation minions
  - Constantly adjusting accelerator input to remain in formation with Michael Chain
  - Use 1.3 accelerator input and boosting as needed to try and keep up when Chain boosts
- Attack minions
  - When you're behind, alternate between 0.8 and 0.0 accelerator input to try and be about 50 km/h slower than you. Down to a minimum of 600 km/h, and up to a maximum of using 0.8 input all the time
  - When you're ahead or about two car lengths behind, 1.3 accelerator input
  - No boosting
    
### Chapter 6 CPUs

The memory structure for racers only accommodates 30 machines, but there are two points during the race where the CPUs teleport ahead, so you end up encountering most CPUs two or three times.

There are two types of CPU machines. The bulky machines that move to the side have a machine ID of 0 (same as Red Gazelle). The smaller machines that look like racing machines have a machine ID of 1 (same as White Cat).

CPU list, Normal:

Machine type | Machine array positions | Notes
--- | --- | ---
ID 0, stationary | 2
ID 0, moving | 3, 4, 5, 6
ID 1, stationary | 7, 9, 18, 21
ID 0, moving | 12, 13, 14, 15, 16, 17
ID 0, moving | 24, 25, 26
ID 1, moving | 8, 10, 11, 19, 20, 22, 23, 27, 28, 29, 30 | When the player has about 24384m remaining, the CPUs will teleport ahead
ID 0, moving | 2, 3, 4, 5, 6
ID 0, moving | 12, 13, 14, 15, 16, 17
ID 0, moving | 24, 25, 26 | When the player has about 11284m remaining, the CPUs will teleport ahead
ID 0, moving | 24, 25, 26
ID 0, moving | 12, 13, 14, 15, 16, 17
ID 0, moving | 2, 3, 4, 5, 6
    
CPU list, Hard and Very Hard:

Machine type | Machine array positions | Notes
--- | --- | ---
ID 0, stationary | 2
ID 0, moving | 3, 4, 5, 6
ID 0, moving | 12, 13, 14, 15, 16, 17
ID 0, moving | 24, 25, 26
ID 1, moving | 7, 8, 9, 10, 11, 18, 19, 20, 21, 22, 23, 27, 28, 29, 30 | When the player has about 24384m remaining, the CPUs will teleport ahead
ID 0, moving | 2, 3, 4, 5, 6
ID 0, moving | 12, 13, 14, 15, 16, 17
ID 0, moving | 24, 25, 26
ID 1, moving | 7, 8, 9, 10, 11
ID 1, moving | 18, 19, 20, 21, 22, 23 | When the player has about 11284m remaining, the CPUs will teleport ahead
ID 1, moving | 27, 28, 29, 30
ID 0, moving | 24, 25, 26
ID 0, moving | 12, 13, 14, 15, 16, 17
ID 0, moving | 2, 3, 4, 5, 6
  
Energy:

- From start: 100
- After a teleport: 10000
    
Machine stats:

- ID 0 machines are like Red Gazelle, except:
  - Weight: 1330 -> 2000
  - Acceleration: 0.5 -> 0.4
  - Max speed: 0.198 -> 0.01
  - Turn movement: 175 -> 180
  - Drag: 0.01 -> 0.03
  - The collision properties are the same as Red Gazelle, despite the different machine model.
- ID 1 machines are like White Cat, except:
  - Weight: 1150 -> 2000
  - Acceleration: 0.45 -> 0.4
  - Max speed: 0.14 -> 0.01
  - Turn movement: 130 -> 180
  - Drag: 0.01 -> 0.03
  - The collision properties are the same as White Cat, despite the different machine model.

Accelerator input:

- ID 0, stationary machines have 0.0 accelerator input.
- ID 0, moving machines have 1.0 accelerator input when you're close, 0.5 when you're far away.
- ID 1, moving machines:
  - Normal: 0.95 accelerator input at first, then gradually go up to 1.02 after you pass them.
  - Hard: 1.0 accelerator input at first, then gradually go up to 1.05 after you pass them.
  - Very Hard: 1.02 accelerator input at first, then gradually go up to 1.08 after you pass them.

### Chapter 7 CPUs

Black Bull and Blood Hawk:

- Energy: Black Bull 180, Blood Hawk 150
- Stat changes
  - Laps 1-3 on any difficulty, when not ranked top 2: Acceleration stat +0.2, max speed stat +0.2
  - Lap 4 on Hard or Very Hard: Acceleration stat -0.1, max speed stat -0.1
    - If they are not top 2 at the end of Lap 3, then they will be stuck with +0.1 throughout Lap 4 instead!
  - Lap 5 on Very Hard: Regular stats are used
- Attack very aggressively during Lap 4 on both Hard and Very Hard
- Accelerator input: Gradual changes depending on amount ahead/behind compared to the player, like Grand Prix mode. During Laps 1-3, Black Bull and Blood Hawk switch between modes depending on whether they're ranked in the top 2 at that moment. The non-top-2 mode is actually slower in terms of accel input, though the non-top-2 stat changes counteract that.

Difficulty and situation | Lowest accel input when ahead of the player | Accel input when about even with the player | Highest accel input when behind the player
--- | --- | --- | ---
Normal, not top 2 | 0.515 | 0.9785 | 1.0506
Normal, top 2 | 0.51 | 1.01745 | 1.09242
Hard Laps 1-3, not top 2 | 0.6825 | 1.05 | 1.1025
Hard Laps 1-3, top 2 | 0.676 | 1.092 | 1.1466
Hard Lap 4 | 0.7475 | 1.15 | 1.2075
Very Hard Laps 1-3, not top 2 | 0.8025 | 1.0914 | 1.1556
Very Hard Laps 1-3, top 2 | 0.795 | 1.13526 | 1.20204
Very Hard Lap 4 | 0.9 | 1.224 | 1.296
Very Hard Lap 5 | Same as Laps 1-3, not top 2 | Same as Laps 1-3, not top 2 | Same as Laps 1-3, not top 2

Other 27 racers:

- Accelerator input: Gradual changes depending on amount ahead/behind compared to the player, like Grand Prix mode.

Difficulty | Lowest accel input when ahead of the player | Accel input when about even with the player | Highest accel input when behind the player
--- | --- | --- | ---
Normal | 0.5 | 0.95 | 1.02
Hard | 0.663 | 1.02 | 1.071
Very Hard | 0.78 | 1.10608 | 1.1232
  
### Chapter 8 Dark Schneider

- Energy: 500
  - Gets restored Practice-mode style if retired
- Grip 1 stat: 1.1 -> 1.3
- Uses side attacks as well as spin attacks
- Never uses boost power

Accelerator input: Gradual changes depending on amount ahead of the player, like Chapter 3. Also, alternates between up to three "modes" depending on which part of the track he's at.

Difficulty and mode | Lowest accel input when ahead of the player | Accel input when even with or behind the player
--- | --- | ---
Normal, mode 1 | 0.4 | 0.816
Normal, mode 2 | 0.75 | 1.3
Normal, mode 3 | 1.0 | 1.3
Hard, mode 1 | 0.52 | 0.84
Hard, mode 2 | 0.975 | 1.3
Hard, mode 3 | 1.3 | 1.3
Very Hard, mode 1 | - | -
Very Hard, mode 2 | 1.125 | 1.3
Very Hard, mode 3 | 1.3 | 1.3

The track has 283 checkpoints. Here's where each mode is used. Basically, he's somewhat slower in the middle laps of Normal and Hard (whether you're ahead or behind), but in Very Hard he remains fairly fast throughout the race:

Checkpoint ranges | 0-59 | 60-79 | 80-159 | 160-189 | 190-239 | 240-259 | 260-282
--- | --- | --- | --- | --- | --- | --- | ---
Normal Laps 1 and 3, Hard Laps 1 and 4, Very Hard Laps 1 and 5 | 3 | 3 | 2 | 3 | 2 | 3 | 2
Normal Lap 2 | 3 | 1 | 2 | 1 | 2 | 1 | 2
Hard Laps 2 and 3 | 3 | 1 | 2 | 1 | 3 | 1 | 3
Very Hard Laps 2, 3, and 4 | 3 | 2 | 3 | 2 | 3 | 2 | 2

Dark Schneider's high max speed and high accel input make it difficult to keep up in Lap 1. However, since he doesn't boost and there are a lot of pit areas, you can make up a lot of ground in the boost laps.


## Some unexplored aspects of CPU racers

- How does the CPU determine where to boost?
- How does the CPU determine what racing line to take?
- What are the internal values defining how aggressively a CPU attacks?
