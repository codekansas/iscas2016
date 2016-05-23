# Neural Networks I

## Memory-error tolerance of scalable and highly parallel architecture for restricted boltzmann machines in deep belief networks

### Introduction

We'd like to make deep learning networks that are bigger and bigger. As the number of parameters increases, however, the number of parameters increases exponentially. One of the most critical factors in this is memory error, especially for low voltage applications. Bit Error Rate (BER) depends on Vdd: 0.01% at 0.6V, 0.0001% at 0.7V...

### Concept of the study

Implemented a deep learning hardware system on an FPGA. Neural networks have inherent robustness against precision error. After intentionally injecting faults into the weights on the FPGA, the deep learning system was not greatly affected.

### Restricted Boltzmann Machine

Hidden layer and visible layer, learning to decrease the difference between the activation of the visible units and some target activation (for example, learning to represent digits). A deep belief network is built by adding more hidden layers, and can be trained independently. Fine tuning is done using backpropagation.

### Implementing RBM on hardware

Concerned about the size of the network, because the number of connections increases quadratically with the number of neurons. Fault-tolerant analysis was done by training three RBMs for classifying MNIST digits, then flipping some random bits (realistically). Fine tuning through backpropagation completely fixed the error.

### Result

Bit error rates of above `10^-4` showed significant drops in accuracy. They had a highly scalable RBM implementation on a hardware platform.

## Liquid state machine based pattern recognition on FPGA with firing-activity dependent power gating and approximate computing

### Motivation

Von Neumann architecture is pretty old. There has been a lot of interest in building brain-inspired computers. The brain is made up of neurons plus feed-forward and recurrent networks. They use different types of codes to send information, like rate or timing codes. Brain-inspired computing is a compromise between biological plausibility, complexity and performance.

For a liquid-state machine, they used spiking neurons and tried to build in some spiking mechanism. A liquid-state machine has some group of input neurons fed into a network of "reservoir neurons", then some output neurons with plastic synapses from the reservoir neurons. With spiking neurons this training problem gets even harder. Fixed synapses in the recurrent reservoir make this problem easier, but probably less realistic. Since there are recurrent connections in the network, interesting spatial-temporal patterns can be found.

### Liquid state machine processor architecture

Reservoir is made up of firing activity-based power / clock gating, adjustable arithmetic precision / approximate computing microprocessors. Randomly generated reservoir connections. Learning is biologically inspired: local probabilistic spike-based learning. Tradeoff between learning performance and learning speed and memory retention. Given some presynaptic spike and postsynaptic activity, we can calculate how to change the strength of the synapse.

### Implementation

Used an FPGA. Liquid elements (LEs) compute the liquid response in parallel, liquid response is used to train the model. Crossbar interface for feeding the output back into the inputs for the next timestep. Plastic synaptic weights stored in BRAMs (Xilinx FPGA). Each OE operates in parallel.

### Digital neural models neurons

Using a leaky integrate-and-fire (LIF) model. Using a 2nd-order synaptic model led to better performance. Implementation of liquid elements is done using standard logic gates. Output elements are realized in a similar way, plus a plastic weight.

Energy efficiency is mostly lost to the adders. Monitor the firing activities during the first phase of training to generate the updates. Use approximate adders, varying precision.

### Firing-activity based clock/power gating

Classify each neuron based on how much it fires, then change the precision based on the firing rate. More firing gets higher precision, less firing gets lower precision. Generated an 88x speedup over general-purpose CPUs. Get significant energy savings on the FPGA. Used some techniques for saving energy (e.g. gating off silent neurons). The network size is pretty small, only about 130 neurons.

### Links

 - [Wikipedia article on LSMs](https://en.wikipedia.org/wiki/Liquid_state_machine)

## Learning spatio-temporal patterns in the presence of input noise using phase-change memristors

### Introduction

Scaling up cognitive systems get bottlenecked around energy consumption. The brain is very parallel and asynchronous. Neurons have all the knowledge stored in their synaptic weights. Could use memristor technologies to construct neuromorphic systems. In particular, we would like to use memristors to generate synapses.

### Crystals

Crystallization dynamics can be described using an interfacial crystal growth model. Map functionality of a biological synapse to the phase-change synapse. Synapses have input modulation, which can be modeled as conductance dependent on amorphous volume, and plasticity, which can be modeled as crystal growth.

STDP: Spike-timing-dependent plasticity, biologically plausible local learning rule. Would like to map STDP to a phase change device. Integrate-and-fire neurons are used. Correlated inputs increase synaptic weights, uncorrelated inputs decrease synaptic weights (STDP). FPGA board communicates with the computer.

System detects temporal correlations between groups of signals that have the same rate.

## Neuromorphic implementation of attractor dynamics in decision circuit with NMDARs: A simulation study

### Introduction

Emulation of cognitive functions in neuromorphic systems: Develop biomimetic device with adaptive and interactive behaviors. Decision making: Select an option among a set of alternatives.

### Attractor dynamics

Winner-take-all (WTA) mechanism: Saddle-node structure. There is one unstable steady state and two stable steady states. Depending on how large the node is, this model tends towards one of two attractor states (high or low firing rate for input neurons). In biological systems, there are excitatory synapses (AMPA and NMDA).

## A VLSI implementation of a calcium-based plasticity learning model

### Learning

Two types of learning: Hebbian and STDP. Hebbian learning: "Neurons that fire together, wire together." STDP: Correlation-based. SCBM: Stochastically connected Boltzmann machine. Gives learning rules for realistic spiking behavior. Gave synapse circuits for different learning rules.

STDP circuit simulation: The learning rule looks a lot like what the actual STDP learning rule is. After doing some simulations, depression does actually decrease synaptic weights, and potentiation does actually increase synaptic weights.