# The 'FLIP' Bernoulli Gate for Eurorack

The Eurorack version of FLIP is implemented as a 'sandwich' construction of two printed circuit boards:

<p align='center'>
<img width=20%, src="https://github.com/m0xpd/FLIP/blob/main/Graphics/Flip%20Sandwich%20Construction%20LoRes.jpg">
</p>

The [main board](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Main%20Board/README.md) contains the majority of the active electronics, realised in 4000 series CMOS logic and a quad op-amp.

The [control board](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Control%20Board/README.md) accommodates all the [front panel](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Front%20Panel/README.md) components and the output buffer stages. 

The component board is mounted to the front panel by the probability control potentiometer, RV2, and five PJ398SM ('Thonkiconn') 3.5mm jack sockets.

The two PCBs are joined electrically by two 1*8 way 0.1 inch headers, with further mechanical security provided by a pair of 3mm bolts and spacers.

**Note:** the 12V line runs close to the upper spacer on the main board (on the bottom side of the PCB). If you use a metal spacer you would be well advised to insert an insulating washer at this point. I didn't have an insulating washer available on my first assembly, so I made an insulating spacer. This has now been replaced, as I got some M3 Nylon washers. Perhaps I'll move the 12V track if there's ever a revision of the PCB. 

Full design details of the [main board](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Main%20Board/README.md), [control board](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Control%20Board/README.md), and [front panel](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Front%20Panel/README.md) are presented as KiCad projects. The folders also include schematics and BoMs, where relevant.

Populated boards from my first build are seen below.

First, there is an exploded view of the "outside" of the sandwich; the component side of the main board (left) and the bottom side of the control board (right), which houses the "user interface" components which protrude through the front panel:

<p align='center'>
<img width=50%, src="https://github.com/m0xpd/FLIP/blob/main/Graphics/Flip%20PCBs%20Populated%20Outside%20View.jpg">
</p>

Finally, an exploded view of the "inside" of the sandwich, showing the headers which join the boards, the bottom of the main board (left), and the component side of the control board (right):

<p align='center'>
<img width=50%, src="https://github.com/m0xpd/FLIP/blob/main/Graphics/Flip%20PCBs%20Populated%20Inside%20View.jpg">
</p>

(The two boards are exactly the same size but sit at slightly different distances from the camera in the images above, making them *appear* differently dimensioned.)

# Specifications

**Width:** 

FLIP is **6 HP wide**.

**Depth:**

FLIP extends **43 mm** behind the [front panel](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Front%20Panel/README.md) when a conventional Eurorack power header **with strain relief** is inserted.

**Power Consumption:**

| Power Rail | Current |
|---|---|
| +12V | **5.5mA** (max) |
| -12V | **2.7mA** (max) |
| 5V | **0** |
