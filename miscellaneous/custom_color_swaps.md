# Custom machine color swaps in Machine Settings

Here's how your custom machine colors change when you press L or R in Machine Settings.

Red (R), green (G), and blue (B) values range from 0 to 255. If a formula makes a color value go to 256 or higher, then subtract 256 to get the final value.

- Color 1 (what you choose in the garage) = R, G, B
- Color 2 (press R from color 1) = R+32, G+128, B+192
- Color 3 (press R from color 2) = R+192, G+128, B+32
- Color 4 (press R from color 3) = R+128, G+32, B+192
 
The point of knowing this is so you can use a different pilot color swap, along with the machine colors you want.
