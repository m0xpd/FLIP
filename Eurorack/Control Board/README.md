# FLIP Control Board

This folder contains details of the Control Board for the Eurorack implementation of the FLIP Bernoulli Gate.

There is a KiCad [Project file](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Control%20Board/Files/Flip%20Control%20Board.kicad_pro) a [schematic file](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Control%20Board/Files/Flip%20Control%20Board.kicad_sch) and a [PCB file](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Control%20Board/Files/Flip%20Control%20Board.kicad_pcb). 

<p align='center'>
<img width=30%, src="https://github.com/m0xpd/FLIP/blob/main/Eurorack/Control%20Board/Files/Flip%20Control%20Board%20Unpopulated.jpg">
</p>

[JLC](https://jlcpcb.com/) made my prototype PCBs (seen above) and did their usual great job.

There is also a schematic (click on the image below to open a larger version) and a BoM, saved as an [Excel file](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Control%20Board/Files/Flip%20Control%20Board%20BoM.xlsx)

<p align='center'>
<img width=70%, src="https://github.com/m0xpd/FLIP/blob/main/Eurorack/Control%20Board/Files/Flip%20Control%20Board.jpg">
</p>

The BoM specifies the PJ398SM ('Thonkiconn') Jacks, Alpha 9mm potentiometer and Song Huei trimmer, which are important for mechanical as well as electrical compatability.

As I've mentioned on the [Main Board page](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Main%20Board/README.md), this is only the second project I've developed in KiCad and I'm still feeling my way around. The only aspect of the control board PCB which I regret is the (default, library) footprint for the transistors Q1:3, which has unnecessarily small and close pads. It works, but it asks a lot during soldering. I will modify this if a "v2" revision is ever made. 
