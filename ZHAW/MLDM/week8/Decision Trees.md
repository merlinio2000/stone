- classification & regression
- split-nodes & leaf-nodes
- **gini**: Measures the nodes [[#Gini Impurity]] 
- value: how many training samples of which class are in this class?

![[decision_tree_ex.png]]

The estimated probabilites when reaching the green node would be: ($54 = 49 + 5$)
- Setosa: $0/54 = 0$
- Versicolor: $49/54$
- Virginica: $5/54$

# Impurity Measures For Classification

- data at node $\large i$: $\large Q_i$, consisting of $\large M_i$ samples
- target is a classification outcome on values $\large k=1,2,\dots,K$
- proportion of class $\large k$ for node $i$:
$$\Large
p_{ik} = \frac{1}{M_i}\sum_{y\in Q_i} I(y=k)
$$
- if $\large i$ is a **leaf node**, $\large p_{ik}$ is the predicted probability


## Gini Impurity
"how distinctly separated is this node?"
- measures probability of misclassification
- $\in [0, 0.5]$
- a node is **pure** ($gini=0$) if all training instances it applies to belong to the same class
- the root node is maximally **impure**, each of the three classes is present

By default scikit-learn measures gini impurity using
$$\large 
G\left(Q_i\right)=1-\sum_{k=1}^K p_{i,k}^2 \tag{7.1}
$$


## Entropy

$$\large
H\left(Q_i\right)=-\sum_{k=1}^K p_{i,k} \log_2 p_{i,k} \tag{7.2}
$$
- gini impurity and entropy behave similarly:
	- $=0$ if all samples in same class
	- maximum at $p = 0.5$
- gini impurity is slightly faster thus a better default



# Classification Trees

- Classification and Regression Tree (**CART**)
- produces only binary trees
- greedy algorithm (not guaranteed optimal)
	- operates top-down and doesnt later check if there could maybe be a better solution

## Training classification trees
![[proc_train_decision_tree.png]]

- start at depth=0 with a root node $\Large Q_{i=0}$
- split training set into 2 subsets using a single feature $\large n$ and threshold $\large t_i$
- $\large (n, t_i)$ get chosen by the pair that produces the purest subsets (weighted by size)
- recursively split subsets and repeat until:
	- max_depth is reached
	- $M_i < \mathrm{min_{samples}}$  
	- $M_i = 1$

#### finding ideal (n, t_i)
- sort all unique values of features $\large n$ among the samples at node $\large i$
- calculate midpoints between adjacent values
	- evaluate each midpoint in a candidate split $\Large \theta = (n, t_i)$

$$\Large
Q_i^{\text{left}}(\theta) = \{(x,y)| x_n \leq t_i \} \ \text{ and } \ Q_i^{\text{right}}(\theta) = Q_i \setminus Q_i^{\text{left}}(\theta)
$$
- in each split the $\theta = (n, t_i)$ that minimize the [[#cost function]] are selected
$$\large
\theta^\ast=\text{argmin}_\theta J(Q_i,\theta)
$$

### cost function

To evaluate candidate split $\theta$ from [[#finding ideal (n, t_i)]]
Weighted average of impurities from the left & right side
(note: by default scikit uses [[#Gini Impurity]] (G), [[#Entropy]] (H) could also be used)

$$\Large
J(Q_i,\theta)=\frac{m^{\text{left}}_i}{m_i}G\left(Q^{\text{left}}_i\left(\theta\right)\right) + \frac{m^{\text{right}}_i}{m_i}G\left(Q^{\text{right}}_i\left(\theta\right)\right) \tag{7.3}
$$



# Regression Trees

main difference to [[#Classification Trees]] :
instead of predicting a class, each leaf predicts a continuous value
This value prediciton is the **average** target value of the training samples associated with this leaf node. ("mean squared error" is also taken over these samples)

![[regression_tree_ex.png]]


The figures below represent the predictions as the red line with max_depth = 2 & 3
![[regression_tree_max_depth_ex.png]]


## Training Regression Trees

analogous to [[#Training classification trees]]
BUT instead of an impurity metric the Mean Squared Error **MSE** is used

$$\large
MSE(Q_i)=\frac{1}{M_i}\sum_{y\in Q_i} \left(y-\bar{y}_i\right)^2  \tag{7.4}
$$
with
$$\large
\bar{y}_i=\frac{1}{M_i}\sum_{y\in Q_i} y
$$



# Regularization

- decision trees make **NO** assumptions (like linearity) about the data
- thus if left unconstrained the tree will adapt to the data, fitting very closely possibly even overfitting
	- models like this are called **nonparametric** because the number of parameters are not determined prior to training
	- in contrast parametric models like linear regression have a predetermined number of parameters thus are restricted in their fit limiting the possibility for overfitting


To avoid overfitting in decision trees the freedom needs to be restricted (called **regularization**)
In scikit-learn a few hyperparams control stopping conditions which will restrict the maximum depth of the tree which regularizes the model

Increasing `min_` / decreasing `max_` variables increases regularization

- max_depth, maximum depth of the tree
- min_samples_split, minimum samples in a node before it can be split
- min_samples_leaf, minimum samples a leaf needs to be created
- min_weight_fraction_lef, min_samples_leaf but as a fraction of the total number of weighted instances
- max_leaf_nodes, maximum leaf nodes
- max_features, maximum number of features that are evaluated for splitting at each node

#### example min_samples_leaf (classification)
![[min_samples_leaf_class_ex.png]]


#### example min_samples_leaf (regression)

![[min_samples_leaf_regression_ex.png]]






# Misc: White- vs Black-Box Algorithms

The prediction of a decision tree is easy to reason about (decisions can be followed top-to-bottom). Models like this are called **White-Box Models**

On the other hand models like random forests and neural networks are called **Black-Box Models** because even though you can check the calculations made it is usually hard to explain **WHY** the predictions were made.
Example Person detection: did the model detect the eyes, the nose, ...?

