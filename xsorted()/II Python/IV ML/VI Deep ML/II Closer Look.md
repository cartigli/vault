Inside the Network
```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=5pt, inner sep=2pt]

    % Hidden Layer[s]
    \node[neuron] (x1) at (-2, 1) {$x_{1}$};
    \node[neuron] (x2) at (-2, 0) {$x_{2}$};
    \node[neuron] (x3) at (-2, -1) {$x_{3}$};
    \node[neuron] (x4) at (-2, -2) {$x_{4}$};

    \node[neuron] (H1) at (0, 1.5) {$h_{1}$};
    \node[neuron] (H2) at (0, 0.5) {$h_{2}$};
    \node[neuron] (H3) at (0, -0.5) {$h_{3}$};
    \node[neuron] (H4) at (0, -1.5) {$h_{4}$};
    \node[neuron] (H5) at (0, -2.5) {$h_{5}$};

    % Output Layer
    \node[neuron] (y1) at (2, 0.5) {$y_1$};
    \node[neuron] (y2) at (2, -0.5) {$y_2$};
    \node[neuron] (y3) at (2, -1.5) {$y_3$};

    % Connect the nodes with lines
    \draw (x1) -- (H1);
    \draw (x1) -- (H2);
    \draw (x1) -- (H3);
    \draw (x1) -- (H4);
    \draw (x1) -- (H5);

    \draw (x2) -- (H1);
    \draw (x2) -- (H2);
    \draw (x2) -- (H3);
    \draw (x2) -- (H4);
    \draw (x2) -- (H5);

    \draw (x3) -- (H1);
    \draw (x3) -- (H2);
    \draw (x3) -- (H3);
    \draw (x3) -- (H4);
    \draw (x3) -- (H5);

    \draw (x4) -- (H1);
    \draw (x4) -- (H2);
    \draw (x4) -- (H3);
    \draw (x4) -- (H4);
    \draw (x4) -- (H5);

    \draw (H1) -- (y1);
    \draw (H2) -- (y1);
    \draw (H3) -- (y1);
    \draw (H4) -- (y1);
    \draw (H5) -- (y1);

    \draw (H1) -- (y2);
    \draw (H2) -- (y2);
    \draw (H3) -- (y2);
    \draw (H4) -- (y2);
    \draw (H5) -- (y2);

    \draw (H1) -- (y3);
    \draw (H2) -- (y3);
    \draw (H3) -- (y3);
    \draw (H4) -- (y3);
    \draw (H5) -- (y3);

\end{tikzpicture}
\end{document}
```

This network has 5 inputs and an initial weight matrix of 4 x 5 weights to feed forward to layer h1 of 5 neurons. We'll call this weight matrix $w_1$. To get from the results of $w_1$ to the output layer, the results must be multiplied again by the matrix $w_2$ between h1 and y. 
	So, $x \cdot w_1 = h\text{, and } h \cdot w_2 = y$.
		This algebraic expression can be simplified by substituting h for $x \cdot w_1$
				leaving $y = x \cdot w_1 \cdot w_2$ 
					but** the matrices for the weights are shapes $4 \cdot 5$ and $5 \cdot 3$, so they can be combined
						combining the weight matrices of $w_1 \text{ } \& \text{ } w_2$ gives us $w^*$ ; shape $4 \cdot 3$ 
							This leaves $y = x \cdot w^*$ -- a linear model, eliminating the need for a hidden layer and reverting the model's abilities to linear functions only
										*the two consecutive linear transformations are equal to one linear transformation*
								Neural Networks apply activation functions to the outputs of these weight matrices to derive non-linear patterns from linear combinators

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

Our model used a linear transformation to derive linear patterns through the objective function. Neural Networks have the same basic architecture but with small twist.

```tikz
\begin{document}
\begin{tikzpicture}

    % Style for the (neurons)
    \tikzstyle{neuron}=[circle, draw, minimum size=10mm]
    \tikzstyle{fx}=[rectangle, draw, minimum size=10mm]

    % Layer 0 
    \node[neuron] (I1) at (0, 1) {$x$};
    \node[neuron] (I2) at (0, -1) {$z$};

    \node[neuron] (y) at (3, 0) {$y$};

	\node[fx] (Sigmoid) at (5,0) {$Sigmoid$};

    % --- Connect the nodes with lines ---
    \draw (I1) -- (y);
    \draw (I2) -- (y);

    \draw [red] (y) -- (Sigmoid);


\end{tikzpicture}
\end{document}
```

Applying the Sigmoid function here allows the non-linear transformation to take place, enabling prediction of non-linear functions. This is the magic behind Neural Networks.

```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=5pt, inner sep=2pt]
    \tikzstyle{fx}=[rectangle, draw, minimum size=2mm, inner sep=2pt]

    % Hidden Layer[s]
    \node[neuron] (x1) at (-6, 1) {$x_{1}$};
    \node[neuron] (x2) at (-6, 0) {$x_{2}$};
    \node[neuron] (x3) at (-6, -1) {$x_{3}$};
    \node[neuron] (x4) at (-6, -2) {$x_{4}$};

    \node[neuron] (H1) at (-2, 1.5) {$h_{1}$};
    \node[neuron] (H2) at (-2, 0.5) {$h_{2}$};
    \node[neuron] (H3) at (-2, -0.5) {$h_{3}$};
    \node[neuron] (H4) at (-2, -1.5) {$h_{4}$};
    \node[neuron] (H5) at (-2, -2.5) {$h_{5}$};

    % Output Layer
    \node[neuron] (y1) at (2, 0.5) {$y_1$};
    \node[neuron] (y2) at (2, -0.5) {$y_2$};
    \node[neuron] (y3) at (2, -1.5) {$y_3$};

	\node[fx] (Sx1) at (-4.75, 1) {$Sigmoid$};
	\node[fx] (Sx2) at (-4.75, 0) {$Sigmoid$};
	\node[fx] (Sx3) at (-4.75, -1) {$Sigmoid$};
	\node[fx] (Sx4) at (-4.75, -2) {$Sigmoid$};

	\node[fx] (Sh1) at (-0.75, 1.5) {$Sigmoid$};
	\node[fx] (Sh2) at (-0.75, 0.5) {$Sigmoid$};
	\node[fx] (Sh3) at (-0.75, -0.5) {$Sigmoid$};
	\node[fx] (Sh4) at (-0.75, -1.5) {$Sigmoid$};
	\node[fx] (Sh5) at (-0.75, -2.5) {$Sigmoid$};

	\node[fx] (Sy1) at (3.25, 0.5) {$SoftMax$};
	\node[fx] (Sy2) at (3.25, -0.5) {$SoftMax$};
	\node[fx] (Sy3) at (3.25, -1.5) {$SoftMax$};

	\node[fx] (o1) at (5, 0.5) {$Output$};
	\node[fx] (o2) at (5, -0.5) {$Output$};
	\node[fx] (o3) at (5, -1.5) {$Output$};

    % Connect the nodes with lines
    \draw (x1) -- (Sx1);
    \draw (x2) -- (Sx2);
    \draw (x3) -- (Sx3);
    \draw (x4) -- (Sx4);


	\draw (Sx1) -- (H1);
    \draw (Sx1) -- (H2);
    \draw (Sx1) -- (H3);
    \draw (Sx1) -- (H4);
    \draw (Sx1) -- (H5);

    \draw (Sx2) -- (H1);
    \draw (Sx2) -- (H2);
    \draw (Sx2) -- (H3);
    \draw (Sx2) -- (H4);
    \draw (Sx2) -- (H5);

    \draw (Sx3) -- (H1);
    \draw (Sx3) -- (H2);
    \draw (Sx3) -- (H3);
    \draw (Sx3) -- (H4);
    \draw (Sx3) -- (H5);

    \draw (Sx4) -- (H1);
    \draw (Sx4) -- (H2);
    \draw (Sx4) -- (H3);
    \draw (Sx4) -- (H4);
    \draw (Sx4) -- (H5);


    \draw (H1) -- (Sh1);
    \draw (H2) -- (Sh2);
    \draw (H3) -- (Sh3);
    \draw (H4) -- (Sh4);
    \draw (H5) -- (Sh5);


    \draw (Sh1) -- (y1);
    \draw (Sh2) -- (y1);
    \draw (Sh3) -- (y1);
    \draw (Sh4) -- (y1);
    \draw (Sh5) -- (y1);

    \draw (Sh1) -- (y2);
    \draw (Sh2) -- (y2);
    \draw (Sh3) -- (y2);
    \draw (Sh4) -- (y2);
    \draw (Sh5) -- (y2);

    \draw (Sh1) -- (y3);
    \draw (Sh2) -- (y3);
    \draw (Sh3) -- (y3);
    \draw (Sh4) -- (y3);
    \draw (Sh5) -- (y3);


    \draw (y1) -- (Sy1);
    \draw (y2) -- (Sy2);
    \draw (y3) -- (Sy3);

    \draw (Sy1) -- (o1);
    \draw (Sy2) -- (o2);
    \draw (Sy3) -- (o3);


\end{tikzpicture}
\end{document}
```