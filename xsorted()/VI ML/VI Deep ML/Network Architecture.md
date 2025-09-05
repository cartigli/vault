Layer 0 is our input layer, so our data is given to the Model here. If our data has 10 components or variables, we would have 10 neurons in layer 0

```tikz
\begin{document}
\begin{tikzpicture}

    % style neurons
    \tikzstyle{neuron}=[circle, draw, minimum size=10pt]

    % Layer 0
    \node[neuron] (I1) at (0, 1) {$x_1$};
    \node[neuron] (I2) at (0, 0) {$x_2$};
    \node[neuron] (I3) at (0, -1) {$x_3$};

    % Hidden Layer[s]
    \node[neuron] (H11) at (2.5, 1.5) {$h_1$};
    \node[neuron] (H12) at (2.5, 0.5) {$h_2$};
    \node[neuron] (H13) at (2.5, -0.5) {$h_3$};
    \node[neuron] (H14) at (2.5, -1.5) {$h_4$};

    \node[neuron] (H21) at (2.5, 1.5) {$hh_1$};
    \node[neuron] (H22) at (2.5, 0.5) {$hh_2$};
    \node[neuron] (H23) at (2.5, -0.5) {$hh_3$};
    \node[neuron] (H24) at (2.5, -1.5) {$hh_4$};

    % Output Layer
    \node[neuron] (O1) at (5, 0) {$y$};

    % Connect the nodes with lines
    \draw (I1) -- (H11);
    \draw (I1) -- (H12);
    \draw (I1) -- (H13);
    \draw (I1) -- (H14);

    \draw (I2) -- (H11);
    \draw (I2) -- (H12);
    \draw (I2) -- (H13);
    \draw (I2) -- (H14);

    \draw (I3) -- (H11);
    \draw (I3) -- (H12);
    \draw (I3) -- (H13);
    \draw (I3) -- (H14);

    \draw (H11) -- (H21);
    \draw (H11) -- (H22);
    \draw (H11) -- (H23);
    \draw (H11) -- (H24);

    \draw (H12) -- (H21);
    \draw (H12) -- (H22);
    \draw (H12) -- (H23);
    \draw (H12) -- (H24);

    \draw (H13) -- (H21);
    \draw (H13) -- (H22);
    \draw (H13) -- (H23);
    \draw (H13) -- (H24);

    \draw (H14) -- (H21);
    \draw (H14) -- (H22);
    \draw (H14) -- (H23);
    \draw (H14) -- (H24);

    \draw (H21) -- (O1);
    \draw (H22) -- (O1);
    \draw (H23) -- (O1);
    \draw (H24) -- (O1);

\end{tikzpicture}
\end{document}
```
