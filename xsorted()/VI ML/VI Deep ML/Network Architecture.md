Below is a diagram of a simple Neural Network. The neurons denoted with x in the initial layer form the layer 0. The neurons denoted with y's are the output layer of the network, and their values after feeding forward are what we compare to $\hat{y}$

```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=10pt]

    % Layer 0
    \node[neuron] (I1) at (-6, 2.25) {$x_1$};
    \node[neuron] (I2) at (-6, .75) {$x_2$};
    \node[neuron] (I3) at (-6, -.75) {$x_3$};
    \node[neuron] (I4) at (-6, -2.25) {$x_4$};

    % Hidden Layer[s]
    \node[neuron] (H11) at (-3, 3) {$h_{11}$};
    \node[neuron] (H12) at (-3, 1.5) {$h_{12}$};
    \node[neuron] (H13) at (-3, 0) {$h_{13}$};
    \node[neuron] (H14) at (-3, -1.5) {$h_{14}$};
    \node[neuron] (H15) at (-3, -3) {$h_{15}$};

    \node[neuron] (H21) at (0, 3) {$h_{21}$};
    \node[neuron] (H22) at (0, 1.5) {$h_{22}$};
    \node[neuron] (H23) at (0, 0) {$h_{23}$};
    \node[neuron] (H24) at (0, -1.5) {$h_{24}$};
    \node[neuron] (H25) at (0, -3) {$h_{25}$};

    \node[neuron] (H31) at (3, 3) {$h_{31}$};
    \node[neuron] (H32) at (3, 1.5) {$h_{32}$};
    \node[neuron] (H33) at (3, 0) {$h_{33}$};
    \node[neuron] (H34) at (3, -1.5) {$h_{34}$};
    \node[neuron] (H35) at (3, -3) {$h_{35}$};
    

    % Output Layer
    \node[neuron] (O1) at (6, 1.5) {$y_1$};
    \node[neuron] (O2) at (6, 0) {$y_2$};
    \node[neuron] (O3) at (6, -1.5) {$y_3$};

    % Connect the nodes with lines
    \draw (I1) -- (H11);
    \draw (I1) -- (H12);
    \draw (I1) -- (H13);
    \draw (I1) -- (H14);
    \draw (I1) -- (H15);

    \draw (I2) -- (H11);
    \draw (I2) -- (H12);
    \draw (I2) -- (H13);
    \draw (I2) -- (H14);
    \draw (I2) -- (H15);

    \draw (I3) -- (H11);
    \draw (I3) -- (H12);
    \draw (I3) -- (H13);
    \draw (I3) -- (H14);
    \draw (I3) -- (H15);

    \draw (I4) -- (H11);
    \draw (I4) -- (H12);
    \draw (I4) -- (H13);
    \draw (I4) -- (H14);
    \draw (I4) -- (H15);
    

    \draw (H11) -- (H21);
    \draw (H11) -- (H22);
    \draw (H11) -- (H23);
    \draw (H11) -- (H24);
    \draw (H11) -- (H25);

    \draw (H12) -- (H21);
    \draw (H12) -- (H22);
    \draw (H12) -- (H23);
    \draw (H12) -- (H24);
    \draw (H12) -- (H25);

    \draw (H13) -- (H21);
    \draw (H13) -- (H22);
    \draw (H13) -- (H23);
    \draw (H13) -- (H24);
    \draw (H13) -- (H25);

    \draw (H14) -- (H21);
    \draw (H14) -- (H22);
    \draw (H14) -- (H23);
    \draw (H14) -- (H24);
    \draw (H14) -- (H25);

    \draw (H15) -- (H21);
    \draw (H15) -- (H22);
    \draw (H15) -- (H23);
    \draw (H15) -- (H24);
    \draw (H15) -- (H25);


    \draw (H21) -- (H31);
    \draw (H21) -- (H32);
    \draw (H21) -- (H33);
    \draw (H21) -- (H34);
    \draw (H21) -- (H35);

    \draw (H22) -- (H31);
    \draw (H22) -- (H32);
    \draw (H22) -- (H33);
    \draw (H22) -- (H34);
    \draw (H22) -- (H35);

    \draw (H23) -- (H31);
    \draw (H23) -- (H32);
    \draw (H23) -- (H33);
    \draw (H23) -- (H34);
    \draw (H23) -- (H35);

    \draw (H24) -- (H31);
    \draw (H24) -- (H32);
    \draw (H24) -- (H33);
    \draw (H24) -- (H34);
    \draw (H24) -- (H35);

    \draw (H25) -- (H31);
    \draw (H25) -- (H32);
    \draw (H25) -- (H33);
    \draw (H25) -- (H34);
    \draw (H25) -- (H35);


    \draw (H31) -- (O1);
    \draw (H32) -- (O1);
    \draw (H33) -- (O1);
    \draw (H34) -- (O1);
    \draw (H35) -- (O1);

    \draw (H31) -- (O2);
    \draw (H32) -- (O2);
    \draw (H33) -- (O2);
    \draw (H34) -- (O2);
    \draw (H35) -- (O2);

    \draw (H31) -- (O3);
    \draw (H32) -- (O3);
    \draw (H33) -- (O3);
    \draw (H34) -- (O3);
    \draw (H35) -- (O3);

\end{tikzpicture}
\end{document}
```

 We know what the initial layer, layer 0, receives and the final layer is output so we can see these values as well, but all layers between are Hidden Layers. This is because we never know the values, weights, biases, or any behavior or measurement of a single node, or neuron. We could determine this but it is meaningless. The model adjusts its weights and biases based off the gradient descent, which is determined with respect to each weight and bias for every weight and bias. 
 
 Manually adjusting or analyzing individual neurons defeats the concept of letting the model determine the optimal route, or configuration of weights and biases. Remember, Hyperparameters are settings we configure for the model like number of layers, layer depth, input variables, etc., while Parameters are configurations *the Model* selects and optimizes through the optimization function. Manual intervention would cripple the effectiveness of the learning technique.

Layers are denoted in many ways, but the only important thing is the notation. like pythonic indexing, the layers are indicated by their position - 1. The first layer is layer 0, the second is layer 1, etc., etc., until layer n. The network itself is n layers + the input layer. The input layer isn't considered in standard ML practice because it is essentially *the inputs themselves*. Whatever data the model is designed to be trained on dictates the layer 0's size. If we have 10 variables to train the model on, layer 0 would have 10 neurons. If we were training it on words or text, the input layer would need to be exponentially bigger.

Weights
The connection between two neurons is a weight. Each neuron of the layer $L_{i}$ is connected to every neuron of layer $L_{i+1}$ and received the outputs of every neuron in layer $L_{i-1}$. For example, the neuron denoted $h_{11}$ is connected to the neurons $h_{21}, h_{22}, h_{23}, h_{24}, \& h_{25}$ and received the outputs of $x_1, x_2, x_3, x_4, x_5$. The same is true for any given neuron of any network, except for those of the input and output layer. Therefore, weights and their shape are defined by the configuration of the network and the neurons within.

Every neuron of a single layer are connected to every neuron in the layer preceding and following it, except for layers 0 and L. This network has 5 layers of neurons, so we denote this as L=4. So, layer L would be layer 4, or the fifth layer $y$. Layer 0 is the layer of $x$'s and layers 1, 2, & 3 are Hidden Layers. This network takes four inputs and outputs 3 values.


Feed Forward
Shown below is the layer 0 and first hidden layer, or layer 1. We know $x_1$ connects to each neuron in layer 1, as well as $x_2, x_3, \& \text{ } x_4$. $x_1$ has five connections, and the same is true for $x_{2-4}$, so layer 0 has a  4 x 5 connection; 20 weights between the both of them. When data is given to the model, the first step is passing to the second layer. To get to the second layer, the values given to $x_{1-4}$ get passed to the weights matrix. The weights are multiplied against each value of $x_{1-4}$ to obtain some value which is passed to the neurons $h_{1(1-5)}$ for each value of $x_{1-4}$. 

```tikz
\begin{document}
\begin{tikzpicture}

    % Style for the nodes (neurons)
    \tikzstyle{neuron}=[circle, draw, minimum size=2mm]

    % Layer 0 (Input)
    \node[neuron] (I1) at (-0.5, 2.25) {$x_1$};
    \node[neuron] (I2) at (-0.5, 0.75) {$x_2$};
    \node[neuron] (I3) at (-0.5, -0.75) {$x_3$};
	\node[neuron] (I4) at (-0.5, -2.25) {$x_4$};

    % Hidden Layer 1
    \node[neuron] (H11) at (2, 3) {$h_{11}$};
    \node[neuron] (H12) at (2, 1.5) {$h_{12}$};
    \node[neuron] (H13) at (2, 0) {$h_{13}$};
    \node[neuron] (H14) at (2, -1.5) {$h_{14}$};
    \node[neuron] (H15) at (2, -3) {$h_{15}$};

    % --- Connect the nodes with lines ---

    % Layer 0 to Hidden 1 --- FIXED node names from H1 to H11 etc.
    \draw (I1) -- (H11); \draw (I1) -- (H12); \draw (I1) -- (H13); \draw (I1) -- (H14); \draw (I1) -- (H15);
    \draw (I2) -- (H11); \draw (I2) -- (H12); \draw (I2) -- (H13); \draw (I2) -- (H14); \draw (I2) -- (H15);
    \draw (I3) -- (H11); \draw (I3) -- (H12); \draw (I3) -- (H13); \draw (I3) -- (H14); \draw (I3) -- (H15);
    \draw (I4) -- (H11); \draw (I4) -- (H12); \draw (I4) -- (H13); \draw (I4) -- (H14); \draw (I4) -- (H15);


\end{tikzpicture}
\end{document}
```

Take the connection below. This is what our model was in the previous two TenserFlow scripts. This model, designed to find the minimum of an optimization function through gradient descent, was trained on a data set of observations in the shape of (1000,2). This data was randomly generated but set to an objective function with a linear pattern containing two variables, x & z. In this model, there are two weights and one bias. The weights are applied to each input value as it is passed to y, which outputs a value. 

```tikz
\begin{document}
\begin{tikzpicture}

    % Style for the (neurons)
    \tikzstyle{neuron}=[circle, draw, minimum size=10mm]

    % Layer 0 
    \node[neuron] (I1) at (0, 1) {$x$};
    \node[neuron] (I2) at (0, -1) {$z$};

    \node[neuron] (y) at (3, 0) {$y$};

    % --- Connect the nodes with lines ---

    \draw (I1) -- (y);
    \draw (I2) -- (y);


\end{tikzpicture}
\end{document}
```

We measure this value against the target to determine loss, which is normalized by L2-Norm in our model. The model calculate the gradient of the loss function with respect to the weights and the bias from the Loss Function. Doing so informs the model of the optimal weights and bias values to reduce the cost function for those given inputs. To throttle this, we take the returned optimal value and factor it by the learning rate. This was 0.01 for our model, but is usually generated with observations or some other activation function. Blind guy going down the mountain, you remember. 

x & z are both (1000,1) but were combined for processing, becoming the shape (1000,2). Initially, we had 1,000 pairs for our model to train on, the pairs perfectly split between each randomly generated set. This is for matrix multiplication; ML core. Having the inputs in the shape (1000,2) allows us to multiply them agains the weights matrix, or passing forward in this network. The weights matrix is (2x1); 2 weights, one for each variable. Multiplying the inputs matrix of (1000x2) by (2x1) gives us a dot product of (1000,1). There is only one layer in this network and it posses a single neuron, so there is only one bias to be added. Scalars are added Element-wise throughout matrices, meaning they are added to every element independently. (1000,1) times the (B) scalar bias results in the output of the model. Then we repeat until the gradient ceases to decrease. This is the foundation of the neural network; every node's consequent connection and signal is like one of our previous model but strung together in parallel.


```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=10pt]

    % Layer 0
    \node[neuron] (I1) at (-6, 2.25) {$x_1$};
    \node[neuron] (I2) at (-6, .75) {$x_2$};
    \node[neuron] (I3) at (-6, -.75) {$x_3$};
    \node[neuron] (I4) at (-6, -2.25) {$x_4$};

    % Hidden Layer[s]
    \node[neuron] (H11) at (-3, 3) {$h_{11}$};
    \node[neuron] (H12) at (-3, 1.5) {$h_{12}$};
    \node[neuron] (H13) at (-3, 0) {$h_{13}$};
    \node[neuron] (H14) at (-3, -1.5) {$h_{14}$};
    \node[neuron] (H15) at (-3, -3) {$h_{15}$};

    \node[neuron] (H21) at (0, 3) {$h_{21}$};
    \node[neuron] (H22) at (0, 1.5) {$h_{22}$};
    \node[neuron] (H23) at (0, 0) {$h_{23}$};
    \node[neuron] (H24) at (0, -1.5) {$h_{24}$};
    \node[neuron] (H25) at (0, -3) {$h_{25}$};

    \node[neuron] (H31) at (3, 3) {$h_{31}$};
    \node[neuron] (H32) at (3, 1.5) {$h_{32}$};
    \node[neuron] (H33) at (3, 0) {$h_{33}$};
    \node[neuron] (H34) at (3, -1.5) {$h_{34}$};
    \node[neuron] (H35) at (3, -3) {$h_{35}$};

    % Output Layer
    \node[neuron] (O1) at (6, 1.5) {$y_1$};
    \node[neuron] (O2) at (6, 0) {$y_2$};
    \node[neuron] (O3) at (6, -1.5) {$y_3$};

    % Connect the nodes with lines
    \draw (I1) -- (H11);
    \draw (I1) -- (H12);
    \draw (I1) -- (H13);
    \draw (I1) -- (H14);
    \draw (I1) -- (H15);

    \draw (I2) -- (H11);
    \draw (I2) -- (H12);
    \draw (I2) -- (H13);
    \draw (I2) -- (H14);
    \draw (I2) -- (H15);

    \draw (I3) -- (H11);
    \draw (I3) -- (H12);
    \draw (I3) -- (H13);
    \draw (I3) -- (H14);
    \draw (I3) -- (H15);

    \draw (I4) -- (H11);
    \draw (I4) -- (H12);
    \draw (I4) -- (H13);
    \draw (I4) -- (H14);
    \draw (I4) -- (H15);
    

    \draw (H11) -- (H21);
    \draw (H11) -- (H22);
    \draw (H11) -- (H23);
    \draw (H11) -- (H24);
    \draw (H11) -- (H25);

    \draw (H12) -- (H21);
    \draw (H12) -- (H22);
    \draw (H12) -- (H23);
    \draw (H12) -- (H24);
    \draw (H12) -- (H25);

    \draw (H13) -- (H21);
    \draw (H13) -- (H22);
    \draw (H13) -- (H23);
    \draw (H13) -- (H24);
    \draw (H13) -- (H25);

    \draw (H14) -- (H21);
    \draw (H14) -- (H22);
    \draw (H14) -- (H23);
    \draw (H14) -- (H24);
    \draw (H14) -- (H25);

    \draw (H15) -- (H21);
    \draw (H15) -- (H22);
    \draw (H15) -- (H23);
    \draw (H15) -- (H24);
    \draw (H15) -- (H25);


    \draw (H21) -- (H31);
    \draw (H21) -- (H32);
    \draw (H21) -- (H33);
    \draw (H21) -- (H34);
    \draw (H21) -- (H35);

    \draw (H22) -- (H31);
    \draw (H22) -- (H32);
    \draw (H22) -- (H33);
    \draw (H22) -- (H34);
    \draw (H22) -- (H35);

    \draw (H23) -- (H31);
    \draw (H23) -- (H32);
    \draw (H23) -- (H33);
    \draw (H23) -- (H34);
    \draw (H23) -- (H35);

    \draw (H24) -- (H31);
    \draw (H24) -- (H32);
    \draw (H24) -- (H33);
    \draw (H24) -- (H34);
    \draw (H24) -- (H35);

    \draw (H25) -- (H31);
    \draw (H25) -- (H32);
    \draw (H25) -- (H33);
    \draw (H25) -- (H34);
    \draw (H25) -- (H35);


    \draw (H31) -- (O1);
    \draw (H32) -- (O1);
    \draw (H33) -- (O1);
    \draw (H34) -- (O1);
    \draw (H35) -- (O1);

    \draw (H31) -- (O2);
    \draw (H32) -- (O2);
    \draw (H33) -- (O2);
    \draw (H34) -- (O2);
    \draw (H35) -- (O2);

    \draw (H31) -- (O3);
    \draw (H32) -- (O3);
    \draw (H33) -- (O3);
    \draw (H34) -- (O3);
    \draw (H35) -- (O3);

\end{tikzpicture}
\end{document}
```

Every connection above is the exact same as our miniature model. Every pair of neuron to neuron connection is an entirely independent and separate weight and bias that the model must compute the gradient of the loss function against while holding every other weight and bias constant. We know this, get on with it. Modern neural networks apply activations functions to most, if not all, layers. We did something similar with the L2-Norm calculation of the loss, but standard practice is to apply additional non-linear functions to the outputs of the weights and biases matrices. This way, the model can optimize its weights and biases to utilize these non-linear functions. In this way, a neural network can derive and predict much more complicated patterns and algorithms than a linear model could.


Activation
If we only had weights and biases between these neurons without non-linear activation functions, we'd only ever find linear models. I recommend going back to the TensorFlow model and giving it a function of $x^2$ or something. It panics and has no means to derive representation for, much less find the minimum of, a non-linear function. Modern networks utilizes non-linear functions for adjustments of weights and biases. This allows the adjustments of the weights and biases which take advantage and utilize non-linear functions. In this way, the model, or network, can derive complicated patterns and complex functions, unlike our previous model with TensorFlow. This is genius and incredible but it also means for every calculation of the gradient through the network, these non-linear activation functions must be calculated in reverse to determine the gradient of the loss with respect to the weights upstream of said activation functions. It's just hard, there's nothing else to it. 
```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=5pt]

    % Layer 0


    % Hidden Layer[s]


    \node[neuron] (H21) at (-2, 2.5) {$h_{21}$};
    \node[neuron] (H22) at (-2, 1.25) {$h_{22}$};
    \node[neuron] (H23) at (-2, 0) {$h_{23}$};
    \node[neuron] (H24) at (-2, -1.25) {$h_{24}$};
    \node[neuron] (H25) at (-2, -2.5) {$h_{25}$};

    \node[neuron] (H31) at (0, 2) {$h_{31}$};
    \node[neuron] (H32) at (0, 0.75) {$h_{32}$};
    \node[neuron] (H33) at (0, -0.75) {$h_{33}$};
    \node[neuron] (H34) at (0, -2) {$h_{34}$};

    % Output Layer
    \node[neuron] (O1) at (2, 1.5) {$y_1$};
    \node[neuron] (O2) at (2, 0) {$y_2$};
    \node[neuron] (O3) at (2, -1.5) {$y_3$};

    % Connect the nodes with lines

 



    \draw (H21) -- (H31);
    \draw (H21) -- (H32);
    \draw (H21) -- (H33);
    \draw (H21) -- (H34);
    %%\draw (H21) -- (H35);

    \draw (H22) -- (H31);
    \draw (H22) -- (H32);
    \draw (H22) -- (H33);
    \draw (H22) -- (H34);
    %%\draw (H22) -- (H35);

    \draw (H23) -- (H31);
    \draw (H23) -- (H32);
    \draw (H23) -- (H33);
    \draw (H23) -- (H34);
    %%\draw (H23) -- (H35);

    \draw (H24) -- (H31);
    \draw (H24) -- (H32);
    \draw (H24) -- (H33);
    \draw (H24) -- (H34);
    %%\draw (H24) -- (H35);

    \draw (H25) -- (H31);
    \draw (H25) -- (H32);
    \draw (H25) -- (H33);
    \draw (H25) -- (H34);
    %%\draw (H25) -- (H35);




    \draw (H31) -- (O1);
    \draw (H32) -- (O1);
    \draw (H33) -- (O1);
    \draw (H34) -- (O1);
    %%\draw (H35) -- (O1);

    \draw (H31) -- (O2);
    \draw (H32) -- (O2);
    \draw (H33) -- (O2);
    \draw (H34) -- (O2);
    %%\draw (H35) -- (O2);

    \draw (H31) -- (O3);
    \draw (H32) -- (O3);
    \draw (H33) -- (O3);
    \draw (H34) -- (O3);
    %%\draw (H35) -- (O3);

\end{tikzpicture}
\end{document}
```

This model has { 4 x 5 } + { 5 x 5 } + { 5 x 4 } + { 4 x 3 } weights, and { 5 + 5 + 4 + 3 } biases. That's 77 weights and 18 biases, only 12 weights and 3 biases can be normally configured against the gradient while the rest are forced to be calculated through those 15. Every layer is activated, so h3 has some function like the sigmoid function, although there are many others. The gradient must be found through the results of this function, as that is all that we know. The derivative of this sigmoid function $\sigma (x) = \frac{1}{1+e^{-x}}$  is  $\sigma(x)(1-\sigma(x))$.


Back Propagation
Not only must this be found for all weights and biases, the values derived for the weights protruding right from the h3 layer are calculated against the gradient, and every consequential weight and bias must be calculated from the derivative found *through that final function*. This process is called Back Propagation, and it is another core feature of modern ML architecture.

```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=5pt]

    % Layer 0


    % Hidden Layer[s]


    \node[neuron] (H21) at (-2, 2.5) {$h2_1$};
    \node[neuron] (H22) at (-2, 1.25) {$h2_2$};
    \node[neuron] (H23) at (-2, 0) {$h2_3$};
    \node[neuron] (H24) at (-2, -1.25) {$h2_4$};
    \node[neuron] (H25) at (-2, -2.5) {$h2_5$};

    \node[neuron] (H31) at (0, 2.25) {$h3_1$};
    \node[neuron] (H32) at (0, 0.75) {$h3_2$};
    \node[neuron] (H33) at (0, -0.75) {$h3_3$};
    \node[neuron] (H34) at (0, -2.25) {$h3_4$};

    % Output Layer
    \node[neuron] (O1) at (2, 1.5) {$y_1$};
    \node[neuron] (O2) at (2, 0) {$y_2$};
    \node[neuron] (O3) at (2, -1.5) {$y_3$};

    % Connect the nodes with lines

 



    \draw (H21) -- (H31);
    \draw (H21) -- (H32);
    \draw (H21) -- (H33);
    \draw (H21) -- (H34);
    %%\draw (H21) -- (H35);

    \draw (H22) -- (H31);
    \draw (H22) -- (H32);
    \draw (H22) -- (H33);
    \draw (H22) -- (H34);
    %%\draw (H22) -- (H35);

    \draw (H23) -- (H31);
    \draw (H23) -- (H32);
    \draw (H23) -- (H33);
    \draw (H23) -- (H34);
    %%\draw (H23) -- (H35);

    \draw (H24) -- (H31);
    \draw (H24) -- (H32);
    \draw (H24) -- (H33);
    \draw (H24) -- (H34);
    %%\draw (H24) -- (H35);

    \draw (H25) -- (H31);
    \draw (H25) -- (H32);
    \draw (H25) -- (H33);
    \draw (H25) -- (H34);
    %%\draw (H25) -- (H35);




    \draw (H31) -- (O1);
    \draw (H32) -- (O1);
    \draw (H33) -- (O1);
    \draw (H34) -- (O1);
    %%\draw (H35) -- (O1);

    \draw (H31) -- (O2);
    \draw (H32) -- (O2);
    \draw (H33) -- (O2);
    \draw (H34) -- (O2);
    %%\draw (H35) -- (O2);

    \draw (H31) -- (O3);
    \draw (H32) -- (O3);
    \draw (H33) -- (O3);
    \draw (H34) -- (O3);
    %%\draw (H35) -- (O3);

\end{tikzpicture}
\end{document}
```

Back Propagating through the network allows the computation of the gradient descent with respect to each weight be determined with proportionality of its affect on the output. For example, we need to find the adjustments for the weight that protrudes from the h2_1 neuron and goes through the h3_1 neuron to y_1, we'd calculate the gradient for the weight from h3_1 to y_1, and use this value to compute the value we had at h3_1, which we find a new gradient for and use to adjust the h2_1 neuron. This is key as since we found the h2_1 weight through the gradient of the h3_1 weight, we found the h2_1 weight's relative impact on the cost function. 

Since whatever value and function h2_1 is configured to use, the output is still then affected by another weight from the h3 layer's weights. This means whatever information it was trying to pass along was affect by the weight matrix of the consecutive layer, changing the message, so h2_1's message was proportionally distorted by a scale of h3's weight matrix, so it must be judged and adjusted as such.