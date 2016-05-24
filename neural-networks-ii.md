# Neural Networks II

## Binary image classification using a neurosynaptic processor: a tradeoff analysis

### Motivation

Would like to move towards autonomous sensors. Given some image, classify whether or not it contains a particular object. The main goal is accuracy, while using very little energy. How does image classification on a neuromorphic processor compare to image classification on a conventional processor?

### Metric

Use a score of `score = |accuracy| / energy_active` where `|accuracy| = (accuracy - 0.5) / 0.5`. This normalizes accuracy to between 0 and 1 (since there is a 50% random guessing chance). `energy_active` is the energy the system uses while active.

### Processors

#### NVIDIA Tegra K1

Jetson development board (I have one of these actually). It's basically Theano / Tensorflow with a bunch of parallelization.

#### IBM TrueNorth

Models 1 million digital spiking neurons, 256 million synapses. CPU runs the operating system, FPGA pushes input data to the spiking neuron chip. Define models with Theano / Tensorflow, but with some extensions that are specific to IBM (strange).

4096 neurosynaptic cores per chip, each core models 256 neurons and 65000 synapses. Draws 50-100 mV of power, inputs and outputs are encoded as spikes. Constraints mean that each neuron can only contain inputs from 256 neurons, which is a limitation for really large neural networks.

### Algorithms

Implemented convolutional neural network on the Tegra, conv-rectify-pool. This doesn't work super well for TrueNorth, so they used an algorithm called TEA, which is conceptually similar to a locally-connected MLP. TEA is a weaker classification algorithm.

### Results

TrueNorth took much about 50% longer to process each image, but was also about 300% more energy efficient (admittedly, CNNs were throttled back a lot).

## A non-parametric framework for quantifying generative inference on neuromorphic systems

### Restricted boltzmann machine

Probabilistic generative model based on Boltzmann distribution. Inference occurs through Gibbs sampling. Generative applications include cleaning noisy or incomplete images. Implemented RBMs on TrueNorth neurosynaptic processor. Spikes are explicitly aligned at a particular block edge.

### Digital gibbs sampler algorithm

Integrate and fire neurons with stochastic leak and threshold to realize the Markov-Chain Monty Carlo sigmoidal sampling rule.

### Implementation tradeoffs

Varying degrees of neuron complexity are possible for inference tasks. The performance metric could be KL-divergence, however, the partition function is difficult to calculate. Alternatively, Annealed Importance Sampling could be used, but was not suitable to their task. Best was nonparametric statistical tests: perform off-line training of RBM, then goodness-of-fit tests.

### Nonparametric statistical tests

#### Kolmogorov-Smirnov test

Maximum distance between two samples

#### Graph-based similarity tests

Crossmatch test: Rosenbaum 2005. 2 sets of samples from two distributions, compute minimum bipartite matching between the samples. Outputs some p-value. 

### Result

Tested the difference between an ideal sampler (implemented in software) and a sampler implemented in hardware. Decision-directed criteria for choosing a sampler; proposed a new metric which was the mean p-value for the model divided by the Boltzmann energy of the model.

### Links

 - [TrueNorth paper, Cassidy et. al. 2013](http://www.research.ibm.com/software/IBMResearch/multimedia/IJCNN2013.neuron-model.pdf)

## A simple variable-width CMOS bump circuit

### Overview

A bump circuit takes two input voltages and produces a bell-shaped curve of the difference between the two voltages. Has been used in more generic neuromorphic applications to determine how similar two voltages are to each other.

Delbruck original bump circuit. Differential pair, biased in subthreshold, added current correlator (product of two currents divided by their sum).

