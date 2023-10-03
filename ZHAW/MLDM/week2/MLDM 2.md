some definitions:
- Median $\mu$
# Linear Regression
#linear-regression 
Given $M$ samples $(x_m, y_m)$

Hypothesis function (gives estimates for $y=f(x)$) 
$$h(x) = \theta_0 + \theta_1*x \quad (= \hat{y} ) $$
Cost function (how good is the estimate)
$$
 J = \frac{1}{2M} \sum^{M}_{m=1}(y_m - \hat{y}_m)
$$
The goal is to minimize the cost function

## Residual Plot

Helps to judge a regression (especially in higher dimensions since it always stays 2D)
![[Pasted image 20230927211845.png]]


## Assumptions of Linear regression

- Linearity: in/output have linear relation
- Independence: the outcome of one sample doesnt affect another (would be violated by periodically repeating data -> would mean dependent on time)
- Normality: errors should be normally distributed (larger deviations less likely)
- Equality of Variance("Homoscedasticity"): error distribution should be the same for all inputs


## Coefficient of Determination

$$
R^2 = 1 - \frac{SS_{res}}{SS_{tot}}
$$

A model that always predicts $\mu_y$  has $R^2 = 0$, $R^2 = 1$ would mean a perfect fit, values below $0$ mean a prediction **worse** than the median $\mu_y$