# A Stripboard Layout for the 'FLIP' Bernoulli Gate

During development I made a prototype on stripboard, based on a design made in [DIYLC](https://bancika.github.io/diy-layout-creator/) :

<p align='center'>
<img width=60%, src="https://github.com/m0xpd/Flip/blob/main/Stripboard/Graphics/Vero%20Prototype.jpg">  
</p>

I have decided (for the first time) to publish a stripboard layout for this project as 
* it is small enough to make the stripboard layout tractable
* there is a considerable tradition within synth DIY for the use of stripboard - as demonstrated at [Eddy Bergman's site](https://www.eddybergman.com/)
* the test/development version was close-enough to completion to make this task simple and, finally, 
* publishing a stripboard layout might make FLIP accessible to a few more potential users, who might otherwise be put off by the PCBs.

# System Schematic

First, we need to look at the schematic for the entire system (presented here as one sheet - unlike in the Eurorack folder, where there are separate sheets for the two PCBs).

The schematic is linked below (click on the image to open the schematic at higher-resolution, which you can download):
<p align='center'>
<img width=70%, src="https://github.com/m0xpd/Flip/blob/main/Stripboard/Graphics/m0xpd%20FLIP%20Bernoulli%20Gate.jpg">
</p>

There is a description of system operation, which references the schematic, [here](https://github.com/m0xpd/Flip/tree/main#circuit-operation).

# Stripboard Layout

The prototype stripboard system (seen pictured at the head of this page) was made from a DIYLC design, which was found to have a few errors (this was my first time using the software). 

I corrected these errors on the prototype and on the layout, yielding the following design:

<p align='center'>
<img width=90%, src="https://github.com/m0xpd/Flip/blob/main/Stripboard/Graphics/m0xpd%20FLIP%20Bernoulli%20Gate%20Stripboard%20Layout.png">
</p>

In an attempt to make the layout clearer, +12V power links are shown in red, GROUND links are in green and -12V links are black. The remainder are blue.

The board is shown below (viewed from the **top/component side**) without components to allow the cuts and links to be more clearly seen:

<p align='center'>
<img width=90%, src="https://github.com/m0xpd/Flip/blob/main/Stripboard/Graphics/m0xpd%20FLIP%20Bernoulli%20Gate%20Cuts%20and%20Links.png">
</p>

Finally, an image showing off-board connections is seen here:

<p align='center'>
<img width=90%, src="https://github.com/m0xpd/Flip/blob/main/Stripboard/Graphics/m0xpd%20FLIP%20Bernoulli%20Gate%20Connections.png">
</p>

The entire DIYLC file is available for download [here](https://github.com/m0xpd/Flip/blob/main/Stripboard/Graphics/m0xpd%20FLIP%20Bernoulli%20Gate.diy). It must be opened in [DIYLC](https://bancika.github.io/diy-layout-creator/)

Whilst the layout above was developed directly from the prototype stripboard system, which is working, the layout has not been verified. I would appreciate either verification from anybody who builds from this layout or notification of any errors/omissions

# Board Size and Operation on Different Power Rails

The board used in this stripboard layout was selected as the largest format used on [Eddy Bergman's site](https://www.eddybergman.com/) who, originally, was building for the [Kosmo standard](https://lookmumnocomputer.discourse.group/t/kosmo-specification/896). The stripboard FLIP layout is really too big for Eurorack (it certainly isn't skiff-friendly!) and would need a deep case to run in a Eurorack system. Most of my card frames are only 155mm deep, which isn't really enough to hold the stripboard (which is ~140mm long). I have one 6U frame which is about 175mm deep, but I still don't plan to run the stripboard prototype *inside* my Eurorack system and I suggest anybody wishing to use FLIP in a Eurorack system should use the [dedicated design](https://github.com/m0xpd/Flip/blob/main/Eurorack/README.md).

The layout shows a Eurorack power header and the system is designed for +/- 12V power operation. Other power connectors can easily fit in the space allocated for the 2*5 Eurorack header and it is self-evident how the power connections should be made. What is less clear is the potential for operation in contexts outside the Eurorack bipolar 12V power supply.

FLIP requires a bipolar power supply and (whilst I haven't tested it) I am confident that it will work on anything from +/- 9V to +/-15V, which will cover most synth standards. The only area I can see which *may* need some adjustment is the range over which the threshold voltage operates, as this is set by diode forward voltage drops over D3,D5), whilst the range of the sawtooth waveform will scale with the power supply (as the 40106's Schmitt trigger thresholds scale). The upper and lower limits of the threshold voltage can be changed by adjusting the volue of R9 and R18, respectively.
