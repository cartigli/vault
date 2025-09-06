Algorithms used to vary our model's parameters

So far, we have seen Gradient Descent optimization
	this technique involves iterating over every weight to compute its contribution to the error of the model through the derivative of the cost function. This is slow and computational rich, requiring re-computation of every value after every epoch. It is also the original ML optimization.

Stochastic Gradient Descent
	This is what we used in our previous TensorFlow model. Instead of updating all weights at once after a single epoch, Stochastic Gradient Descent splits epochs into batches and after running each batch, the weights are updated. The default size of a batch is one, so if we had an epoch of 100, the weights would be updated 100 times while that epoch ran. If we have 10 batches in an epoch, the weights will be updated 10 times during one epoch.
	This is just faster gradient descent, and some information is lost, however, splitting into batches allows CPU / GPU cores to compute batches in parallel, which significantly decreases the time for training. Also, as we did with our models, having one batch equal an entire epoch is called Batch Gradient Descent. If we had, say an epoch of 100 and batch size of 10, this would be Mini-Batch Gradient Descent, not Stochastic Gradient Descent.

Classic Problems
	Gradient Descent works by finding the slope of the gradient of the cost function with the goal of minimizing it. To do so, it follows the derivative of the cost function to find its minimums by going down the direction of the negative slope. This is the information it uses to update its weights.
	The biggest problem with Gradient Descent is the local minimum. If the graph of our Cost Function looks like the function below, the Gradient Descent finds this portion of the function that has upwards slopes on either side. Using the only method it has, the gradient, to determine the minimum of this function, the model oscillates in the valley and never reaches the true minimum. Sometimes it can overcome this with a properly configured learning rate and good luck, but it is not reliably capable of doing so.
	This is also why the model we created has no means to explain a gradient descent with curvature like this, it can only explain away linear relationships between data points. This relationship is considerably more complex and has several exponential variables.

```tikz
\begin{document}
\begin{tikzpicture}[x=0.6cm, y=0.8cm]

    % --- Define boundaries for the first quadrant ---
    \draw[step=1, gray, very thin] (0,0) grid (9,6);

    % --- Draw Axes ---
    \draw[->, thick] (0,0) -- (9,0) node[right] {$x$};
    \draw[->, thick] (0,0) -- (0,6) node[above] {$f(x)$};

    % --- Add Ticks and Labels ---
    \foreach \x in {1,2,...,8}
        \draw (\x,0) -- (\x,0.1) node[below] {\x};
    \foreach \y in {1,2,...,5}
        \draw (0,\y) -- (0.1,\y) node[left] {\y};

    % --- ADD THIS LINE ---
    % This acts as scissors, hiding anything drawn outside this box.
    \clip (0,0) rectangle (9,6);

	\fill[red] (1, 3.35) circle (2pt);
    % --- Plot the non-linear function ---
    % The part of the curve where y > 6 will now be invisible.
    \draw[blue, thick, smooth, samples=100, domain=0:8.5]
        plot (\x, {0.0497*pow(\x,4) - 0.707*pow(\x,3) + 3*pow(\x,2) - 4*\x + 5});

\end{tikzpicture}
\end{document}
```

Momentum
*Extension of GD*
	Imagine a ball rolling down a hill. The steeper the slope, the forward energy the ball gains.
Similarly, momentum accountants for the small uphills in the gradient slope and can compensate. It takes into consideration the rate at which we are descending down the gradient slope when determining the size of the consecutive step.
	In gradient descent, the consecutive step is determined with :$$w_{new} = w_{old} - \eta\frac{\partial L}{\partial w}$$
	With momentum, we add the previous update step to the formula:$$w_{new} = w(t) - \eta \frac{\partial L}{\partial w_{old}}(t) - \alpha \eta \frac{\partial L}{\partial w_{old}}( t - 1 )$$
	We multiply the previous gradient descent by some coefficient, denoted $\alpha$, because otherwise it would be considered at the same importance as the current gradient. $\alpha =$ 0.9 is conventional.