# 45x7-flipdot-controller
Custom PCB controller board for a single 45x7 flip dot panel from a Luminator MAX3000 SideSign

# How To

You will need the following items to assemble your

1. This PCB from [Osh Park](https://oshpark.com/shared_projects/JROcn5LK) or another fab.
2. [The Arduino example clock program](https://github.com/hshutan/FlipDotDisplay_Clock1_SWv1) which contains my Matrix CoProcessor library, a library specifically built to drive this PCB.
3. The surface mount silicon parts (see the Digi-Key BOM file in this project) as well as two through hole capacitors of your choosing. I am using 470 microfarads for the flip voltage, and 100 microfarads for the logic voltage.
4. A Luminator MAX3000 Side Sign. I purchased mine from [Rollsign Gallery](http://rollsigngallery.com/)
5. A microcontroller/Arduino, and various power supply components
 

# Notes
There are three voltages: Logic (5v), Flip (12-15v), LED (19v or 400mA max)

HW Rev1 of the PCB does not include any current limiting for the flip dots, or for the LEDs. I am using a 60mA current limter in-line with the flip dot voltage line. The dots seem to flip based on voltage and not current, which is why I am using such a small current. The LEDs are meant to be driven at 19 volts max.

My first prototype clock/sign with this PCB uses 15 volts for both the LEDs and flip dots. This means the LEDs are always on, although not near their maximum brightness. I am using a 5 volt Arduino Pro Mini, and also supplying 5 volts to the logic voltage input on the PCB.

Watch for ground loops, as I believe these cause weak/un-reliable flips. Because the grounds are all "commoned" on the PCB, do not tie any of your grounds together pre-PCB.
