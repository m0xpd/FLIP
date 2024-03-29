# FLIP

This repository describes a 'Bernoulli Gate', intended for switching applications in electronic music.

<p align='center'>
<img width=40%, src="https://github.com/m0xpd/FLIP/blob/main/Graphics/Flip%20Front%20Perspective%20Right.jpg">
</p>
  
You can dive straight in to details of the [Eurorack module](https://github.com/m0xpd/Flip/blob/main/Eurorack/README.md), or a [stripboard layout for the circuit](https://github.com/m0xpd/FLIP/tree/main/Stripboard), or read more about the background and operation of this new design, below.

# Background

A Bernoulli Gate, named for Swiss mathematician and physicist [Daniel Bernoulli](https://en.wikipedia.org/wiki/Daniel_Bernoulli), takes a clock or gate input and routes it to one of two outputs, A & B, based on the 
value of an internally generated [Bernoulli Variable](https://web.stanford.edu/class/archive/cs/cs109/cs109.1178/lectureHandouts/070-bernoulli-binomial.pdf). When this (discrete, Boolean) random variable has value 1 the clock is routed to output A, and when the variable has value 0 the clock is routed to output B. The probability of the Bernoulli variable assuming value "1", p, is set by a front panel control (and/or by CV input). The probability of the variable assuming value "0" is (of course) 1-p. 

When the probability is set to p = 0.5, the process is equivalent to a "coin toss"; the input is routed to output A or B based on the outcome of a fair coin toss at each input onset. As p moves from the 0.5 value, the coin becomes increasingly "biased", with the outcome favouring one or other output. Larger values of p favors output A.

Bernoulli Gates have become familiar objects in modular synthesizers, the definitive example being Mutable Instruments' [Branches](https://pichenettes.github.io/mutable-instruments-documentation/modules/branches/) and various clones from other manufacturers. There is also a Bernoulli Gate within Mutable Instruments' [Marbles](https://pichenettes.github.io/mutable-instruments-documentation/modules/marbles/) module (and its clones), which is where it caught my interest. These implementations are achieved in software, running on microcontrollers.

# FLIP - a Hardware Bernoulli Gate

The Bernoulli Gate described in this repository is distinguished by being a completely **hardware realisation**. It generates the Bernoulli variable by a test of the instantaneous value of a linear ramp waveform. This ramp is running at a frequency several orders of magnitude above the clock frequencies typically used in synthesiser timing applications and is asynchronous to such input clocks/gates. Further, the ramp waveform is frequency-modulated by a second asynchronous signal, such that there is no possibility of 'phase' lock between an input clock and a subharmonic of the ramp waveform; the process is sufficiently random.

I should make it clear - I have absolutely nothing against the use of microcontrollers and DSP in modular synths, as I believe my work demonstrates. I designed FLIP for pleasure as a deliberate 'break' from playing with software-based systems in the recent development of my [STRACHEY](https://github.com/m0xpd/STRACHEY) sequencer. I based FLIP in hardware (rather than software) because I wanted the pleasure of something different. 

However, I should also confess to a feeling that we have become too ready to turn to soft solutions. There is something wasteful about having a little microcontroller (like Branches' ATMega88) sitting there doing something as simple as implementing (in that case two) Bernoulli Gates, even though it was *definitively the correct solution* for Mutable's commercial product. But I'm not designing for production - I'm enjoying myself, playing with ideas and materials I find to hand (often literally from the junk box). So - whilst I could easily have implemented my new Bernoulli Gate on an Atmel device or a PIC or similar, I think there remains something interesting and worthwhile in doing it 'old school'. 

I also recognise there are some members of the synth DIY community who actively do not like embedded/DSP. I repeat: **I'm NOT one of them**. But I'm pleased this project will be accessible to them.

Two versions of the hardware for FLIP are described in this repository. First, there is an implementation as a [Eurorack Module](https://github.com/m0xpd/Flip/blob/main/Eurorack/README.md), with full design details of the PCBs and front panel required for the 6HP module seen in the image at the head of this page. Second, I have included a [stripboard layout](https://github.com/m0xpd/Flip/blob/main/Stripboard/README.md) for the circuit for people who wish to build for a different format or who prefer to avoid the expense, delay, and minimum order quantities involved in making PCBs. The schematic for FLIP is presented as a single, system-level circuit in the [stripboard version](https://github.com/m0xpd/Flip/blob/main/Stripboard/README.md), whereas the [Eurorack version](https://github.com/m0xpd/Flip/blob/main/Eurorack/README.md) splits the system into two elements for implementation on two PCBs. Accordingly, those wishing to understand system operation might prefer to look at the schematic in the [stripboard folder](https://github.com/m0xpd/FLIP/tree/main/Stripboard) first. 

FLIP has two controls: the main 'probability' control and a control for the CV attenuverter. Advancing the probability control clockwise increases the probability that output A will be activated. When a positive CV is input, advancing the attenuverter control clockwise also increases the probability that A will 'fire' (the opposite sense applies when a negative CV is input). 

# Demo Video

A [short video](https://youtu.be/AdmhHrzYtKI), introduces FLIP and demonstrates its functions. The video is never going to win any oscars, not least as the camera is out of focus for the central 'demo' section. I don't know what changed between recording the music for the intro and 'closing credits' and the main, central demo portion. However, the message is clear, even if the image is not.    

# License

Material in this repository, including the circuit design and Eurorack implementation of FLIP, is published under a Creative Commons CC BY-SA 4.0 [License](https://github.com/m0xpd/Flip/blob/main/LICENSE.txt)

# Circuit Operation

Operation of the 'FLIP' Bernoulli Gate will now be described in some detail. Reference should be made to [this system-level schematic](https://github.com/m0xpd/Flip/blob/main/Stripboard/Graphics/m0xpd%20FLIP%20Bernoulli%20Gate.jpg) to which the component idents, circuit block names, and node names in the description below refer. [Note that these component idents differ from those used in the Eurorack version.]

FLIP derives a new value of a Bernoulli variable, p (as has been briefly introduced above) at the start of every clock input. This is done by comparing the instantaneous amplitude of a sawtooth wave to a threshold value. 

The sawtooth wave is generated by a 40106 oscillator (the block 'RAMP GENERATOR'), which is tuned (by adjustment of trimmer RV1, which should be set so there is approximately 1V on its wiper) to run at approximately 3.5kHz. The resulting sawtooth runs between voltages defined by the Schmitt trigger points of the 40106's inputs but the sawtooth is shifted to 0V mean by the high pass filter network C1,R3. Comparing this 'Saw' voltage with the fixed threshold voltage, 'Thres' (the magnitude of which is set either by the front panel probability potentiometer RV3 and/or by CV input to J2) produces a new Bernoulli variable, P at the output of the 'THRESHOLD COMPARATOR'. If the threshold is close to the bottom of the sawtooth's voltage range, the probability is close to (logical) one. If the threshold is close to the top of the sawtooth's voltage range, the probability is close to (logical) zero. the threshold voltage has been designed so it can be set slightly above or below the sawtooth's range, locking the probability to 1 or 0 (*and thereby setting the 'A' output on or off, with no switching action*), if required.

The photo below shows the 'Saw' waveform (in Yellow), the threshold voltage, 'Thres', set to just above the bottom of the sawtooth's voltage range (in Magenta) and the resulting Bernoulli variable, 'P' (in Cyan). The FM modulation of the saw oscillator (see below) has been disabled to make the image clearer and the results were captured from the prototype [stripboard](https://github.com/m0xpd/Flip/blob/main/Stripboard/README.md) system.

<p align='center'>
<img width=80%, src="https://github.com/m0xpd/Flip/blob/main/Graphics/Triggering%20at%20Bottom%20of%20Range.jpg">
</p>

It is seen that the Bernoulli variable is almost always "1", as expected.

In the practical circuit, frequency response and slew rate limitations in the op-amp used as the comparator constrain behaviour when the threshold is placed closer to the top of the sawtooth's range.

The photo below shows behaviour when the threshold, 'Thres' is at about 50% of the positive range of the sawtooth.

<p align='center'>
<img width=80%, src="https://github.com/m0xpd/Flip/blob/main/Graphics/Triggering%20at%20Top%20of%20Range.jpg">
</p>

It is seen that the Bernoulli variable is almost always "0"; this is the highest we can take the threshold voltage before it locks the gate "off". Taking the threshold value any higher in the practical circuit causes the comparator to fail to produce any 'non-zero' (in a logical sense) output. This is why the sawtooth wave - and the operation of FLIP - has been limited to 3.5kHz. 

The potential divider at the CV input, J2 (R13,R14) is loaded by the input resistance of the susbsequent attenuverter stage; this "loaded attenuator" produces around 6dB of attenuation in any configuration of the attenuverter. This allows a 5V CV signal to control the system, switching the gate from fully "on" to fully "off", whilst a higher CV input can achieve the same control at a lower attenuverter setting. Obviously, more subtle changes in configuration can be achieved with smaller control voltages, or with lower attenuverter settings.  

The external clock or gate signal is applied via J4 to FLIP's Schmitt trigger input circuit 'CLOCK IN' (with upward switchig threshold of 1.4V and downward threshold of 1.05V) to produce the gate signal, 'Input', which indicates an active input. The start of this input is detected by a typical passive differentiator / diode combination (C10,R30,D8), producing the signal 'dInput'.

The system is built around a trivial state machine which has two states, held on a SR flip-flop. I imlemented the flip-flop on 4001 (NOR) and 4081 (AND) gates, which were to hand (FLIP was designed around 'available materials') and provided sufficient logic resources for the remainder of the system. The transitions for the state machine were sufficient to define the Set and Reset signals:

The flip-flop is 'Set' when there is a leading edge of the clock AND the Bernoulli variable is 1 (Set = P.dInput).

The flip-flop is 'Reset' when 'Input' is false (Reset = _Input).

This system was found to work perfectly well in practical musical application, but offended me, as I understood there was possibility for a 'lock' between  a harmonic of the clock and the sawtooth wave, making the process less than random. I had anticipated this in design and arranged for the sawtooth oscillator to be voltage controlled. A second stage of the 40106 ('FM Osc') is used to implement an oscillator from which a triangular wave (at around 800Hz) is generated. This triangular voltage is used to frequency modulate the sawtooth, effectively removing the possibility of any 'lock' between the sawtooth and a periodic input signal. 

The photo below shows triggering with FM enabled:

<p align='center'>
<img width=80%, src="https://github.com/m0xpd/Flip/blob/main/Graphics/Triggering%20with%20FM.jpg">
</p>

In this case, the threshold has been set to approximately 0V and the Bernoulli variable is returning a true value approximately 35% of the time (but not achieving the 50% score of a "fair" system, as the 0V threshold is above the middle of the range determined by the two limiting cases shown in the previous two oscilloscope screen shots). Variation in the period of the sawtooth (and the resulting outputs from the comparator) caused by the frequency modulation is clearly visible.

FLIP's three outputs use a simple 'emitter follower' buffer scheme taught by Ken Stone. The 'A' output follows directly the 'Q' output of the flip-flop. The 'B' output must be derived from additional logic to AND the complemented flip-flop state _Q with the input clock/gate signal. Finally, an output is provided which mirrors the input. This output is driven by a further inversion of _Input, rather than by adding load to the output of the CLOCK IN circuit, which could impact the edge detection circuit. 


