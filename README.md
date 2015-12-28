# 45x7-flipdot-controller
Custom PCB controller board for a single 45x7 flip dot panel from a Luminator MAX3000 SideSign

![PCBFront](https://644db4de3505c40a0444-327723bce298e3ff5813fb42baeefbaa.ssl.cf1.rackcdn.com/efcd5a3d5b252e8c72fecd9c762bc942.png) ![PCBBack](https://644db4de3505c40a0444-327723bce298e3ff5813fb42baeefbaa.ssl.cf1.rackcdn.com/0564cc1702dee4a132bf6b567288d8c7.png)

# How To

**A much more [detailed How To](#detailed) is below**

You will need the following items to assemble a flip dot sign using my PCB

1. The Eagle PCB in this github project, which can be ordered from [OSH Park](https://oshpark.com/shared_projects/JROcn5LK) or another fab.
2. [The Arduino example clock program](https://github.com/hshutan/FlipDotDisplay_Clock1_SWv1) which contains my `Matrix_CoProcessor` library, a library specifically built to drive this PCB.
3. Surface mount silicon parts (see the Digi-Key BOM file, also in this github project) as well as two through hole capacitors of your choosing. I am using 330 microfarads for the flip voltage, and 100 microfarads for the logic voltage.
4. A Luminator MAX3000 Side Sign. I purchased mine from [Rollsign Gallery](http://rollsigngallery.com/). A single Luminator MAX3000 side sign will have two 45x7 display panels inside, which are very easy to remove.
5. A microcontroller or Arduino, and various power supply components to provide the different needed voltages.
 

# Notes
The silkscreen for the 64 pin connector is for aesthetics. You should install the connector on the back of the board not the front, using the silkscreen for orientation reference only.

There are three voltages: Logic (5v), Flip (12-15v), LED (19v or 400mA max)

HW Rev1 of the PCB does not include any current limiting for the flip dots, or for the LEDs. I am using a 60mA current limiter in-line with the flip dot voltage line. The dots seem to flip best based on voltage and not current, which is why I am using such a small current. The LEDs are meant to be driven at 19 volts max, however less is safer. A current limit of 350mA would be safe for the LEDs.

My first prototype clock/sign with this PCB uses 15 volts for both the LEDs and flip dots. This means the LEDs are always on, although not near their maximum brightness. I am using a 5 volt Arduino Pro Mini, and also supplying 5 volts to the logic voltage input on the PCB.

Watch for ground loops, as I believe these cause weak/un-reliable flips. Because the grounds are all "commoned" on the PCB, do not tie any of your grounds together pre-PCB.

Luminator and MAX3000 are trade names of the Luminator Technology Group, not mine.

<a name="detailed"></a>
# Detailed How To / Step by Step Instructions
1. Acquire a Luminator MAX3000 Side Sign. I found mine on [Rollsign Gallery](http://rollsigngallery.com/).
  - A single Luminator side sign will contain two 45x7 panels.
2. Order the PCB in this github project, it can be ordered with a few clicks from [Osh Park](https://oshpark.com/shared_projects/JROcn5LK)
3. Order the bill of materials ([see CSV file](https://github.com/hshutan/45x7-flipdot-controller/blob/master/FlipDotBOM.csv))
  - Also grab two spare through hole capacitors from your parts bin. Try a 50 volt 330 microfarad for the flip voltage, and a 16 volt 100 microfarad capacitor for the logic voltage.
4. Take apart the MAX3000 side sign and remove both of the 45x7 panels.
5. Assemble the PCB by placing all components and soldering. Hot air can be used for all the surface mount components.
  - For aesthetics, the PCB has very little silk screen. Here is how to place components: Pin 1 of each IC is in the lower left of the land pattern when viewing the board from the top (see PCB pictures at the top of this page).
  - The 0805 (2012 Metric) pads in the lower right area of the PCB are for the pull-up and pull-down resistors.
  - The 0805 (2012 Metric) pads in the upper left of the PCB are for the 0.1 microfarad shift register supporting capacitors.
6. Program an Arduino or microcontroller with the [test pattern](https://github.com/hshutan/FlipDotDisplay_TestPatterns_SWv1) software. A good test pattern to start with is `testPattern2()`
7. Hook up the Arduino per the comments in the code:
  - Arduino Uno pin 11, to SER on PCB
  - Arduino Uno pin 13, to SCK on PCB
  - Arduino Uno pin 10, to RCK on PCB
  - Arduino 5v, to 5v+ on PCB
8. Connect a power supply (start with 10-12 volts) to GND and Flip+ on the PCB.
  - For prototyping, use a constant voltage/constant current power supply. This will allow you to limit the current to 100mA (or less) for safety, and also to test flip reliability at different voltages. If you are using my `Matrix_CoProcessor` library that comes with the [test pattern](https://github.com/hshutan/FlipDotDisplay_TestPatterns_SWv1) software, then there is little risk of a flip dot being energized for more than a few hundred microseconds, however you should still use current limiting of 100mA or less to prevent damage if any paths remain energized for too long.

# Thanks
I would like to thank the following sources:
- [Dottie the Flip Dot Clock](http://dhenshaw.com/Art/Dottie/start.html)
- [Rollsign Gallery](http://rollsigngallery.com/)
