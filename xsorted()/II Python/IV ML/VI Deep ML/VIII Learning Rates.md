Learning Rate
Hyperparameters are set by us, like the width, depth, and $\eta$ of the network
	$\eta$, or the Learning Rate, is rate at which the model is allowed to modify its weights in respect to the cost gradient

Learning rate Schedule
	To optimize the models learning, we start with high training rates to facilitate big patterns and initial discoveries
		we lower it as the model progresses through the data so it does not overfit as patterns it adopts become more specific
				ex:
					First 5 epochs : $\eta = 0.1$
					Second 20 epochs : $\eta = 0.01$
					Third 100 epochs : $\eta = 0.001$
				A more modern solution is an exponential learning rate based on the number of epochs. 
					for n in range(epochs):
						$\eta = \eta_0  e^{-n / c }$
						so in the exponent of e, n is the current epoch and c is some constant
						c can be a range of values but its around the number of epochs needed to minimize the cost
							if this is around 100 epochs, c could be from 50 - 500
							if this is around 1000 epochs, c could be from 500 - 5000
								c is another Hyperparameter of the model
This shows the lost function against the epoch count of different learning rates. A regular learning rate, i.e., 0.01, is shown in blue. It learns but plateaus easily and is prone to being stuck in a local minimum. Shown in red is a learning rate that is too aggressive ; it learns faster initially but it also plateaus earlier. Green is the ideal learning rate we are aiming for.

```tikz
\begin{document}
\begin{tikzpicture}[x=0.6cm, y=0.6cm]

    % --- Define boundaries and axes ---
    \draw[step=1, gray, very thin] (0,0) grid (10,10);
    \draw[->, thick] (0,0) -- (10,0) node[right] {$epoch$};
    \draw[->, thick] (0,0) -- (0,10) node[above] {$Loss$};
    \clip (0,0) rectangle (10,10);

    % --- Plot the piecewise function (steep then plateau) ---
    \draw[blue, thick] (0,10) -- (1,7) -- (2,5) -- (6,3) -- (10,2.75) -- (10,2.25);
    \draw[red, thick] (0,10) -- (0.5,6) -- (1,4.5) -- (2.5,3.75) -- (4,3.5) -- (10,3.25); %-- (15,3.2);
    \draw[green, thick] (0,10) -- (0.75,6.5) -- (1.5,4.75) -- (3,3.5) -- (5,2.5) -- (7,2) -- (10,1.75);

\end{tikzpicture}
\end{document}
```

AdaGrad
*Adaptive Gradient Algorithm*
	The Adaptive Gradient Algorithm was proposed in 2011 and dynamically varies the learning rate after each update for every weight individually. It divides $\eta$ by the square root of a monotonously increasing function, G. 
				$\triangledown w_i (t) = - \frac{\eta}{\sqrt{G_i (t)}+\epsilon} \frac{\partial L}{\partial w_i}(t)$
			Since $\eta$ is divided by the monotonously increasing G { plus $\epsilon$ incase G is ever 0 }, $\eta$ is monotonously { quadratically ? }decreasing. $t$ is the iteration or batch or epoch. G's function is as follows :
					$G_i (t) = G_i (t - 1) + (\frac{\partial L}{\partial w_i}(t))^2$
									*with beginning point $G_i(0) = 0$*
				So we are dividing the learning rate by the gradient of the loss with respect to that weight every time we update the weights. It also considers the previous value of G.


RMSprop
*Root Mean Square Propagation*
	Root Mean Square Propagation is very similar to AdaGrad but its G function is averaged out with $\beta$ :
				$\triangledown w_i (t) = - \frac{\eta}{\sqrt{G_i (t)}+\epsilon} \frac{\partial L}{\partial w_i}(t)$
								$G_i (t) = \beta G_i (t - 1) + (1-\beta)(\frac{\partial L}{\partial w_i}(t))^2$
												 *Decay Factor* : 	 $\beta$ = 0.99 
						With AdaGrad, the monotonous increase eventually is not advantage as it can be come extremely large, making $\eta$ approach 0. RMSprop helps with this by diminishing G by some decaying factor, i.e., 0.9 or 0.99, and stops $\eta$ from being inevitably zeroed. This is $\beta$.


AdamE
*Adaptive Moment Estimation*
	Adam uses Momentum and RMSprop in its equation. It was proposed in 2014 and uses momentum as its variable instead of G or $\beta$.
			$\triangledown w_i (t) = - \frac{\eta}{\sqrt{G_i (t)}+\epsilon} M_i(t)$
					It modifies the Momentum function we used earlier
				$M_i(t)= \alpha M_i(t-1) + (1-\alpha) \eta \frac{\partial L}{\partial w_i}(t)$
					$M_i(0) = 0$
		This function removes the calculation of gradient descent of each weight and holds the value in the function M. It further averages the gradients descent of each weight over another decay factor, $\alpha$. This lessens the effects of exploding gradients of zeroed functions. Its good.