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
Hidden Markov Models (HMM) are an extension of a mixture model, where there are various discrete multinomial latent variables that could be responsible for generating a particular observation in a sequence. The choice of picking a mixture component or hidden state for a particular observation depends on the choice of component for the previous observation. The transition probabilities are defined by this transition from previous hidden state to the current hidden state based on the observation denoted by A, and emission probabilities are defined by the conditional distribution of the observed variables <img src="https://render.githubusercontent.com/render/math?math=p(x_n|z_n,\phi)"> for each latent variable denoted by B. HMMs in general are not susceptible to local warping and variability in generations, making it an excellent choice for speech recognition, handwriting generation etc. 

### Forward Backward (Baum-Welch) Algorithm 
This algorithm capable of determining the probability of emitting a sequence of observation given the parameters (z,x,A,B) of a HMM, using a two stage message passing system. It is used when we know the sequence of observation but don't know the sequence of hidden states that generates the sequence of observation in question. Let us represent the sequence of observation with X and parameters using theta,

<p align= "center">
<img src="https://render.githubusercontent.com/render/math?math=P(X^T\ |\ \theta) = \Sigma_{n^T}\ p(X^T, Z^T)" height="30">
</p>
The time complexity of calculating the posterior with just one pass will be <img src="https://render.githubusercontent.com/render/math?math=O(n^T.T)"> 
<br>
For a given sequence of T observations. The complexity can be reduced by calculating the following, 
<p align= "center">
<img src="https://render.githubusercontent.com/render/math?math=\alpha_j(t) = p(x_1,....x_t, z_t = j)" height="30">
  <br>
<img src="https://render.githubusercontent.com/render/math?math=\alpha_j(t%2B1) = b_{jk}(x_{t%2B1}) \Sigma^n_{i=1} \ a_{ij}\alpha_i(t)" height="30">  
</p>
After completing this step, we backtrack through our trellis using the following function, 
<p align= "center">
<a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;\beta_i(t)&space;=&space;\begin{Bmatrix}&space;1&space;&&space;when\&space;t=T\\&space;\sum_{j=0}^{n}&space;a_{ij}&space;b_{jk}(x_{t&plus;1})\beta_{j}(t&plus;1)&space;&&space;when\&space;t<T&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\large&space;\beta_i(t)&space;=&space;\begin{Bmatrix}&space;1&space;&&space;when\&space;t=T\\&space;\sum_{j=0}^{n}&space;a_{ij}&space;b_{jk}(x_{t&plus;1})\beta_{j}(t&plus;1)&space;&&space;when\&space;t<T&space;\end{Bmatrix}" title="\large \beta_i(t) = \begin{Bmatrix} 1 & when\ t=T\\ \sum_{j=0}^{n} a_{ij} b_{jk}(x_{t+1})\beta_{j}(t+1) & when\ t<T \end{Bmatrix}" /></a>
</p>
The program contains following steps to run the above algorithms:
1. 

Cheers!

## References 

