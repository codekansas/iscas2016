# Neural Networks III

## Dynamic hand gesture recognition for wearable devices with low complexity recurrent neural networks

### Introduction and background knowledge

Wearable devices are pretty popular. Two types of hand gesture recognition: static and dynamic. Dynamic means that it recognizes patterns. Image and accelerometer based methods are both used. Network: CNN - LSTM RNN. Three convolutional layers and one recurrent layer to the output (for the image-based method) vs. one single recurrent layer (for the accelerometer-based method).

### Problems

There are a ton of parameters for a neural network, so it is important to reduce the size of memory used in order to embed them. In this case, it means doing layer-wise sensitive analysis to find the optimal word lengths.

Used the backpropagation through time algorithm for training the RNN. Gave a weight quantization function that gives an estimation of how sensitive weights are to bit accuracy, which can be used to estimate word sizes. Four types of activation functions: `sigmoid`, `tanh`, `relu`, and `softplus`.

### Layerwise sensitivity analysis

Find the most sensitive layer in the network. Group the weight parameters layerwisely. Retrain the network in the fixed-point domain.

### Results

Resized each image to 32 by 32 pixels (from original 1024 x something). Using 2 bit quantization for all weight groups can save 93.75% of memory. The total number of multiplications is greatly reduced. The model can efficiently be implemented in embedded systems like Cortex A9. They evaluated how neural networks could be implemented with a small word length (neat).

### Links

 - [Wikipedia page for Cortex A9](https://en.wikipedia.org/wiki/ARM_Cortex-A9)
 - [Binary Connect paper by Bengio](http://arxiv.org/abs/1511.00363)

## Effective sensor fusion with event-based sensors and deep network architectures

### Event-based sensors

Dynamic vision sensors: Supposed to be like the eye. Models cells in the eye that detect changes in pixels; each pixel generates an event if a local contrast change exceeds a threshold. Can detect on-contrast and off-constrast changes separately.

Dynamic audio sensor: Supposed to be like the cochlea. Acts loosely like a frequency analyzer. Different parts of the membrane are sensitive to different frequencies, so it is modeled by a filterbank that responds to individual frequencies. With both of these sensors, there are no events if no changes are observed.

### Deep networks

Classification with convolutional neural networks (CNNs). Task where classification is done using CNNs. Take the sensor output of an event-based sensor and stream it into a network which is updated on every clock tick.

Training and testing as analog CNNs: Bin each set of spikes and treat them as a particular frame (like a rate code). Training as an analog CNN and testing as a spiking CNN: more appropriate. Transform data into frame-based inputs and outputs. Train a neural network offline for these input-output pairs. Normalize neuron weights to account for spiking inputs. Put the now-spiking network in front of the spiking sensor and evaluate its performance.

### MNIST digit database

The demo is really cool. Given a particular digit, the number of spikes representing the correct number increases while the others don't. N-MNIST: A dataset like MNIST but with saccades.

### Classifying audio using MFCCs

First, play the track to the cochlea, which produces spikes. Bin the spikes (you get a spectrogram-like map, where each pixel is the number of spikes at a particular time/frequency - cochleagrams). For testing, make the network spiking and you don't have to use bins.

### Results

N-MNIST performance was 95.72% accuracy (quite good) but might have been trained on testing dataset? Sensory fusion deep belief network (e.g. both visual and audio inputs). Deep network combines information from both visual and audio spiking inputs. Sensory fusion can improve performance.
