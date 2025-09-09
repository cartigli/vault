usefulness: price optimization, inventory management
- goal: increase profit, minimize costs

Now that collection/preprocessing/Data analysis
transition from analysis to analytics - trend prediction

[Traditional]
- Regression [popular]
	- representing causal relationships between observations[/measurements]
	- [shown below] scatter plot of values in respect to [x, y]
```tikz
\begin{document}
\begin{tikzpicture}

    % style for data points
    \tikzstyle{point}=[circle, fill=blue, minimum size=4pt, inner sep=0pt]

    % Draw coordinate axes
    \draw[->] (0,0) -- (5,0) node[right] {Independent Variable};
    \draw[->] (0,0) -- (0,5) node[above] {Dependent Variable};

    % Plot the data points
    \node[point] at (1, 1.5) {};
    \node[point] at (1, 0.9) {};
    \node[point] at (2, 2.2) {};
    \node[point] at (2, 2.7) {};
    \node[point] at (3, 3.3) {};
    \node[point] at (3, 2.9) {};
    \node[point] at (4, 3.9) {};
    \node[point] at (5, 4.2) {};
    \node[point] at (5, 4.7) {};
    \node[point] at (5, 4.4) {};

\end{tikzpicture}
\end{document}
```
-		y = house size 
		 x = size of house
	 	Equation [y = m[slope]x + b[y_intercept]]
			 regression aims to define a relationship between sets [pairs in this ex] of data
			 tries to find trend instead of perfect fit; much more interpretable measurement
			 in this ex, size of house increases = price increases

[Clustering] - group observations
	find collections and groups standing out from whole
	more closely related between themselves than the group as a whole
		[below] scatter plot of values in respect to [x, y]
```tikz
\begin{document}
\begin{tikzpicture}

    % style for data points
    \tikzstyle{point}=[circle, fill=blue, minimum size=4pt, inner sep=0pt]

    % Draw coordinate axes
    \draw[->] (0,0) -- (5,0) node[right] {House Size};
    \draw[->] (0,0) -- (0,5) node[above] {Price};

    % Plot the data points
    \node[point] at (1, 1.5) {};
    \node[point] at (1, 0.9) {};
    \node[point] at (1, 0.5) {};
    \node[point] at (2, 1.3) {};
    \node[point] at (2, 2.1) {};

    \node[point] at (4, 4.6) {};
    \node[point] at (4, 3.9) {};
    \node[point] at (5, 4.2) {};
    \node[point] at (4, 4.3) {};
    \node[point] at (5, 4.4) {};

\end{tikzpicture}
\end{document}
```
-	y_axis |________________________ x_axis
	x = price of house
	y = size of house
		now, we see two clusters of 'outliers' 
			small house ; lower price
			large house ; higher cost

[Factor Analysis] - grouping explanatory variables
- Ex: 100 question survey
- 1. I like animals [1-5]
- 1. I care about animals [1-5]
- 1. I am against animal cruelty [1-5]
	- one can assume if someone responds 5 for 1, they'll likely continue with high score responses for q2 & q3
	- from this, we could assume relevancy/relationship between the q's and responses
	- use this relationship to combine all q's into 'general attitude towards animals'
		- repeated over 100 question survey:
		- variables decrease from 100 to a multiple of 100 [factorally scale database size]

[Time Series] - plotted values on T.time
- time is *always* on the x_axis
```tikz
\begin{document}
\begin{tikzpicture}

    % style for data points
    \tikzstyle{point}=[circle, fill=blue, minimum size=4pt, inner sep=0pt]

    % Draw coordinate axes
    \draw[->] (0,0) -- (5,0) node[right] {Time};
    \draw[->] (0,0) -- (0,5) node[above] {Temperature};

    % Plot the data points
    \node[point] at (1, 1.1) {};
    \node[point] at (1.5, 1.2) {};
    \node[point] at (2, 1.4) {};
    \node[point] at (2.5, 1.8) {};
    \node[point] at (3, 2.4) {};
    \node[point] at (3.5, 2.2) {};
    \node[point] at (4, 1.8) {};
    \node[point] at (4.5, 1.7) {};
    \node[point] at (5, 1.9) {};

\end{tikzpicture}
\end{document}
```