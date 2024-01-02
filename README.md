# Bernoulli

This repository describes a 'Bernoulli Gate', intended for random switching applications in electronic music.

A Bernoulli Gate, named for Swiss mathematician and physicist [Daniel Bernoulli](https://en.wikipedia.org/wiki/Daniel_Bernoulli), takes a clock input and routes it to one of two outputs, A & B, based on the 
value of an internally generated [Bernoulli Variable](https://web.stanford.edu/class/archive/cs/cs109/cs109.1178/lectureHandouts/070-bernoulli-binomial.pdf). When this (discrete, Boolean) random variable has value 1 the clock is routed to output A, and when the variable has value 0 the clock is routed to output B. The probability of the Bernoulli variable assuming value "1", p, is set by a front panel control (and/or by CV input). The probability of the variable assuming value "0" is (of course) 1-p. 

When the probability is set to p = 0.5, the process becomes equivalent to a "coin toss"; the clock is routed to output A or B based on the decision of a coin toss at each clock cycle. As p moves from the 0.5 value, the coin becomes increasingly "biased", with the outcome favouring one or other outputs. Larger values of p favors output A.

Bernoulli Gates have become familiar objects in modular synthesizers, the definitive example being Mutable Instruments' [Branches](https://pichenettes.github.io/mutable-instruments-documentation/modules/branches/) and various clones from other manufacturers. There is also a Bernoulli Gate implementation within the Mutable Instruments' [Marbles](https://pichenettes.github.io/mutable-instruments-documentation/modules/marbles/) module (and its clones), which is where it caught my interest. These implementations are achieved in software, running on microcontrollers.

The Bernoulli Gate described in this repository is distinguished by being a completely **hardware realisation**. It generates the Bernoulli variable by a test of the instantaneous value of a linear ramp waveform. This ramp is running at a frequency several orders of magnitude above the clock frequencies used in synthesiser timing applications and is asynchronous. Further, the ramp waveform is frequency-modulated by a second asynchronous signal, such that there is no possibility of 'phase' lock between the input clock and a subharmonic of the ramp waveform; the process is sufficiently random.


