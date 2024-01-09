# A Eurorack Implementation of the 'FLIP' Bernoulli Gate

The Eurorack version of Flip is implemened as a 'sandwich' consruction of two printed circuit boards.

The [main board](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Main%20Board/README.md) contains the majority of the active electronics, realised in 4000 series CMOS logic and a quad J-FET input TL-84 op-amp.

The [control board](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Control%20Board/README.md) accommodates all the [front panel](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Front%20Panel/README.md) user interface components, the input/output connectors, and the output buffer stages. The component board is mounted to the front panel by the probability control potentiometer and five 3.5mm jack sockets.

The two PCBs are joined electrically by two 1*8 way 0.1 inch headers, with further mechanical security provided by a pair of 3mm bolts and spacers.

Full design details of the main board, [control board](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Control%20Board/README.md), and [front panel](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Front%20Panel/README.md) are presented as KiCad projects. The folders include schematics and BoMs, where relevant.

# Specifications

**Width:** 

FLIP is **6 HP wide**.

**Depth:**

FLIP extends **43 mm** behind the [front panel](https://github.com/m0xpd/FLIP/blob/main/Eurorack/Front%20Panel/README.md) when a conventional Eurorack power header **with strain relief** is inserted.

**Power Consumption:**

| Power Rail | Current |
|---|---|
| +12V | **xxmA** |
| -12V | **xxmA** |
| 5V | **0** |
