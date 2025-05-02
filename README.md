# Adaptive-Activations

University of Edinburgh Undergraduate Dissertation. Created and implemented novel parametrisation of Activation Functions on various Neural Network architectures to study the nature of Deep Learning

# Single Hidden-Layer Perceptrons and Neural Networks

Somewhat of a misnomer, the Single Hidden-Layer Perceptron (SHLP) doesn't really have much to do with the classical Perceptron algorithm that's used to classify linearly separable data. SHLP refers to Neural Network architectures that distinctly have the property of only implementing a Single Hidden-Layer. The choice for this isn't arbitrary, but based on the Universal Approximation Theorem, which generally states that Artificial Neural Networks only need a single Hidden-Layer (alongside the Input and Output layer) in order to approximate any continuous function within an interval. Hence the SHLP architectures investigated within this project wouldn't be considered conventional Deep Learning, since the approximation power comes not from the "depth" but rather the "width" and the number of neurons that make up the Hidden-Layer itself. Three main architectures are studied:

## 1. Feedforward Networks

This is the most basic form of the SHLP considered. The binary classification problem on planar data provides context to train the following architecture

$$\hat{y}({x}) = \sigma(W_2 \times \text{ReLU}(W_1 \times {x} + b_1) + b_2) $$

where the typical ReLU and Sigmoid functions are implemented on the hidden and output layers respectively.  

## 2. Convolutional Networks

![conv](https://github.com/user-attachments/assets/2cd5a51d-2a78-4478-9915-a1006e512a57)

A simple CNN is used to classify MNIST image data. The SHLP architecture implemented is fairly straightforward, with the inputs feeding into a Convolutional ReLU Layer, after which there is Pooling. Following that there is a single Dense Fully-Connect ReLU Hidden-Layer, with the Softmax output layer for the corresponding 10 classes. 

## 3. Recurrent Networks

In particular a network with a single hidden LSTM Layer and a feedforward output layer. This is trained and validated on intervals of artificial stock-price data. The results regarding this network within the Thesis are fairly preliminary but promising. 

# Adaptive Activation Functions

Universal Approximation allows us to control for the depth of the network architectures and set the number of hidden-layers to 1 so fairly simple datasets (with minimal features needed for hierarchical representation) are chosen. Each hidden-layer neuron is observed in isolation representing a specific feature of the data, while the Activation Function implemented can be specifically seen to take the shape of the feature learnt. The main contribution of the project is to fundamentally understand the effect of the shape of the Activation functions implemented, beyond that of simply adding a functional non-linearity to the network. Both the Sigmoid and Softmax outputs normalize values onto a probability distribution across the classes, but the choice of the ReLU function seem somewhat arbitrary, as evidenced by it's various drawbacks and the existence of the many ReLU-variants intending to solve said problems. The innovation introduced in this project is to construct Adaptive Activations which shapes can be learned and trained as parameters similarly to the Weights and Biases. 

![SReLU diff eps](https://github.com/user-attachments/assets/a37bcaa8-61fe-4e6b-b394-536996363148)

$$
  f(x) =
  \begin{cases}
  \frac{1}{4\varepsilon} x^{2}+ \frac{1}{2}x + \frac{\varepsilon}{4} & \text{for $|x| < \varepsilon$} \\
  max(0,x) & \text{otherwise}.
  \end{cases}
$$

As an example, the ReLU is smoothed as an attempt to prevent dying ReLU-neurons. The motivation for parametrising it with a smooth interval is twofold; altering the shape of the passing of information in the form of learnt parameters as well as it potentially being a parameter itself of which the output is a function. 

Further, another Adaptive ReLU-variant is studied: $
 Swish(x) =
  \begin{cases}
 max(0,x) & \text{as $\alpha \xrightarrow{} \infty$} \\
  \frac{x}{1+e^{-\alpha x}} & \text{otherwise}.
  \end{cases}$ 

  For each Adaptive Activation, the additional variables ($\varepsilon$ and $\alpha$) are updated with each training iteration similarly to the other learned parameters by integrating the respective derivatives (wrt to the variables) into the backpropagation architecture of the SHLP networks. On the Feedforward Network, adaptivity is implemented onto the hidden-layer ReLU-neurons, while on the Convolutional Model, this is done on the Convolutional ReLU layer. For the LSTM, the Sigmoid and Tanh functions are adapted to increase the efficacy of the Forget gate and the capacity for Long-term memory. 

$$Ad-\sigma (x) = \dfrac{1}{1+e^{-\beta x}}                                  Ad-tanh (x) = \dfrac{e^{\beta x} - e^{-\beta x}}{e^{\beta x}+e^{-\beta x}}$$

