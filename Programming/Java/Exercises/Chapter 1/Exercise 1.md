# Point processing

Purpose: Points processing:

We have the points array (x, y)
The program calculate coefficients of the line **y = ax + b**, and with switch you will get some qualities, from bias to prediction accuracy.

Purpose: Statistics and predictions based on points (least squares method).

## Actions

Your actions:

1. Asked user about "n" points amount (an integer, from 2 to 100).
2. Create 2 arrays: double x[] and double y[] of size n.
3. Filled them - user input values x and y step by step for every point.
4. After filling, shows the menu:

Menu:
```text
1 - Slope coefficient "a" (slope)
2 - Intercept b (intercept)
3 - Pearson's correlation coefficient "r" (strenght of correlation).
4 - Predict "y" for "a" given x
5 - Display the equation of the line
0 - Exit.
```

Complete this point by a switch-case construction.
For every case, use the sum cycles ($sumX$, $sumY$, $sumXY$, $sumX^2$, $sumY^2$) - these requires for formulas.
Add the conditional checkers - (If every x as the same, throw an exception: Dividing by zero)

# Additionally

##### You have n points ($x_i$, $y_i$)

Then, the required amounts (calculated once in the loop or each time as needed):
- - Sx = Σ $x_i$
- - Sy = Σ $y_i$
- - Sxy = Σ ($x_i$ * $y_i$)
- - Sxx = Σ $(x_i)^2$
- - Syy = Σ $(y_i)^2$
#### Formulas:

- Slope a = $(n * Sxy - Sx * Sy) / (n * Sxx - Sx * Sx)$
- Intercept b = $(Sy - a * Sx) / n$
- Correlation coefficient:
	$r = (n * Sxy - Sx * Sy) / sqrt((n*Sxx - Sx²) * (n*Syy - Sy²))$
	(value ranges from -1 to 1; the closer to 1, the better the line fits the points)
- Prediction for a given x: y_pred = $a * x + b$

# Example of program output:

```Console
How many points? 3
Enter x1, y1: 1  2
Enter x2, y2: 2  4
Enter x3, y3: 3  5

Menu:
1 – Slope a
2 – Intercept b
3 – Correlation r
4 – Predict y
5 – Equation
0 – Exit
Your selection: 1

Result: a = 1.5

... (after selecting 5)
Equation of the line: y = 1.5 * x + 0.8333333333333333
```