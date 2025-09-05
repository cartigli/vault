```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=5pt, inner sep=2pt]

    % Hidden Layer[s]
    \node[neuron] (H21) at (-2, 1) {$x_{1}$};
    \node[neuron] (H22) at (-2, 0) {$x_{2}$};
    \node[neuron] (H23) at (-2, -1) {$x_{3}$};
    \node[neuron] (H24) at (-2, -2) {$x_{4}$};

    \node[neuron] (H31) at (0, 1.5) {$h_{11}$};
    \node[neuron] (H32) at (0, 0.5) {$h_{12}$};
    \node[neuron] (H33) at (0, -0.5) {$h_{13}$};
    \node[neuron] (H34) at (0, -1.5) {$h_{14}$};
    \node[neuron] (H35) at (0, -2.5) {$h_{15}$};

    % Output Layer
    \node[neuron] (O1) at (2, 0.5) {$y_1$};
    \node[neuron] (O2) at (2, -0.5) {$y_2$};
    \node[neuron] (O3) at (2, -1.5) {$y_3$};

    % Connect the nodes with lines
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

This network has 5 inputs and an initial weight matrix of 4 x 5 weights to feed forward to layer h1 of 5 neurons. We'll call this weight matrix $w_1$. To get from the results of $w_1$ to the output layer, the results must be multiplied again by the matrix $w_2$ between h1 and y. 
	So, x * $w_1$ = h, and h * $w_2$ = y.
		This algebraic expression can be simplified by substituting h for x * $w_1$
				leaving y = x * $w_1$ * $w_2$ 
					but** the matrices for the weights are shapes 4 x 5 and 5 x 3, so they can be combined
						combining the weight matrices of $w_1 \text{ } \& \text{ } w_2$ gives us $w^*$ ; shape 4 x 3 
							This leaves y = x * $w^*$ -- a linear model, eliminating the need for a hidden layer and reverting the model's abilities to linear functions only
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

    \draw (y) -- (Sigmoid);


\end{tikzpicture}
\end{document}
```

Applying the Sigmoid function here allows the non-linear transformation to take place, enabling prediction of non-linear functions. This is the magic behind Neural Networks.




```tikz
% Preamble of your .tex file
\documentclass{article}
\usepackage{graphicx} % This line is required!
\usepackage{tikz}

\begin{document}

% Your image inclusion command
% The file "some_other_image.png" must be in the same folder as this .tex file
\includegraphics{some_other_image.png}


% Your TikZ code, which is already working correctly
\begin{tikzpicture}
    ...
\end{tikzpicture}

\end{document}
```