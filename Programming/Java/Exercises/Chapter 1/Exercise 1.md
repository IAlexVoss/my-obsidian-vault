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
For every case, use the sum cycles ($sumX$, $sumY$, $sumXY$, $sumX^2$ ) - these requires for formulas.
Add the conditional checkers - (If every x as the same, throw an exception: Dividing by zero)

# Additionally

You have n points ($x_i$, $y_i$)

Then, the required amounts (ca)