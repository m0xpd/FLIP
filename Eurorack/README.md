# A Eurorack Implementation of the 'FLIP' Bernoulli Gate

The Eurorack version of Flip is implemented as a 'sandwich' construction of two printed circuit boards:

<p align='center'>
<img width=30%, src="https://github.com/m0xpd/FLIP/blob/main/Graphics/Flip%20Sandwich%20Construction%20LoRes.jpg">
</p>

The [main board](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Main%20Board/README.md) contains the majority of the active electronics, realised in 4000 series CMOS logic and a quad J-FET input TL084 op-amp.

The [control board](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Control%20Board/README.md) accommodates all the [front panel](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Front%20Panel/README.md) user interface components, the input/output connectors, and the output buffer stages. 

The component board is mounted to the front panel by the probability control potentiometer and five 'Thonkiconn' 3.5mm jack sockets.

The two PCBs are joined electrically by two 1*8 way 0.1 inch headers, with further mechanical security provided by a pair of 3mm bolts and spacers.

**Note:** the 12V line runs close to the upper spacer on the main board (on the bottom side of the PCB). If you use a metal you would be well advised to insert an insulating washer at this point. I didn't have one on my first assembly, so I made an insulating spacer.  

Full design details of the [main board](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Main%20Board/README.md), [control board](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Control%20Board/README.md), and [front panel](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Front%20Panel/README.md) are presented as KiCad projects. The folders also include schematics and BoMs, where relevant.

# Specifications

**Width:** 

FLIP is **6 HP wide**.

**Depth:**

FLIP extends **43 mm** behind the [front panel](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Front%20Panel/README.md) when a conventional Eurorack power header **with strain relief** is inserted.

**Power Consumption:**

| Power Rail | Current |
|---|---|
| +12V | **5.5mA** |
| -12V | **2.7mA** |
| 5V | **0** |
