Previously, we made a linear model with a single layer and two variables
	the model only had the means to explain linear relationships
		it had multiple inputs, but it optimized each through linear functions

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

*This is a visual representation of the model we defined and trained in V Linear Networks, Tensors*

an example of a  non-linear function ; [ Sigmoid Function ]$$\text{Sigmoid} = \sigma (x) = \frac{1}{1+\epsilon^{-x}}$$ The graphical representation of the Sigmoid function is
```tikz
\begin{document}
\begin{tikzpicture}[xscale=2,yscale=4]
    % --- Draw Grid ---
    % Grid now goes from bottom-left (-4,-0.2) to top-right (4,1.2)
    \draw[step=1cm, gray, very thin] (-4,-0.2) grid (4,1.2);

    % --- Draw Axes ---
    \draw[->, thick] (-4,0) -- (4,0) node[right] {$x$};
    \draw[->, thick] (0,-0.2) -- (0,1.2) node[above] {$S(x)$};

    % --- Add Ticks and Labels ---
    \draw (0,1) -- (-0.1,1) node[left] {1};
    \foreach \x in {-3,-2,-1,1,2,3}
        \draw (\x,0) -- (\x,-0.05) node[below] {\x};

    % --- Plot the Sigmoid Function ---
    \draw[blue, thick, smooth, samples=100, domain=-4:4]
        plot (\x, {1/(1+exp(-\x))});
\end{tikzpicture}
\end{document}
```

The leap between models like the one we configured and Deep Networks are the activation functions
	Activation Functions are non-linear, usually normalizing functions applied to layers of a network
			When a non-linear function is applied, the model's optimization function can utilize these non-linear results to derive non-linear patterns and discover more complex subtleties than a linear model
					This combination of linear and non-linear modeling allows for more dynamic learning than strictly linear or non-linear functions

A [ Neural Network ]

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

Networks are usually considered by layer
	the input layer is the layer of x's and the output layer is the layer of y's
		neural nets are designed off of the idea of giving inputs and receiving outputs ; like our model
			the input layer, or layer 0, input data for and ' feeds it forward ' to the next layer
				This process is done through the weights matrix, so to get the values given to layer 0 to layer 1, the first hidden layer, they must be weighted

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
    \draw (I1) -- (H11); \draw (I1) -- (H12); \draw (I1) -- (H13); \draw (I1) -- (H14); \draw (I1) -- (H15);
    \draw (I2) -- (H11); \draw (I2) -- (H12); \draw (I2) -- (H13); \draw (I2) -- (H14); \draw (I2) -- (H15);
    \draw (I3) -- (H11); \draw (I3) -- (H12); \draw (I3) -- (H13); \draw (I3) -- (H14); \draw (I3) -- (H15);
    \draw (I4) -- (H11); \draw (I4) -- (H12); \draw (I4) -- (H13); \draw (I4) -- (H14); \draw (I4) -- (H15);


\end{tikzpicture}
\end{document}
```
.
	Consider we are using this model and examining only the first two layers, layers 0 and 1
		the network is given 4 pieces of data which must be passed to 5 neurons
			let's say our dataset is 1000 observations ; our training data would be in the shape of 1000 rows and 4 columns. 
				layer 0 is called such because it is essentially non-existent ; when we give data to the model the initial layer only acts as an interpreter for the network to input the information
				The real power of the network is when we feed the data past layer 0 to the weights
					layer 0 has four neurons and layer 1 has 5, so we need one weight for every neuron in layer 1 for every neuron in layer 0 ; [ 4 x 5 ]
						the obvious shortcut for this operation is matrices !
							the input data is shape 1000x4 and the weights are shape 4x5, so the dot product of a 1000x4 matrix and a 4x5 matrix is 1000x5, the shape of layer 1!
										*this is one linear transformation ^ ; adding an activation function makes it non-linear, but solely multiplying weights by inputs is purely linear*
							Next, every neuron { except those in layer 0 } have a bias which is added to the value derived from the weights matrices' dot product 
							This results in values for each neuron in layer 1, derived from the input data and modified by the weights and biases
								This process is completed when the values are passed through the network and output of the final layer which we compare to the targets to compute loss
										This is Feeding Forward
.
		*Consider this as a whole. The weights and biases are random values which initially are irrelevant. the model feeds forward through the net and produces a prediction, which is compared to the targets for loss. With loss, we compute the gradient of said cost function to determine the optimal position for every weight and bias in the network. Then, the process is repeated until the cost function diminishes or ceases to decrease. It is nearly identical to our model in terms of functionality, it is just scaled exponentially and carries non-linear activation functions*
.
	*Additionally, these activation functions are applied to the outputs of layers when their weights are applied and biases are added. In the case above, the values derived for layer 1, or h1, would be processed through an activation function before they were fed to the next layer. This is the power behind Deep Networks but also the bottleneck of their size, as the cost gradient must be determined through such functions.*