Below is a diagram of a simple Neural Network. The neurons denoted with x in the initial layer form the layer 0. The neurons denoted with y's are the output layer of the network, and their values after feeding forward are what we compare to $\hat{y}$

 We know what the initial layer, layer 0, receives and the final layer is output so we can see these values as well, but all layers between are Hidden Layers. This is because we never know the values, weights, biases, or any behavior or measurement of a single node, or neuron. We could determine this but it is meaningless. The model adjusts its weights and biases based off the gradient descent, which is determined with respect to each weight and bias for every weight and bias. 
 
 Manually adjusting or analyzing individual neurons defeats the concept of letting the model determine the optimal route, or configuration of weights and biases. Remember, Hyperparameters are settings we configure for the model like number of layers, layer depth, input variables, etc., while Parameters are configurations *the Model* selects and optimizes through the optimization function. Manual intervention would cripple the effectiveness of the learning technique.

Layers are denoted in many ways, but the only important thing is the notation. like pythonic indexing, the layers are indicated by their position - 1. The first layer is layer 0, the second is layer 1, etc., etc., until layer n. The network itself is n layers + the input layer. The input layer isn't considered in standard ML practice because it is essentially *the inputs themselves*. Whatever data the model is designed to be trained on dictates the layer 0's size. If we have 10 variables to train the model on, layer 0 would have 10 neurons. If we were training it on words or text, the input layer would need to be exponentially bigger.

The connection between two neurons is a weight. Each neuron of the layer $L_{i}$ is connected to every neuron of layer $L_{i+1}$ and received the outputs of every neuron in layer $L_{i-1}$. For example, the neuron denoted $h1_1$ is connected to the neurons $h2_1, h2_2, h2_3, h2_4, \& h2_5$ and received the outputs of $x_1, x_2, x_3, x_4, x_5$. The same is true for any given neuron of any network, except for those of the input and output layer. 

Every neuron of a single layer are connected to every neuron in the layer preceding and following it. 



```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=10pt]

    % Layer 0
    \node[neuron] (I1) at (-5, 1.5) {$x_1$};
    \node[neuron] (I2) at (-5, 0.5) {$x_2$};
    \node[neuron] (I3) at (-5, -0.5) {$x_3$};
    \node[neuron] (I4) at (-5, -1.5) {$x_4$};

    % Hidden Layer[s]
    \node[neuron] (H11) at (-1.5, 1.5) {$h1_1$};
    \node[neuron] (H12) at (-1.5, 0.5) {$h1_2$};
    \node[neuron] (H13) at (-1.5, -0.5) {$h1_3$};
    \node[neuron] (H14) at (-1.5, -1.5) {$h1_4$};
    \node[neuron] (H15) at (-1.5, -2.5) {$h1_5$};

    \node[neuron] (H21) at (1.5, 1.5) {$h2_1$};
    \node[neuron] (H22) at (1.5, 0.5) {$h2_2$};
    \node[neuron] (H23) at (1.5, -0.5) {$h2_3$};
    \node[neuron] (H24) at (1.5, -1.5) {$h2_4$};
    \node[neuron] (H25) at (1.5, -2.5) {$h2_5$};

    \node[neuron] (H31) at (4.5, 1.5) {$h3_1$};
    \node[neuron] (H32) at (4.5, 0.5) {$h3_2$};
    \node[neuron] (H33) at (4.5, -0.5) {$h3_3$};
    \node[neuron] (H34) at (4.5, -1.5) {$h3_4$};

    % Output Layer
    \node[neuron] (O1) at (5.5, 1) {$y_1$};
    \node[neuron] (O2) at (5.5, 0) {$y_2$};
    \node[neuron] (O3) at (5.5, -1) {$y_3$};

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
