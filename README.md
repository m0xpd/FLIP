# Flip

This repository describes a 'Bernoulli Gate', intended for random switching applications in electronic music.

A Bernoulli Gate, named for Swiss mathematician and physicist [Daniel Bernoulli](https://en.wikipedia.org/wiki/Daniel_Bernoulli), takes a clock input and routes it to one of two outputs, A & B, based on the 
value of an internally generated [Bernoulli Variable](https://web.stanford.edu/class/archive/cs/cs109/cs109.1178/lectureHandouts/070-bernoulli-binomial.pdf). When this (discrete, Boolean) random variable has value 1 the clock is routed to output A, and when the variable has value 0 the clock is routed to output B. The probability of the Bernoulli variable assuming value "1", p, is set by a front panel control (and/or by CV input). The probability of the variable assuming value "0" is (of course) 1-p. 

When the probability is set to p = 0.5, the process becomes equivalent to a "coin toss"; the clock is routed to output A or B based on the decision of a coin toss at each clock cycle. As p moves from the 0.5 value, the coin becomes increasingly "biased", with the outcome favouring one or other outputs. Larger values of p favors output A.

Bernoulli Gates have become familiar objects in modular synthesizers, the definitive example being Mutable Instruments' [Branches](https://pichenettes.github.io/mutable-instruments-documentation/modules/branches/) and various clones from other manufacturers. There is also a Bernoulli Gate implementation within the Mutable Instruments' [Marbles](https://pichenettes.github.io/mutable-instruments-documentation/modules/marbles/) module (and its clones), which is where it caught my interest. These implementations are achieved in software, running on microcontrollers.

The Bernoulli Gate described in this repository is distinguished by being a completely **hardware realisation**. It generates the Bernoulli variable by a test of the instantaneous value of a linear ramp waveform. This ramp is running at a frequency several orders of magnitude above the clock frequencies used in synthesiser timing applications and is asynchronous. Further, the ramp waveform is frequency-modulated by a second asynchronous signal, such that there is no possibility of 'phase' lock between the input clock and a subharmonic of the ramp waveform; the process is sufficiently random.

Two versions of the hardware for Flip are described in this repository. First, there is an implementation as a [Eurorack Module](https://github.com/m0xpd/Flip/blob/main/Eurorack/README.md), with full design details of the PCBs and front panel required for the 6HP module seen in the image at the head of this page. Second, I have included a [stripboard layout](https://github.com/m0xpd/Flip/blob/main/Stripboard/README.md) for the circuit for people who wish to build for a different format or who prefer to avoid the expense of making PCBs. The schematic for Flip is presented as a single, system-level circuit in the [stripboard version](https://github.com/m0xpd/Flip/blob/main/Stripboard/README.md), whereas the [Eurorack version](https://github.com/m0xpd/Flip/blob/main/Eurorack/README.md) splits the system into two elements for implementation on two PCBs. Accordingly, those wishing to understand system operation might prefer to look at the schematic in the stripboard folder first. 

# Circuit Operation

Operation of the 'Flip" Bernoulli Gate will now be described in some detail. Reference should be made to [this system-level schematic](https://github.com/m0xpd/Flip/blob/main/Stripboard/Graphics/m0xpd%20FLIP%20Bernoulli%20Gate.jpg) to which the component idents, circuit block names, and node names, in the description below refer. [Note that these component idents differ from those used in the Eurorack version.]

Flip derives a new value of a Bernoulli variable, p (as has been briefly introduced above) at the start of every clock input. This is done by comparing the magnitude of a sawtooth wave to a threshold value. 

The sawtooth wave is generated by a 40106 oscillator (the block 'RAMP GENERATOR'), which is tuned (by adjustment of trimmer RV1, which should be set so there is approximately 1V on its slider) to run at approximately 3.5kHz. The resulting sawtooth runs between voltages defined by the Schmitt trigger points of the 40106's inputs but the sawtooth is shifted to 0V mean by a high pass filter network C1/R3. Comparing this 'Saw' voltage with the fixed threshold voltage, 'Thres' (the magnitude of which is set either by the front panel probability potentiometer RV3 and/or by CV input to J2) produces a new Bernoulli variable, P at the output of the 'THRESHOLD COMPARATOR', U1d. If the threshold is close to the bottom of the sawtooth's voltage range, the probability is close to one. If the threshold is close to the top of the sawtooth's voltage range, the probability is close to zero. the threshold voltage has been designed so it can be set slightly above and below the sawtooth's range, locking the probability to 1 or 0 (*and thereby setting the gate on or off, with no switching action*), if required.

An external clock signal is applied via J4 to a Schmitt trigger input circuit 'CLOCK IN' (with upward switchig threshold of 1.4V and downward threshold of 1.05V) to produce the gate signal, 'Input', which indicates an active clock . The start of the clock is detected by a typical passive differentiator / diode combination (C10/R30/D8), producing the signal 'dInput'.

The system is built around a trivial state machine which has two states, held on a SR flip-flop. I imlemented the flip-flop on 4001 (NOR) and 4081 (AND) gates, which were to hand (Flip was designed around 'available materials') and provided sufficient logic resources for the remainder of the system. The transitions for the state machine were sufficient to define the Set and Reset signals:

The flip-flop is 'Set' when there is a leading edge of the clock AND the Bernoulli variable is 1 (Set = P.dInput).

The flip-flop is 'Reset' when 'Input' is false (Reset = _Input).

This system was found to work perfectly well in practical musical application, but offended me, as I understood there was possibility for a 'lock' between  a harmonic of the clock and the sawtooth wave, making the process less than random. I had anticipated this in design and arranged for the sawtooth oscillator to be voltage controlled. A second stage of the 40106 ('FM Osc') is used to implement an oscillator from which a triangular wave (at around 800Hz) is generated. This triangular wave frequency modulates the sawtooth, effectively removing the possibility of any 'lock' between the sawtooth and a regular clock signal. 

The three outputs use a simple 'emitter follower' buffer scheme taught by Ken Stone. The 'A' output follows directly the 'Q' output of the flip-flop. The 'B' output must be derived from additional logic to AND the complemented flip-flop state _Q with the clock. Finally, a clock signal output is provided. This output is driven by a further inversion of _Input, rather than adding further load to the output of the CLOCK IN circuit, which could impact the edge detection circuit. 


