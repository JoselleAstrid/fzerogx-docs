# Handicap in Versus Battle mode

With handicap on in Vs. Battle mode, your machine stats are improved when you're not in first place.

- The more distance behind first place, the more your stats improve.
- Stat improvement starts as soon as you're behind first place, and stops when you're 3000m behind first place.
  - If you're going 1000 km/h, it takes 10.8 seconds to travel 3000m.
- If you're in first place, your stat values are normal (the stats you would normally have with the machine and setting you picked). So the handicap setting only improves stats; it doesn't worsen them. 
- CPUs don't experience handicap stat boosts. Even so, human players experience handicap stat boosts when a CPU is in first place. 

Here are the affected stats and their maximum improvements:

- Max speed: Up to 1.1 higher than normal
- Acceleration: Up to 0.3 higher than normal
- Boost strength: Up to 120% of the normal value
- Grip 1: Up to 130% of the normal value
- Body: Down to 30% of the normal value (lower value means a stronger body)

Stats change linearly with respect to distance behind. So if you're 1500m behind (half of 3000m), you'll experience half of the max stat improvement: +0.55 max speed, 110% boost strength, and so on.

Normally, some stats' formulas depend on the values of other stats; for example, the max speed formula changes dramatically if the acceleration value is low enough. However, handicap stat boosts cannot cause formulas to switch.

## Examples of max handicap effects

- Blue Falcon 100%
  - Acceleration 0.315 -> 0.615
  - Body 0.85 -> 0.255
  - Boost strength 8.379 -> 10.0548
  - Grip 1 0.52875 -> 0.687375
  - Max speed 0.172 -> 1.272
- Golden Fox 50%
  - Acceleration 0.6 -> 0.9
  - Body 1.1 -> 0.33
  - Boost strength 7.695 -> 9.234
  - Grip 1 0.6 -> 0.78
  - Max speed 0.13 -> 1.23
- Wild Boar 100%
  - Acceleration 0.252 -> 0.552
  - Body 0.78 -> 0.234
  - Boost strength 7.930125 -> 9.51615
  - Grip 1 0.5175 -> 0.67275
  - Max speed 0.4456 -> 1.5456
