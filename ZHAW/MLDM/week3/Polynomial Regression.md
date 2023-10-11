
# Polynomial Models

for non-linear relations, instead of a linear combination of parameters like $h(x)$ from [[MLDM 2#Linear Regression]] we try to fit a polynomial of a fixed degree, i.e.
$$
h(x) =  \theta_0 + \theta_1 x + \theta_2 x^2 + \theta_3 x^3
$$


### Fitting

- define artificial variables $z_1 = x, z_2 = x^2, z_3 = x^3$ to reformulate the hypothesis function as
$$
h_{\theta}(z) =  \theta_0 + \theta_1 z_1 + \theta_2 z_2 + \theta_3 z_3
$$
- now the same methods from linear regression like [[Gradient Descent]] can be used


note the $z$ substitution trick also works for multivariate data where $h$ would be more complicated like $h(x_1, ...,x_n) = \theta_0 +  \theta_1 x1 + \theta_2 x_1^2 x_3 ...$ 





# Over- and Underfitting

The degree of the polynomial is crucial for a good fit, is it too low the fit wont approximate complex curves well but too high and the fit curve becomes too "jumpy"
Overfitted data usually looks ok for trained data but easily falls apart on untrained/unseen data

![[over_under_fitting.png]]

Under-/Overfitting are also termed as **bias / variance** respectively
 



# Regularization

to avoid overfitting we can prevent the curve from "jumping". 
In general: smaller absolute values of $\theta$ -> less extreme curve
	BUT: we do not know how much extreme is too extreme
Solution: learn this data from the training, called **regularization** which aims to limit $\theta$ values from becoming too large

For this a new term is added to the cost function
$$
J(\theta) = \frac{1}{2M} \left[ \sum_{m=1}^M(y_m - h_\theta(x_m))^2 + \lambda \sum_{j=1}^n \theta_j^2 \right]
$$
Hypothesis:
$$
h_\theta(x) = \theta^T x = \sum_{j=1}^n \theta_j * x_j
$$

### NOTE
$\lambda$ depends **ONLY** on $\theta$, not the training samples, the **hyperparameter $\lambda$** determines "how much" regularization counts. Larger values will encourage $\theta$ to stay small


### Hyperparameter optimization

Cannot be known beforehand, a set of values should be tried and evaluated based on a metric like $R^2$ from [[MLDM 2#Coefficient of Determination]]

In polynomial regression there are 2 other hyperparameters: degree of the polynomial and learning rate.
For a good result all these hyperparameters must be well balanced between each other.

With smaller datasets these can be evaluated with **grid search**. simply trying out the combinations
In more complex situations heuristics like **local search** or **simmulated annealing**

**Genetic Algorithms** using selection, crossover and mutation to improve populations of hyperparameter settings over time.