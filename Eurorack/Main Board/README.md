# FLIP Main Board

This [folder](https://github.com/m0xpd/FLIP/tree/main/Eurorack/Main%20Board) contains details of the Main Board for the Eurorack implementation of the FLIP Bernoulli Gate, expressed as a KiCad project.


There is a KiCad [Project file](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Main%20Board/Files/Flip%20Main%20Board.kicad_pro) a [schematic file](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Main%20Board/Files/Flip%20Main%20Board.kicad_sch) and a [PCB file](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Main%20Board/Files/Flip%20Main%20Board.kicad_pcb). 

<p align='center'>
<img width=30%, src="https://github.com/m0xpd/FLIP/blob/main/Eurorack/Main%20Board/Files/Flip%20Main%20Board%20Unpopulated.jpg">
</p>

[JLC](https://jlcpcb.com/) made my prototype PCBs (seen above) and did their usual great job.

There is also a schematic (click on the image below to open a larger version) and a BoM, saved as an [Excel file](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Main%20Board/Files/Flip%20Main%20Board%20BoM.xlsx)

<p align='center'>
<img width=70%, src="https://github.com/m0xpd/FLIP/blob/main/Eurorack/Main%20Board/Files/Flip%20Main%20Board.jpg">
</p>

The schematic above follows pretty closely the [system-level schematic presented in the stripboard folder](https://github.com/m0xpd/Flip/blob/main/Stripboard/Graphics/m0xpd%20FLIP%20Bernoulli%20Gate.jpg) apart from the fact that I have swapped the inverters (from the 40106) on the input to the Clock output stage and in the State Machine with unused gates in the 4001 package. This was done solely for convenience in laying out the PCB and has no impact on system operation - the Schmitt trigger inputs were not being exploited and the NOR gates can work perfectly well as inverters. Obviously, all the other 'missing' elements (user interface components, output buffers, etc) are on the [control board](https://github.com/m0xpd/FLIP/tree/main/Eurorack/Control%20Board)

