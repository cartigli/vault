Heart of ML Architecture
.
	In our previous model, the loss was directly related to the weights and indirectly related to the errors, or deltas, allowing us to adjust them directly
	calculating the delta for a hidden layer is more difficult as we have no targets for their values.
-
```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=4pt, inner sep=2pt]

    % Hidden Layer[s]
    \node[neuron] (x1) at (-2, 1) {$x_{1}$};
    \node[neuron] (x2) at (-2, 0) {$x_{2}$};
    \node[neuron] (x3) at (-2, -1) {$x_{3}$};

    \node[neuron] (H1) at (0, 1.5) {$h_{1}$};
    \node[neuron] (H2) at (0, 0.5) {$h_{2}$};
    \node[neuron] (H3) at (0, -0.5) {$h_{3}$};
    \node[neuron] (H4) at (0, -1.5) {$h_{4}$};

    % Output Layer
    \node[neuron] (y1) at (2, 0.5) {$y_1$};
    \node[neuron] (y2) at (2, -0.5) {$y_2$};

    % Connect the nodes with lines
    \draw (x1) -- (H1);
    \draw (x1) -- (H2);
    \draw (x1) -- (H3);
    \draw (x1) -- (H4);

    \draw (x2) -- (H1);
    \draw (x2) -- (H2);
    \draw (x2) -- (H3);
    \draw (x2) -- (H4);

    \draw (x3) -- (H1);
    \draw (x3) -- (H2);
    \draw (x3) -- (H3);
    \draw (x3) -- (H4);

    \draw (H1) -- (y1);
    \draw (H2) -- (y1);
    \draw (H3) -- (y1);
    \draw (H4) -- (y1);

    \draw (H1) -- (y2);
    \draw (H2) -- (y2);
    \draw (H3) -- (y2);
    \draw (H4) -- (y2);

\end{tikzpicture}
\end{document}
```
.
	Take the model above. We Feed Forward by inputing data to the x's which multiply said values by every set of weights to derive the values for the hidden network. This is repeated for h1 which results in the outputs of the model, y1 and y2. y1 and y2 are compared to the targets to obtain the errors. This is is what we determine the optimal position of the weights and biases from
	In our miniature model, we only had one layer and so one set of partial derivatives to calculate. We needed the gradient of the cost with respect to the weights and the gradient of the cost with respect to the bias, determined independently. In Networks, we must calculate each gradient of the cost function of every weight and bias through these feeding patterns. This is because in our miniature model, the weights directly affected our model's loss. In Neural Nets, the relationship is less trivial. 
	The forefront issue is that the hidden layers have no targets, and therefor have no loss function. However, we can compute the errors for y1 and y2 and ' trace ' the root of the error back through the network. This is called Back Propagation.

```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=4pt, inner sep=2pt]

    % Hidden Layer[s]
    \node[neuron] (x1) at (-2, 1) {$x_{1}$};
    \node[neuron] (x2) at (-2, 0) {$x_{2}$};
    \node[neuron] (x3) at (-2, -1) {$x_{3}$};

    \node[neuron] (H1) at (0, 1.5) {$h_{1}$};
    \node[neuron] (H2) at (0, 0.5) {$h_{2}$};
    \node[neuron] (H3) at (0, -0.5) {$h_{3}$};
    \node[neuron] (H4) at (0, -1.5) {$h_{4}$};

    % Output Layer
    \node[neuron] (y1) at (2, 0.5) {$y_1$};
    \node[neuron] (y2) at (2, -0.5) {$y_2$};

    % Connect the nodes with lines
    \draw (x1) -- (H1);
    \draw (x1) -- (H2);
    \draw (x1) -- (H3);
    \draw (x1) -- (H4);

    \draw (x2) -- (H1);
    \draw (x2) -- (H2);
    \draw (x2) -- (H3);
    \draw (x2) -- (H4);

    \draw (x3) -- (H1);
    \draw (x3) -- (H2);
    \draw (x3) -- (H3);
    \draw (x3) -- (H4);

    \draw [red] (H1) -- (y1);
    \draw [red] (H2) -- (y1);
    \draw [red] (H3) -- (y1);
    \draw [red] (H4) -- (y1);

    \draw [red] (H1) -- (y2);
    \draw [red] (H2) -- (y2);
    \draw [red] (H3) -- (y2);
    \draw [red] (H4) -- (y2);

\end{tikzpicture}
\end{document}
```
-
	Above we see the weights for h1 to the output layer y as red. Each weight here contributes to a certain error from y1 or y2, e1 and e2. We initially take the gradient of the optimization function with respect to each of their weights to determine their contribution e1 or e2. For example, below we have the h1_w1 and h1_w2 weights and would find their contribution to e1 and e2 respectively.
```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=4pt, inner sep=2pt]

    % Hidden Layer[s]
    \node[neuron] (x1) at (-2, 1) {$x_{1}$};
    \node[neuron] (x2) at (-2, 0) {$x_{2}$};
    \node[neuron] (x3) at (-2, -1) {$x_{3}$};

    \node[neuron] (H1) at (0, 1.5) {$h_{1}$};
    \node[neuron] (H2) at (0, 0.5) {$h_{2}$};
    \node[neuron] (H3) at (0, -0.5) {$h_{3}$};
    \node[neuron] (H4) at (0, -1.5) {$h_{4}$};

    % Output Layer
    \node[neuron] (y1) at (2, 0.5) {$y_1$};
    \node[neuron] (y2) at (2, -0.5) {$y_2$};

    % Connect the nodes with lines
    \draw (x1) -- (H1);
    \draw (x1) -- (H2);
    \draw (x1) -- (H3);
    \draw (x1) -- (H4);

    \draw (x2) -- (H1);
    \draw (x2) -- (H2);
    \draw (x2) -- (H3);
    \draw (x2) -- (H4);

    \draw (x3) -- (H1);
    \draw (x3) -- (H2);
    \draw (x3) -- (H3);
    \draw (x3) -- (H4);

    \draw [red] (H1) -- (y1);
    \draw (H2) -- (y1);
    \draw (H3) -- (y1);
    \draw (H4) -- (y1);

    \draw [red] (H1) -- (y2);
    \draw (H2) -- (y2);
    \draw (H3) -- (y2);
    \draw (H4) -- (y2);

\end{tikzpicture}
\end{document}
```
-
	This is the optimization seen in our miniature model. This calculation of gradient directly from loss is a linear function and relationship. However, we need to find the preceding weights in this network. For instance, consider the weight shown in red below, that connects the outputs of the x1 neuron to the h1 neuron of the hidden layer. We'll call this x1_h1.
```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=4pt, inner sep=2pt]

    % Hidden Layer[s]
    \node[neuron] (x1) at (-2, 1) {$x_{1}$};
    \node[neuron] (x2) at (-2, 0) {$x_{2}$};
    \node[neuron] (x3) at (-2, -1) {$x_{3}$};

    \node[neuron] (H1) at (0, 1.5) {$h_{1}$};
    \node[neuron] (H2) at (0, 0.5) {$h_{2}$};
    \node[neuron] (H3) at (0, -0.5) {$h_{3}$};
    \node[neuron] (H4) at (0, -1.5) {$h_{4}$};

    % Output Layer
    \node[neuron] (y1) at (2, 0.5) {$y_1$};
    \node[neuron] (y2) at (2, -0.5) {$y_2$};

    % Connect the nodes with lines
    \draw [red] (x1) -- (H1);
    \draw (x1) -- (H2);
    \draw (x1) -- (H3);
    \draw (x1) -- (H4);

    \draw (x2) -- (H1);
    \draw (x2) -- (H2);
    \draw (x2) -- (H3);
    \draw (x2) -- (H4);

    \draw (x3) -- (H1);
    \draw (x3) -- (H2);
    \draw (x3) -- (H3);
    \draw (x3) -- (H4);

    \draw (H1) -- (y1);
    \draw (H2) -- (y1);
    \draw (H3) -- (y1);
    \draw (H4) -- (y1);

    \draw (H1) -- (y2);
    \draw (H2) -- (y2);
    \draw (H3) -- (y2);
    \draw (H4) -- (y2);

\end{tikzpicture}
\end{document}
```
-
	This weight was used to predict the value of h1 which in turn, helped us predict y1 and y2. Therefore, the explanation given by the weight of x1_h1 is proportionally effective on the final output, and therefore error, of y1 and y2 by a factor of h1. So, to compute the optimal value for this weight, we must consider x1_h1 as if it were directly connected to y1 and y2 as h1_y1_y2(x1_h_1) as an extension of the function, or the Chain Rule in calculus. When we push the errors backwards through the network like this, we can calculate the amount of error that h1 contributed. We use this as a synthetic target to calculate the gradient function for this value, which in turn is used to calculate the optimal position and adjustment for x1_h1. In this way, the adjustment of the weight x1_h1 is done in proportion to its impact on the error of the outputs, i.e.,  bigger contributions to the error are changed more than contributions with smaller impacts on error for every weight and bias in the network.
```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=4pt, inner sep=2pt]

    % Hidden Layer[s]
    \node[neuron] (x1) at (-2, 1) {$x_{1}$};
    \node[neuron] (x2) at (-2, 0) {$x_{2}$};
    \node[neuron] (x3) at (-2, -1) {$x_{3}$};

    \node[neuron] (H1) at (0, 1.5) {$h_{1}$};
    \node[neuron] (H2) at (0, 0.5) {$h_{2}$};
    \node[neuron] (H3) at (0, -0.5) {$h_{3}$};
    \node[neuron] (H4) at (0, -1.5) {$h_{4}$};

    % Output Layer
    \node[neuron] (y1) at (2, 0.5) {$y_1$};
    \node[neuron] (y2) at (2, -0.5) {$y_2$};

    % Connect the nodes with lines
    \draw [red] (x1) -- (H1);
    \draw (x1) -- (H2);
    \draw (x1) -- (H3);
    \draw (x1) -- (H4);

    \draw (x2) -- (H1);
    \draw (x2) -- (H2);
    \draw (x2) -- (H3);
    \draw (x2) -- (H4);

    \draw (x3) -- (H1);
    \draw (x3) -- (H2);
    \draw (x3) -- (H3);
    \draw (x3) -- (H4);

    \draw [red] (H1) -- (y1);
    \draw (H2) -- (y1);
    \draw (H3) -- (y1);
    \draw (H4) -- (y1);

    \draw [red] (H1) -- (y2);
    \draw (H2) -- (y2);
    \draw (H3) -- (y2);
    \draw (H4) -- (y2);

\end{tikzpicture}
\end{document}
```
-
	The process of walking back every calculation and derivative is denoted Back Propagation. Although trivial in examples with minimal layers and linear relationships, activation functions applied to each layer must be considered for Deep Networks. The error and loss of a weight beyond the output layer must be determined after the derivative and backward-error is found for every weight and layer, significantly increasing complexity and computation time.

my favorite resource on this topic:
https://medium.com/@waadlingaadil/learn-to-build-a-neural-network-from-scratch-yes-really-cac4ca457efc