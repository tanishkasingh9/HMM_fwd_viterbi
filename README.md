# Run Forward Backward and Viterbi Algorithms on defined HMM

## Why have such a model?
Usually the data points we encounter in datasets like MNIST, PASCAL etc are assumed to independent and identically distributed. This allows us to apply likelihood function across the data points to model probability distribution. But there are examples of data instances for which making this assumption would clearly be wrong, more specifically time series data points. Time series data is sequential in nature and not all examples of sequential data are time series, some examples for this kind of dataset are accoustic features in speech, sequence of characters, sequence of nucleotide base pairs in a DNA strand etc. 

## Overview of Markov Models
To exploit the sequential patterns that occur in the data, we need a way to model the correlations between the observations. Markov models use the product rule to express the joint distribution for a sequence of observations, 
<br>
<img src="https://render.githubusercontent.com/render/math?math=P(x_1, x_2, ..., x_n) = \Pi^n_{i=2} \ p(x_i | x_1,..., x_i-1) " width="200" >

The program contains following steps to run the above algorithms:
1. 

Cheers!

## References 

