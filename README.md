# Run Forward Backward and Viterbi Algorithms on defined HMM

## Why have such a model?
Usually the data points we encounter in datasets like MNIST, PASCAL etc are assumed to independent and identically distributed. This allows us to apply likelihood function across the data points to model probability distribution. But there are examples of data instances for which making this assumption would clearly be wrong, more specifically time series data points. Time series data is sequential in nature and not all examples of sequential data are time series, some examples for this kind of dataset are accoustic features in speech, sequence of characters, sequence of nucleotide base pairs in a DNA strand etc. 

## Overview of Markov Models
To exploit the sequential patterns that occur in the data, we need a way to model the correlations between the observations. Markov models use the product rule to express the joint distribution for a sequence of observations, 
<br>
<p align= "center">
<img src="https://render.githubusercontent.com/render/math?math=P(x_1, x_2, ..., x_n) = \Pi^n_{i=2} \ p(x_i\ |\ x_1,..., x_{i-1}) " height="30">
</p>
Assuming that the current observation only depends on the previous observation, a <i>first-order Markov Chain</i>, and using <i>d-separation property</i> to reduce the above equation we get, 
<br>
<p align= "center">
<img src="https://render.githubusercontent.com/render/math?math=P(x_1, x_2, ..., x_n) = p(x_1) \Pi^n_{i=2} p(x_i\ |\ x_{i-1}) " height="30">
</p>
We can also create higher orders of markov models in a similar manner.

## Overview of Hidden Markov Model 
Hidden Markov Models(HMM) are an extension of a mixture model, where there are various discrete multinomial latent variables that could be responsible for generating a particular observation in a sequence. The choice of picking a mixture component or hidden state for a particular observation depends on the choice of component for the previous observation. The transition probabilities are used to define this transition from previous hidden state to the current hidden state based on the observation denoted by A, using the conditional distribution of the observed variables <img src="https://render.githubusercontent.com/render/math?math=p(x_n|z_n,\phi)"> 
The program contains following steps to run the above algorithms:
1. 

Cheers!

## References 

