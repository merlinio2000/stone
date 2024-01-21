short: **SVM**

- Hard Margin Classifier [[#Classification using Hyperplanes]]: **NO** violation of hyperplane allowed
- also [[#Soft Margin Classifier]] that allows violation
- The **Support Vector Machine (SVM)** is an extension of the **Support Vector Classifier** that results from enlargin the feature space using kernels [[#Kernel-Trick]]
# Hyperplanes

## Concept

- dimension -> features of the data set (cols of matrix $X$)

In $N$-dim space, a hyperplane is a flat subspace with dm $N - 1$
e.g. 2d -> hyperspace is a 1d line

Defined by equation:

$$\Large \begin{align}
b + w_1 x_1 + w_2 x_2 + \dots + w_N x_N & = 0 \\
b + \mathbf{w}^T\mathbf{x} & = 0
\end{align}
$$

$\mathbf{x}=\begin{pmatrix}x_1 & x_2 & \dots & x_N\end{pmatrix}^T$ represent a point in that $N$-dim space
If $x$ satisfies the above equation it is on the hyperplane

Comparison with $>$ resp. $<$ instead of $=$ tells us on which side of the plane
the point $x$ lies
-> Hyperplane separates hyperspace into 2 sides


## Classification using Hyperplanes

**BINARY** classification like [[Classification (Logistic Regression)]]
**BUT** $\large y \in \set{-1, +1}$ instead of $\large \set{0, 1}$

A test sample is denoted by
$$
\mathbf{x}^{\ast} = \begin{pmatrix}x_1^{(\ast)} & \dots & x_N^{(\ast)}\end{pmatrix}^T
$$
Goal is to set a hyperplane so that each sample gets correctly assigned its class based on what side of the plane it lies on

$$ \large
b + \mathbf{w}^T\mathbf{x}^{(m)} > 0 \ \ \ \text{if} \ y^{(m)}=1,
$$
$$ \large
b + \mathbf{w}^T\mathbf{x}^{(m)} < 0 \ \ \ \text{if} \ y^{(m)}=-1
$$
which also means that the hyperplane must statisfy (**HARD** marginal classifier)
$$\large
y^{(m)} \left(b + \mathbf{w}^T\mathbf{x}^{(m)}\right) > 0
$$

The magnitude (abs) of $f(x)$ can be interpreted as confidence.
larger = more confident

![[2d_hyperplane_example.png]]



## Hard / Maximal Margin Classifier

Target for learning since we want the furthest minimum distance of the plane to the points
== margin

The boundaries of this margin are called **gutters** (illustrated below)

![[max_margin_classifier.png]]

### Support Vectors

In this example 3 points are equidistant from the maximal margin and lie on the gutters.
They are also called **support vectors** (N-dim) since the hyperplane directly depends on them but not on other samples


### Construction of Max Margin Classifier

#todo re-visit chapter 6.4
![[max_margin_geom.png]]


Distance $r$ of arbitrary point $x$ to decision boundary
$$
\mathbf{x}=\mathbf{x}_\bot + r \frac{\mathbf{w}}{||\mathbf{w}||}
$$
This distance **ONLY DEPENDS** on the samples closest to the resulting hyperplane

We want to maximise $r$ so we need to express it as a function of $w$
... some fancy math see chapter 6.4
$$ \Large
r=\frac{f(\mathbf{x})}{||\mathbf{w}||}. \tag{6.7}
$$

**BUT** we only want to maximize it for the training sample closest to the hyperplane ->
$$\large
\underset{b, \mathbf{w}}{\text{max}}\left\{\frac{1}{||\mathbf{w}||}\overunderset{M}{m=1}{\text{min}}\left[y^{(m)}\left(b + \mathbf{w}^T\mathbf{x}^{(m)}\right)\right]\right\}
$$
($w$ does not depend on $m$, thus can be moved outside)
Also: samples must be correctly classified, see [[#Classification using Hyperplanes]]
$$\large
y^{(m)} \left(b + \mathbf{w}^T\mathbf{x}^{(m)}\right) > 0
$$




#### Primal Representation

Since a direct solution would be very complex we can convert into an easier problem
- Rescale parameters $w = \kappa w, b = \kappa b$
	- this does not change the distance to any points since it cancels out when dividing by $||w||$ 
- Define $\kappa$ such that $y^{(m)}f(\mathbf{x}^{(m)})=1$, which also means
	- $\overunderset{M}{m=1}{\text{min}}\left[y^{(m)}\left(b + \mathbf{w}^T\mathbf{x}^{(m)}\right)\right]=1$
	- Constraint becomes $y^{(m)}f(\mathbf{x}^{(m)}) \geq 1$
 - maximising $\frac{1}{||w||}$ is equivalent to **minimising** (1/2 simply for math convenience, does not affect optimal parameters)
$$ \Large
\underset{b, \mathbf{w}}{\text{min}}\frac{1}{2}||\mathbf{w}||^2
$$ 
$$\Large
\text{subject to} \ y^{(m)}\left(b + \mathbf{w}^T\mathbf{x}^{(m)} \right) \geq 1 \ \forall \ m=1,\dots,M
$$


#### Dual Representation

$$\large
\mathcal{L}(\boldsymbol{\alpha})=\sum_{m=1}^M \alpha_m -\frac{1}{2}\sum_{i=1}^M\sum_{j=1}^M \alpha_i\alpha_j y^{(i)}y^{(j)}\mathbf{x}^{(i)^T}\mathbf{x}^{(j)}
$$
- does not contain params $w, b$ anymore
- maximised using Lagrange multipliers $\boldsymbol{\alpha}=\begin{pmatrix}\alpha_1 & \alpha_2 & \dots & \alpha_M \end{pmatrix}$
- $\sum_{m=1}^M \alpha_m y^{(m)}=0$
- $\alpha_m \geq 0 \ \forall \ m=1,\dots,M$

From the optimised $\hat\alpha$ the optimal $\hat w, \hat b$ can be computed which then describe the hyperplane

Predictions can be made using
$$\Large
f(\mathbf{x})=\hat{b}+\hat{\mathbf{w}}^T\mathbf{x}=\hat{b}+\sum_{m\in \mathcal{S}}\hat{\alpha}_m y_m\mathbf{x}^{(m)^T}\mathbf{x}
$$
**NOTE** this only depends on the scalar product of a subset of traing samples, 
the [[#Support Vectors]] denoted by $\mathcal S$ 




## Soft Margin Classifier

- "soft" = the boundary can be violated
- for situations where there is no solution with a margin $> 0$, see below
- even if there is a Hard Margin solution its not always desired with problems similar to overfitting as the model becomes to specialized (a single sample can drastically change output)

![[soft_margin_data.png]]



Benefits
- more robust to individual samples
- better generalisability



### slack variables

$\large \mathbf{\epsilon}=\begin{pmatrix}\epsilon_1 & \epsilon_2 & \dots & \epsilon_M\end{pmatrix}^T, \epsilon_m\geq0$

Allow individual samples $(x_m, y_m)$ to be on the wronge side of the margin of the hyperplane

Hard constraint $y^{(m)}f(\mathbf{x}^{(m)}) \geq 0$ is replaced with 
$$
y^{(m)}f(\mathbf{x}^{(m)}) \geq 1-\epsilon_m
$$
if $e_m = 0$ -> sample in correct class
	$e_m > 0$ sample on the wrong side



#### Cost function
the new cost function becomes
$$\Large
\underset{b, \mathbf{w}, \mathbf{\epsilon}}{\text{min}}\frac{1}{2}||\mathbf{w}||^2 + C \sum_{m=1}^M\epsilon_m 
$$
$$
\text{subject to }\epsilon_m \geq0, \ y^{(m)}\left( b + \mathbf{w}^T\mathbf{x}^{(m)} \right) \geq 1-\epsilon_m
$$

- only samples on the margin or on the wrong side of the margin afffect the resulting hyperplane
- $C \ge 0$ is a tunable hyperparameter ([[Polynomial Regression#Regularization]])
	- controls how many points are allowed to violate
	- small $C$ -> more violations
	- $C = \infty$  -> no violations (back to [[#Hard / Maximal Margin Classifier]])

Effect of $C$ on the resulting classifier ($C$ increasing from a to d)
![[regularisation_effect.png]]


### Lifting Trick

Projection into higher dimensions

![[lifting_trick.png]]

# Kernel-Trick

- for non linearily separable samples like seen below
![[non_linear_data.png]]

- address the problem by enlarging the feature space using polynomials of the predictors (e.g. $x_1, x_2$) [[#Lifting Trick]]
	- with this the $N$ features $x_1, x_2, \dots, x_N$ could become e.g  **$2N$** features
$$ \large
x_1,x_1^2, x_2,x_2^2, \dots, x_N,x_N^2
$$
- we would then need **TWO** parameter vectors
	- $\mathbf{w}_1=\begin{pmatrix}w_{11} & w_{21} & \cdots & w_{N1}\end{pmatrix}^T$
	- $\mathbf{w}_2=\begin{pmatrix} w_{12} & w_{22} &\cdots & w_{N2}\end{pmatrix}^T$
 - the **cost function** becomes #todo 6.15 seems weird because of the ||w||
$$\large
\underset{b, \mathbf{w}_1, \mathbf{w}_2, \mathbf{\epsilon}}{\text{min}}\frac{1}{2}||\mathbf{w}||^2 + C \sum_{m=1}^M\epsilon_m  \tag{6.15}
$$
$$
\text{subject to }\epsilon_m \geq0, \ y^{(m)}\left( b + \sum_{n=1}^N w_{n1}^T x_n^{(m)} \sum_{n=1}^N w_{n2}^T x_n^{(m)} \right) \geq 1-\epsilon_m
$$

Why does this produce a non-linear boundary?
- in the enlarged feature space $(6.15)$ is in fact linear
	- BUT in the original feature space the boundary is of the form
		$q(x) = 0$	
		where $q$ is a polynomial with generally non-linear solutions	



## Kernels

e.g. the Support Vector Classifier can be calculated as follows: $S$ is the set of all support vectors, $a_m = 0$ for non support $x_m$
$$
\langle \mathbf{x}^{(m)}  , \mathbf{x}^{(m')} \rangle=\sum_{n=1}^N x^{(m)}_n x^{(m')}_n \tag{6.16}
$$
$$
f(\mathbf{x})=b+\sum_{m\in\mathcal{S}} \alpha_m \langle \mathbf{x},\mathbf{x}^{(m)} \rangle \tag{6.18}
$$

Generalizing this leads to 
$$ \large
f(\mathbf{x})=b+\sum_{m\in\mathcal{S}} \alpha_m \mathcal{K}(\mathbf{x},\mathbf{x}^{(m)}) \tag{6.22}
$$

Where $\Large \mathcal{K}$ is the **kernel** 


Example of a Quadratic and a RBF Kernel


![[kernels_ex.png]]


### Polynomial Kernel

- of degree $d > 1$

$$\large
\mathcal{K}(\mathbf{x}^{(m)},\mathbf{x}^{(m')})=\left(1+\sum_{n=1}^N x^{(m)}_n x^{(m')}_n\right)^d \tag{6.21}
$$

### RBF-Kernel

- Radial Basis Function
- results in a raidal classifier
- $\gamma > 0$ constant, inversely proportional to the variance of the gaussian
	$\large \gamma = \frac{1}{2 \sigma^2}$ 
	- Smaller $\gamma$ (larger variance) -> wider spread

$$\large
\mathcal{K}\left(\mathbf{x}^{(m)},\mathbf{x}^{(m')}\right)=\exp\left(-\gamma ||\mathbf{x}^{(m)} -\mathbf{x}^{(m')}||^2 \right). \tag{6.23}
$$

![[common_kernel_function.png]]