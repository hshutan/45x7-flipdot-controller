# 45x7-flipdot-controller
Custom PCB controller board for a single 45x7 flip dot panel from a Luminator MAX3000 SideSign

![PCBFront](https://644db4de3505c40a0444-327723bce298e3ff5813fb42baeefbaa.ssl.cf1.rackcdn.com/efcd5a3d5b252e8c72fecd9c762bc942.png) ![PCBBack](https://644db4de3505c40a0444-327723bce298e3ff5813fb42baeefbaa.ssl.cf1.rackcdn.com/0564cc1702dee4a132bf6b567288d8c7.png)

# How To

You will need the following items to assemble a flip dot sign using my PCB

1. The Eagle PCB in this github project, which can be ordered from [Osh Park](https://oshpark.com/shared_projects/JROcn5LK) or another fab.
2. [The Arduino example clock program](https://github.com/hshutan/FlipDotDisplay_Clock1_SWv1) which contains my "Matrix_CoProcessor" library, a library specifically built to drive this PCB.
3. Surface mount silicon parts (see the Digi-Key BOM file, also in this github project) as well as two through hole capacitors of your choosing. I am using 330 microfarads for the flip voltage, and 100 microfarads for the logic voltage.
4. A Luminator MAX3000 Side Sign. I purchased mine from [Rollsign Gallery](http://rollsigngallery.com/). A single Luminator MAX3000 side sign will have two 45x7 display panels inside, which are very easy to remove.
5. A microcontroller or Arduino, and various power supply components to provide the different needed voltages.
 

# Notes
The silkscreen for the 64 pin connector is for aesthetics. You should install the connector on the back of the board, and use the silkscreen for orientation reference.

There are three voltages: Logic (5v), Flip (12-15v), LED (19v or 400mA max)

HW Rev1 of the PCB does not include any current limiting for the flip dots, or for the LEDs. I am using a 60mA current limter in-line with the flip dot voltage line. The dots seem to flip based on voltage and not current, which is why I am using such a small current. The LEDs are meant to be driven at 19 volts max.

My first prototype clock/sign with this PCB uses 15 volts for both the LEDs and flip dots. This means the LEDs are always on, although not near their maximum brightness. I am using a 5 volt Arduino Pro Mini, and also supplying 5 volts to the logic voltage input on the PCB.

Watch for ground loops, as I believe these cause weak/un-reliable flips. Because the grounds are all "commoned" on the PCB, do not tie any of your grounds together pre-PCB.

Luminator and MAX3000 are trade names of the Luminator Technology Group, not mine.

# Thanks
I would like to thank the following sources for helping with my project:
- [Dottie the Flip Dot Clock](http://dhenshaw.com/Art/Dottie/start.html)
- [Rollsign Gallery](http://rollsigngallery.com/)
