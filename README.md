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
The time complexity of calculating the posterior with just one pass will be <a href="https://www.codecogs.com/eqnedit.php?latex=\small&space;O(n^TT)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\small&space;O(n^TT)" title="\small O(n^TT)" /></a> for a given sequence of T observations. The complexity can be reduced to <a href="https://www.codecogs.com/eqnedit.php?latex=\small&space;O(n^2T)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\small&space;O(n^2T)" title="\small O(n^2T)" /></a>, using dynamic programming, 
<p align= "center">
<img src="https://render.githubusercontent.com/render/math?math=\alpha_j(t) = p(x_1,....x_t, z_t = j)" height="30">
  <br>
<img src="https://render.githubusercontent.com/render/math?math=\alpha_j(t%2B1) = b_{jk}(x_{t%2B1}) \Sigma^n_{i=1} \ a_{ij}\alpha_i(t)" height="30">  
</p>
After completing this step, we backtrack through our trellis using the following function, 
<p align= "center">
<a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;\beta_i(t)&space;=&space;\begin{Bmatrix}&space;1&space;&&space;when\&space;t=T\\&space;\sum_{j=0}^{n}&space;a_{ij}&space;b_{jk}(x_{t&plus;1})\beta_{j}(t&plus;1)&space;&&space;when\&space;t<T&space;\end{Bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\large&space;\beta_i(t)&space;=&space;\begin{Bmatrix}&space;1&space;&&space;when\&space;t=T\\&space;\sum_{j=0}^{n}&space;a_{ij}&space;b_{jk}(x_{t&plus;1})\beta_{j}(t&plus;1)&space;&&space;when\&space;t<T&space;\end{Bmatrix}" title="\large \beta_i(t) = \begin{Bmatrix} 1 & when\ t=T\\ \sum_{j=0}^{n} a_{ij} b_{jk}(x_{t+1})\beta_{j}(t+1) & when\ t<T \end{Bmatrix}" /></a>
</p>

### Viterbi Algorithm
For finding the most probable sequence of hidden states, we use max-sum algorithm known as Viterbi algorithm for HMMs. It searches the space of paths (possible sequences) efficiently with a computational cost that grows linearly with the length of chain. We again use the variables z to represent the hidden states, x to represent the observed sequence, n as the number of hidden states, and T as the length of the observed sequence. Our objective is to find the states that maximize the conditional proabbility of states given sequence of observation, 
<br>

<p align= "center">
  <a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;Z^*_{0:T}&space;=&space;argmax_{Z_{0:T}}&space;P(Z_{0:T}&space;|&space;X_{0:T})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\large&space;Z^*_{0:T}&space;=&space;argmax_{Z_{0:T}}&space;P(Z_{0:T}&space;|&space;X_{0:T})" title="\large Z^*_{0:T} = argmax_{Z_{0:T}} P(Z_{0:T} | X_{0:T})" /></a>
</p>

This can again be solved by the means of dynamic programming, as the current state in a HMM only depends on the previous state. We define a function to represent the maximum joint probability of getting an intermediate observation of the sequence and hidden state as follows:
<p align= "center">
<a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;\mu(Z_i)&space;=&space;max_{Z_{0:i-1}}&space;P(Z_{0:i},&space;X_{0:i})\\&space;\mu(Z_i)&space;=&space;max_{Z_{i-1}}&space;\mu(Z_{i-1})P(Z_i|Z_{i-1})P(X_i|Z_i)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\large&space;\mu(Z_i)&space;=&space;max_{Z_{0:i-1}}&space;P(Z_{0:i},&space;X_{0:i})\\&space;\mu(Z_i)&space;=&space;max_{Z_{i-1}}&space;\mu(Z_{i-1})P(Z_i|Z_{i-1})P(X_i|Z_i)" title="\large \mu(Z_i) = max_{Z_{0:i-1}} P(Z_{0:i}, X_{0:i})\\ \mu(Z_i) = max_{Z_{i-1}} \mu(Z_{i-1})P(Z_i|Z_{i-1})P(X_i|Z_i)" /></a>
</p>
We can see from the final formula that the last two probability terms are nothing but the transition probability and the emission probabilities. The runtime complexity comes down to be <a href="https://www.codecogs.com/eqnedit.php?latex=\small&space;O(n^2T)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\small&space;O(n^2T)" title="\small O(n^2T)" /></a> using dynamic algorithm. 

## References 
1.  Rabiner LR (February 1989). "A tutorial on hidden Markov models and selected applications in speech recognition". Proceedings of the IEEE. 77 (2): 257–286. CiteSeerX 10.1.1.381.3454. doi:10.1109/5.18626. (Describes the forward algorithm and Viterbi algorithm for HMMs).
2.  Blasiak, S.; Rangwala, H. (2011). "A Hidden Markov Model Variant for Sequence Classification". IJCAI Proceedings-International Joint Conference on Artificial Intelligence.
3.  Christopher M. Bishop "Pattern Classification and Machine Learning" 13.2 
