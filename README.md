# Bernoulli

This repository describes a 'Bernoulli Gate', intended for use in electronic music and similar switching applications.

A Bernoulli Gate, named for Swiss mathematician [Daniel Bernoulli](https://en.wikipedia.org/wiki/Daniel_Bernoulli), takes a clock input and routes it to one of two outputs, A & B, based on the 
value of an internally generated [Bernoulli Variable](https://web.stanford.edu/class/archive/cs/cs109/cs109.1178/lectureHandouts/070-bernoulli-binomial.pdf). When the variable =1, the clock is routed to one output, A and when the variable =0, the clock is routed to the other output, B. The probability of the Bernoulli variable assuming value "1", p, is set by a front panel control (and/or by CV input). The probability of the variable assuming value "0" is 1-p. 

At extreme settings of probability the clock always goes to one or other output, as described, but at intemediate settings a random allocation is made, such that the probability of the clock routing to output A is p and the probability of routing to B is (1-p).

Bernoulli Gates are familiar objects in modular synthesizers, the definitive example being Mutable Instruments [Branches](https://pichenettes.github.io/mutable-instruments-documentation/modules/branches/) and various clones and versions on other platforms. There is also a Bernoulli Gate implementation within the Mutable Instruments [Marbles](https://pichenettes.github.io/mutable-instruments-documentation/modules/marbles/) module (and its clones), which is where it caught my interest. All these implementations are achieved in software, running on microcontrollers.

The Bernoulli Gate described in this repository is distinguished by being a completely hardware realisation. It generates the Bernoulli variable by a test of the instantaneous value of a linear ramp waveform. This ramp is running at a frequency several orders of magnitude above the clock frequencies used in synthesiser timing applications and is asynchronous. Further, it is frequency-modulated by a second asynchronous signal, such that there is no possibility of phase lock between the input clock and a subharmonic of the ramp waveform; the process is sufficiently random.


