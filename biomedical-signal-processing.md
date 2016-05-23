# Biomedical Signal Processing

## Detecting Tandem Repeats in DNA using Ramanujan Filter Banks

### Applications

 - DNA Fingerprinting
 - Detecting cancer

### About

Given a DNA sequence, can we detect the period of a particular sequence?

Ramanujan Filter Bank

    Rax(n) -> c1(n), c2(n), ... cm(n)

Ramanujan filter bank was designed to detect numbers: transform DNA sequence into numerical value (e.g. `A -> 1`, `T -> 2` ...)

### Tandem Repeat Finder

Highly cited paper. Application in forensics: RFB outperforms TRF.

Fourier transform: STFT. STFT works for forensics, but the RFB gave features which were much more discernable than the STFT. Maybe RFB works as an alternative to STFT? It seems like it's looking at periods rather than frequencies (not clear how it works exactly)

Multiple concurrent periods: STFT and RFB work approximately the same. STFT with window length 70 doesn't isolate them very well, as it might for concurrent "frequencies"

### Links

 - [A paper that talks about RFBs](http://www.eurasip.org/Proceedings/Eusipco/Eusipco2015/papers/1570091833.pdf)
 - [Wikipedia page for Ramanujan sum](https://en.wikipedia.org/wiki/Ramanujan%27s_sum)

## Two-Pass Beamforming for Ultrasound Imaging

### Background

Delay-and-sum (DAS) beamformer: Nonadaptive weight vector `[w1, w2, ..., wM]^T`. Computationally inexpensive, pour rejection of interferers. Static, non-adaptive weights which help improve the strength of the signal.

`Transducer -> Delays -> Weights -> y(t)`

Generalized sidelobe canceller (GSC): Adaptive weight vector `[w_a1(t), w_a2(t), ..., w_aM(t)]^T`. Computationally expensive (matrix inversion), good rejection of interferers.

`x(t) -> [w_q, B -> w_a] -> y(t)`

 - `w_q` are quiescent weights

Needed: Good beamforming performance at low cost. Two-pass DAS / GSC.

### Proposed method

Main idea: Selectively replace nonadaptive (DAS) outputs `y_DAS` with adaptive (GSC) outputs `y_GSC`. Selection criteria are log-compressed value of `y_DAS` envelope in some range. Can run GSC on these values.

### Advantages

 - Expensive GSC beamforming is performed only for a small number of input snapshots, selected from the total
 - The mixed version actually improves scatter contrast over GSC, and is more computationally efficient

### Disadvantages

 - Need to compute preliminary envelope
 - Need to decide on effective threshold settings
 - Need to decide on appropriate buffer size

### Links

 - [Wikipedia page for beamforming](https://en.wikipedia.org/wiki/Beamforming)

## A New L1-Regularized Time-Varying Autoregressive Model for Brain Connectivity Estimation: a Study Using Visual Task-Related fMRI Data

### Introduction

Brain connectivity network (BCN): Connectivity between different regions in the brain. Nodes representing neural units, edges representing connectivity. BOLD: Blod-oxygen-level dependent signal. fMRI measures the BOLD signal as a proxy for brain connectivity.

At each timepoint, the BOLD signal forms a vector. Together, they form a very large matrix. They want to use this data to estimate brain connectivity.

### Challenges

 - High dimensionality of variables
 - Massive number of parameters to estimate
 - Time-varying networks, one network for each timepoint
 - Large memory requirements

### Contributions

 - Identify dynamic BCN for each timepoint instead of static
 - Use L1 regularization to impose prior information to reduce the complexity of variable estimation
 - Matrix form: `X(t+1) = A(t)X(t) + b(t) + err(t)`
   - `A(t)`: Connectivity matrix
   - `X(t)`: BOLD signal vector at timepoint `t`
   - `b(t)`: Bias vector
   - `err(t)`: Error term
 - Solving the above form becomes a minimization problem, but because there are a lot of variables to estimate, much more data is needed than is available
 - Biological processes are smooth, slow. Can impose these facts (continuity and sparsity contraints) on the model to reduce complexity. Sparsity constraint: Apply L1 regularization to the gradients. Continuity constraint: Make `X(t+1)` similar to `X(t)`.

### Results

 - Areas are usually connected to themselves
 - T-test is used to determine if connectivity is significant over baseline
 - High connectivity among visual regions of the brain
 - Visual processing occurs in layers (MOG to FuG). Higher region has a prediction of the visual input, and gets a residual error signal (possibly). This is called a "predictive coding mechanism"

### Conclusions

 - L-BFGS algorithm is possible in a computationally efficient way after applying constraints
 - In the future, hope to apply this method to other datasets

### Links

 - [The NKI-Rockland Sample: A Model for Accelerating the Pace of Discovery Science in Psychiatry](http://www.ncbi.nlm.nih.gov/pubmed/23087608)

## Ultrasound Image Despeckling in the Countourlet Domain Using the Cauchy Prior

### Ultrasound images

Ultrasound images are very popular for pathology detection. There is a lot of noise in ultrasounds that degrades fine details and limits contrast resolution. The objective of this work is propose an ultrasound despeckling method to reduce noise.

Wavelets: Optimal representation for 1D signals. The Contourlet Transform is flexible for image decomposition. Flexible multiresolution and directional decomposition, 2D frequency partition on rectangular grid, fast filter bank algorithm and tree structure.

The contourlet transform is dependent on some parameters. Use Cauchy and Maxwell distributions as priors. To estimate the parameters for the Cauchy distribution, use maximum likelihood estimation.

### Evaluation

Evaluated the despeckling algorithm on both naturally-speckled and statistically speckled images. Their method works pretty well for despeckling data. Experimental results outperform previously proposed methods on synthetically speckled images.

### Conclusion

Proposed a new scheme for despeckling of ultrasound images. Modeling the contourlet coefficients of the log-transformed ultrasound image using Cauchy distributions and the noise using Maxewell distributions.

### Links

 - [Wikipedia page for contourlets](https://en.wikipedia.org/wiki/Contourlet)
