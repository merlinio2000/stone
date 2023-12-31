#### Intro
motivation: #linear-regression is often too slow to be practical for larger datasets($O(n^3)$), also not very numerically stable for highly correlated columns

NO exact solution, gradient descent provides an approximation

Common approach: start with an initial "guess" for $\theta$ and iteratively try to minimize the cost function $J$ from [[MLDM 2#Linear Regression]]

## Gradient Descent 

uses the gradient (i.e. paritial derivatives) to determine in which direction the $\theta_i$ have to be adapted to reduce cost.
The gradient gives the direction of the **steepest increase** and by moving in the opposite of that direction we decrease the functions value

### General Equation
$$
\begin{aligned}
&1. \text{Initialize } \theta_0, \dots, \theta_n \\
&2. \text{Repeat until convergence} \\
& \qquad \qquad \theta_j = \theta_j - \alpha \frac{\partial}{\partial\theta_j}J(\theta) \qquad \forall j = 0,\dots,n
\end{aligned}
$$

- $\alpha$  in this equation represents the learning rate which determines how far a single step goes
- since we want to minimize $J$ we move opposite the gradient ($- \alpha*...$)
- convergence means that the values dont change much anymore

### Linear Regression equation

$$
\theta_j = \theta_j - \alpha \frac{1}{m} 
\sum_{i=1}^m \left(h_\theta(x^{(i)}) - y^{(i)} \right) x_j^{(i)} 
\qquad \forall j = 1,...,n
$$
Univariate linear regression has a concave cost -> **every** local minimum is a global minimum


## Learning Rate

can be either:
- too low: very slow progress towards convergence
- good: adequate progress
- too high: "jumping" between solutions and maybe even not converging
![[learning_rate.png]]

#### Optimization

Start with a high learning rate, gradually "decay" to a lower rate, e.g.
$$
 \alpha_t = \frac{1}{1 + decayrate * t} * \alpha_0
$$



## Batch Gradient Descent

[[#Linear Regression equation]]

Advantage: guaranteed convergence, moves rather "straight" to convergence
Disadvantage: All samples need to be in memory at once
![[batch_gd.png]]

## Stochastic Gradient Descent SGD

![[SGD.png]]


## Mini-batch Gradient Descent

![[mini-batch_gd.png]]