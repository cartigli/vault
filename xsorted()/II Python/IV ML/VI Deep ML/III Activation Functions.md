Non-linear functions for weights and biases

Sigmoid Function : $\sigma (x) = \frac{1}{1+\epsilon^{-x}}$
	*Derivative* : $\sigma(x)(1-\sigma(x))$
			This ranges form 0-1, and sort of behaves like a biological neuron
				Low values are exponentially low and high numbers are exponentially high
					Similar to people neurons, this acts as a sort of energy for the neuron; its firing
							When then model's neurons are given certain values, they can ' fire ' indicating information or signaling that can be interpreted as such
							Oddly enough, if our weights are too close the center value of the Sigmoid Function, the slope is essentially linear
								Conversely, at either pole, highs and lows are pushed to their extremes rapidly

```tikz 
\begin{document}
\begin{tikzpicture}[xscale=2,yscale=4]
    % --- Draw Grid ---
    % Grid now goes from bottom-left (-4,-0.2) to top-right (4,1.2)
    \draw[step=1cm, gray, very thin] (-4,-0.2) grid (4,1.2);

    % --- Draw Axes ---
    \draw[->, thick] (-4,0) -- (4,0) node[right] {$x$};
    \draw[->, thick] (0,-0.2) -- (0,1.2) node[above] {$sigmoid(x)$};

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


TanH : Hyperbolic Tangent : $\text{tanh}(a) = \frac{\epsilon^a-\epsilon^{-a}}{\epsilon^a+\epsilon^{-a}}$
	*Derivative* : $\frac{4}{(\epsilon^a+\epsilon^{-a})^2}$
	 Ranges from -1 to 1, similar to the sigmoid function but more normally distributed over and more aggressive ' transition ' area but consequently more polarization

```tikz 
\begin{document}
\begin{tikzpicture}[xscale=2,yscale=2]
    % --- Draw Grid ---
    % Grid now goes from bottom-left (-4,-0.2) to top-right (4,1.2)
    \draw[step=1cm, gray, very thin] (-4,-1.2) grid (4,1.2);

    % --- Draw Axes ---
    \draw[->, thick] (-4,0) -- (4,0) node[right] {$a$};
    \draw[->, thick] (0,-1.2) -- (0,1.2) node[above] {$tanh(a)$};

    % --- Add Ticks and Labels ---
    \draw (0,1) -- (-0.1,1) node[left] {1};
	\draw (0,-1) -- (-0.1,-1) node[left] {-1};
    \foreach \x in {-3,-2,-1,1,2,3}
        \draw (\x,0) -- (\x,-0.05) node[below] {\x};

    % --- Plot the Sigmoid Function ---
    \draw[blue, thick, smooth, samples=100, domain=-4:4]
        plot (\x, {tanh(\x)});
        %plot (\x, {(exp(\x) - exp(-\x))/(exp(\x) + exp(-\x))});
\end{tikzpicture}
\end{document}
```

Softmax Function: $\sigma_i(a) = \frac{\epsilon^{a_i}}{\sum_i\epsilon^{a_i}}$
	*Derivative* : $\frac{\partial \sigma_i(a)}{\partial a_i} = \sigma_i (a) (\delta_{ij} - \sigma_i(a))$ where $\delta_{ij}$ is 1 if i = j, 0 otherwise
			This is the normalization we would use for the outputs of the classification model as it outputs a probability ; all the results sum to 1
				This is not used for many if any layers within the network; the distortion of values from their original is too great to retain information when feeding forward
						Basically, softmax is only ever applied to the output layer of a network for probabilities of predictions 
