# Adaptive-Activations

University of Edinburgh Undergraduate Dissertation. Created and implemented novel parametrisation of Activation Functions on various Neural Network architectures to study the nature of Deep Learning

# Single Hidden-Layer Perceptrons and Neural Networks

Somewhat of a misnomer, the Single Hidden-Layer Perceptron (SHLP) doesn't really have much to do with the classical Perceptron algorithm that's used to classify linearly separable data. SHLP refers to Neural Network architectures that distinctly have the property of only implementing a Single Hidden-Layer. The choice for this isn't arbitrary, but based on the Universal Approximation Theorem, which generally states that Artificial Neural Networks only need a single Hidden-Layer (alongside the Input and Output layer) in order to approximate any continuous function within an interval. Hence the SHLP architectures investigated within this project wouldn't be considered conventional Deep Learning, since the approximation power comes not from the "depth" but rather the "width" and the number of neurons that make up the Hidden-Layer itself. Three main architectures are studied:

## 1. Feedforward Networks

This is the most basic form of the SHLP considered. The binary classification problem on planar data provides context to train the following architecture

$$\hat{y}(\bm{x}) = \sigma(W_2 \;\text{ReLU}(W_1 \; {x} + b_1) + b_2) $$

where the typical ReLU and Sigmoid functions are implemented on the hidden and output layers respectively.  
