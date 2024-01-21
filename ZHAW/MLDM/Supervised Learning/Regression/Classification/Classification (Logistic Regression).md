

contrast to regression: instead of continuous $y$ values data comes in pairs of $x,y$ where $y$ is in a finite set of possibilities (i.e. $\set{back pain, no back pain}$) and the goal is to predict classification into those possibilities based on $x$


**Binary classification** is a special case where $y$ is only of two outcomes (true/false)


## Sigmoid / Linear Regression based Classification

Use of **sigmoid** functions to approximate the "hard" step nature of classification with a function $g$ :
Example of the **logistic sigmoid**
Function is:
- s-shaped
- continuous
- differentiable
- $\hat{y} \in (0, 1)$
- monotonic 

$$\Large
g(z) = \frac{1}{1 + e^{-z}}
$$



![[logistic_sigmoid.png]]

The new hypothesis function $h$ using this sigmoid function would be of the form (for univariate)
$$\Large
h_\theta(x) = g(\theta_0 * x + \theta_1)
$$

![[sigmoid_hypothesis.png]]



# Logistic Regression (Binary)

Mathematically similar to linear regression but with a sigmoid function to approximate a "step" based shape, see [[#Linear Regression based Classification]]

In binary problems the value of $\hat{y}$ can be interpreted as the "confidence" of the model in a "positive" (close to 1) outcome, with higher values meaning a higher confidence 

Univariate:
$$\large
\hat{y} = h_\theta(x) = g(\theta_0 + \theta_1 * x) = 
\frac{1}{1 + e^{-(\theta_0 + \theta_1 * x)}}
$$

Multivariate:
$$\large
\hat{y} = h_\theta(x) = g(\theta^T x) = \frac{1}{1 + e^{-\theta^T x}}
$$

with $\theta^T x = \theta_0 x_0 + \theta_1 x_1 + ... + \theta_n x_n$     (== scalar product)



## Training

No closed form solution like the normal equation -> gradient descent

### Log Loss

Instead of the sum of least residual squares (RSS) a new function called **log loss** is used

$$\large
\textrm{Loss}(h_\theta(x), y) = \left\{ \begin{align}-\log(h_\theta(x)) & \quad \textrm{if}\quad y=1 \\
                                                          -\log(1 - h_\theta(x)) & \quad \textrm{if}\quad y=0 \end{align} \right.
$$

Which is often instead written as 
$$\large
\textrm{Loss}(h_\theta(x), y) = -y \log(h_\theta(x)) - (1 - y) \log(1 - h_\theta(x))
$$


### Loss function

$$\Large
J(\theta) = \frac{1}{M} \sum_{m=1}^M \textrm{Loss}(h_\theta(x_m), y_m)
$$

### Gradient Descent Algo

$$
\begin{align}
1.& \text{Initialize} \: \theta_0, \theta_1 \\
2.& \text{Repeat until convergence:}\\
\; & \text{Update} \: \theta_0 = \theta_0 - \alpha \frac{1}{M} \sum_{m=1}^{M}(h_{\theta}(x_m) - y_m)\\
\;&  \text{Update} \: \theta_1 = \theta_1 - \alpha \frac{1}{M} \sum_{m=1}^{M}(h_{\theta}(x_m) - y_m)x_m\\
\end{align}
$$




## Evaluation of Binary Classification

For regression we had Mean Squared Error (MSE) as the most common,
classfication -> **proportion-correct accuracy** often abbreviated as **accuracy**

#### Proportion-Correct Accuracy

- the proportion of samples that were correctly classified
- higher values are better (not like MSE)

A good question to ask when "rating" the accuracy is comparing against how high the accuracy would be if the model always simply predicts the most common classification.
For this values $\hat{y} > \textrm{Threshold } \tau$  count as positive (1) and $\hat{y} \le \tau$ as negative



## Hyperparameters

Any variable that influences the training but not contained in the model itself (so not $\theta$)

- Learning rate $\alpha$
- num gradient descent iters $T$

### Hyperparameter optimization

Instead of simply trying out different values and choose the one that yields the highest [[#Proportion-Correct Accuracy]] , split the data in three sets:

- **Training Set**, given fixed hyperparameter ($\alpha = 0.1$) these data points are used to optimize $\theta$
- **Validation/Development Set**, used to measure how good the model of a particular hyperparam choice is. Called **validation accuracy**
- **Testing Set**, Union of Validation and Training Set.  Used at the very end of hyperparam optimization. Judge how good the value is

The training set is then continously trained on using different hyperparams. After judging them in validation one of these hyperparam configurations is "commited upon"

see [[#Python example#Hyperparameter Optimization]]


## Sensitivity to outliers


Example: Correlation $x$ = blood cholesterol, $y$ = heart pain

First dataset with no outliers: Both regression and classification work just fine

![[outlier_sens_OK.png]]

Second with massive outlier (800):  the classification is unaffected since it would have already classified the outlier correctly anyways (the exact value doesnt matter only if its above/below a certain threshold)

![[outlier_sens_NOK.png]]


# Multi-class Classification

For more than 2 classes [[#Logistic Regression (Binary)]] can no longer be used since the model is inherently built for binary classification

Two options:
- Decompose $K$-classes problem into $K$ different binary problems (e.g. [[#One-vs-rest Classification]])
- Use inherently multi-class technique (Neural Networks)


## One-vs-rest Classification (one-vs-all)

Train $K$ binary classifiers (for $K$ classes). The goal of the $k$-th classifier is to distinguish a sample $x$ from belonging to any class other than $k$

![[one-vs-rest.png]]

To get the label for $x$ we apply all $K$ classifiers and choose the one with the highest $\hat{y}_k$





# Python example

#### Binary Classification Training

```python
import numpy as np
import sklearn.linear_model

# Cholesterol levels of patients; need to ensure X is (M x 1) matrix.
X = np.atleast_2d([ 100, 233, 150, 280, 80, 320, 135, 93, 224, 178 ]).T
# Labels of whether they had heart pain in the next year
y = np.array([ 0, 1, 1, 1, 0, 1, 1, 0, 1, 0 ])

# Train model
logr = sklearn.linear_model.LogisticRegression()
logr.fit(X, y)

# We must pack the input x into a 2-d array of size (M x 1). Here, M=1.
yhat = logr.predict([ [ 190 ] ])  # gives 0/1 binary prediction
yhat_prob = logr.predict_proba([ [ 190 ] ])  # gives probabilistic prediction
print(yhat, yhat_prob)
# [[0.16436593], [0.83653407]]
```
#### Hyperparameter Optimization

```python
bestAccuracy = -1
# Try each alpha
for alpha in [ 0.0001, 0.001, 0.01 ]:
    # Train on training data
    model = train(dataTrain, alpha)
    # Evaluate on validation data
    accuracy = evaluate(dataValid, model)
    # Keep track of best alpha
    if accuracy > bestAccuracy:
        bestAlpha = alpha
        bestAccuracy = accuracy
# Since we are done with hyperparameter search, it's
# legitimate to "add" the validation data to our training data
# (which tends to improve the accuracy on the test set).
bestModel = train(dataTrain + dataValid, bestAlpha)
accuracy = evaluate(dataTest, bestModel)
```