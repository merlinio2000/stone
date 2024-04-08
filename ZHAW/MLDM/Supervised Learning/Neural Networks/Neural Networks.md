!!! when this lecture talks about **neural networks**, 
[[#Feed-forward Neural Networks]] are **ACTUALLY** referred to 

# Multiclass Classification

generalization of [[Classification (Logistic Regression)]]
# Softmax

## Softmax Function
$$\large
softmax(\mathbf{z})_k=\dfrac{\exp{(z_k)}}{\sum_{i=1}^{K}\exp{(z_i)}}
$$
Note: $softmax(z)$ is a vector -> $softmax(z)_k$ is the $k$-th component
- scales values onto the Interval $[0, 1]$ so they sum up to one
- returns probabilities that target sample $x^m$ belongs to one of the $K$ classes

### Softmax Cost Function (Cross Entropy Loss)

**Loss Function:**
$y^{(m)}$ = true label, $\hat{y}^{(m)}$  = predicted label
$$\large
\textrm{Loss}(\hat{\mathbf{y}}^{(m)}, \mathbf{y}^{(m)}) = - \sum_{k=1}^{K}{y_k^{(m)} \log(\hat{y}_{k}^{(m)})}
$$
**Cost Function:**
average of the cross entropy loss over all training samples
$$
J(\mathbf{W}) = \frac{1}{M} \sum_{m=1}^M \textrm{Loss}(\hat{\mathbf{y}}_{m}, \mathbf{y}_m)
$$
or more explicit: ($c_m$ is the correct label for the sample)
$$\Large
L_{CE}=-\sum_{m=1}^{M}\sum_{k=1}^{K}y^{(m)}_k log(\hat{y}^{(m)}_k)=-\sum_{m=1}^{M}log\frac{\exp{(\mathbf{w}^T_{c_m}\mathbf{x}^{(m)})}}{\sum_{k=1}^{K}\exp{(\mathbf{w}^T_k\mathbf{x}^{(m)})}}
$$


## Softmax Regression

given samples $\{(\mathbf{x}^{(1)}, \mathbf{y}^{(1)}), (\mathbf{x}^{(2)}, \mathbf{y}^{(2)}), \dots, (\mathbf{x}^{(M)}, \mathbf{y}^{(M)})\}$
where $y^{(i)}$ is one of $K$ classes.

Optimum determined using [[Gradient Descent]]

Encoding:

In this regression the label $y^{(i)}$ is now a $K \times 1$ binary vectory encoing the label of sample $i$.
Example: if we have three classes $\set{1, 2, 3}$, and the first sample belongs to class $2$ then its label will be  $\mathbf{y}^{(i)}=[0,1,0]$
See also: [[Encoding#One-Hot Encoding]]

Output:
In contrast to logistic regression which predicts the probabiltity of a binary outcome
![[log_reg_rep.png]]
Softmax regression generalizes this to predict a probability for each class
![[softmax_reg.png]]


### Softmax Layer

For multiclass-classifcation the network as $N$ input nodes as well as **K** output nodes.
The Softmax Layer calculates the predictions based on the output nodes of the network


# Feed-forward Neural Networks

## Neuron

output is linear combination of inputs & weights + bias -> [[#Activation Functions]]

The model parameters are the bias and weights for each neuron

![[neuron.png]]


### Layers

[[#Neuron]]s are grouped into layers, first layer = input, last layer = output.
All the layers in between = hidden layers. The number of hidden layers is called **depth** of the model

In feed-forward networks all neurons from the previous layer are connected to the neurons from the next layer. **Fully Connected**
No connections between neurons in the same layer or cycles
-> Information only moves "forward"



## Activation Functions

Function using linear combination of inputs applied in each [[#Neuron]]
The activation function in all [[#Layers]] but the last one for regression (output layer)
is typically a non linear function.
If all functions were linear -> the resulting model would also be linear
Overview of most common functions

![[activation_function.png]]

Example: the mapping for a small network with single input, single output and 3 neurons is defined as:

$$\large
\hat{y}=f[x, \mathbf{\phi}]=\phi_0+\phi_1 a[w_{10}+w_{11}x]+\phi_2 a[w_{20}+w_{21}x]+\phi_3 a[w_{30}+w_{31}x]
$$

Where $\mathbf{\phi}=\{\phi_0, \phi_1, \phi_2, \phi_3, w_{10}, w_{11}, w_{20}, w_{21}, w_{30}, w_{31}\}$ are the **model parameters**
- $a$ is the activation function
- $h_i=a[w_{i0}+w_{i1}] \qquad \forall i \in \{1,2,3\}$ 

![[activation_function_map.png]]



## Cost Function

Depends on the underlying problem.
<span style="color:red">!! NOT CONVEX like linear regression !!</span>
**NO** guarantee that we actually find the global minimum

**Regression**: Mean Squared Error MSE
$$
MSE = \frac{1}{M}\sum_{m=1}^{M}(y^{(m)}-\hat{y}^{(m)})^2
$$
**Binary Classifcation**: Logistic Cost Function [[Classification (Logistic Regression)#Loss function]]
$$
L_{logistic}=-\sum_{m=1}^{M}[y^{(m)}log(\hat{y}^{(m)})+(1-y^{(m)})log(1-\hat{y}^{(m)})]
$$

**Multiclass Classification**: [[#Softmax Cost Function (Cross Entropy Loss)]]



## Training Feed-forward

minimization computed using [[Gradient Descent]] 
1.  initialize network parameters randomly
2.  **compute gradient of cost** function with respect to each of the models parameters
3. **adjust model parameters** by small step (learning rate $\alpha$) in the opposite direction of the gradient
$$\large
\mathbf{w} = \mathbf{w} - \alpha \frac{\partial L}{\partial \mathbf{w}}
$$
The gradient of the loss is computed starting from the last layer back towards the first layer -> called **Backpropagtion**


![[feed_forward_training.png]]


### Training in Practice

in practice **mini-batch** gradient descent algorithms are used [[Gradient Descent#Mini-batch Gradient Descent]]
- batch size: the number of training samples per batch
- iteration: completing forward & backpropagation pass for batch
- epoch: after iteration is complete for all batches


# (Logistic) Regression using Neural Networks 

For regression (e.g. price of a house, binary classification) the output is a single node corresponding to the prediction
![[neural_network_for_regression.png]]

Same goes for **binary classification**, output is a single node computed using the logistic sigmoid
[[Classification (Logistic Regression)#Sigmoid / Linear Regression based Classification]]

For multiclass the [[#Softmax Layer]] handles this
![[feed_forward_pred_layer.png]]









# Universality Theorem
Hornik, 1991

**Proof sketch for one-dimensional input**: A neural network with one input, one output, and one hidden layer with two neurons and sigmoid activation function, can approximate a step function. Recall that having very large weight in the sigmoid function makes the function very steep (left-most figure in [Figure 8.12](https://github.zhaw.ch/pages/doem/mldm_book/08_neural_networks#fig-nn-step-fn) showing output of top neuron). The bias (offset) weight moves the step from the origin to the left or right (middle figure in [Figure 8.12](https://github.zhaw.ch/pages/doem/mldm_book/08_neural_networks#fig-nn-step-fn) showing output of top neuron). By having an additional neuron with a negative weight to the output layer and same magnitude as the top neuron, we get a bar with height equal to the magnitude of the weight (right-most figure in [Figure 8.12](https://github.zhaw.ch/pages/doem/mldm_book/08_neural_networks#fig-nn-step-fn) showing the output for the bottom neuron).
![[universality_theorem.png]]

Since any continuous function can be represented by infinitely small rectangles (integration) it is obvious that these functions can be represented by an arbitrary number of neurons





# Backpropagation

Based on the **chain rule for partial derivatives** 
![[chain_rule_part_deriv.png]]

## Example on model with one neuron per layer

**NOTE** usually the derivatives are averaged over all training samples because the cost function is computed as the average of the individual costs over all training samples

based on the following model:
![[backprop_ex_single.png]]

- Training data is one sample with (in, out) = $(x, y)$
- $L$ layers, each one neuron
- input node $a^{(0)}$ is not a neuron, it only passes the value into the network
- neuron of last layer produces output $\hat{y} = a^{(L)}$
- each neuron in layers calculates the linearfunction (preactivation)
$$
z^{(L)} = w^{(L)}\cdot a^{(L-1)} + b^{(L)}
$$
- [[#Activation Functions]] $\sigma$ (e.g. Sigmoid)
$$
a^{(L)}=\sigma(z^{(L)}) = \frac{1}{1+e^{-z^{(L)}}} = \left(1+e^{-z^{(L)}}\right)^{-1}
$$
- Cost function, for simplicity squared error
$$
C:C\left(x,y;w^{(1)},b^{(1)},w^{(2)},b^{(2)},...,w^{(L)},b^{(L)}\right)
$$
$$
C = \left(y-a^{(L)}\right)^2
$$

As the name BACKpropagation implies we start from the back

### first layer

![[backprop_ex_back.png]]

applying the chain rule:
$$\large
\frac{\partial C}{\partial w^{(L)}} = \frac{\partial C}{\partial a^{(L)}} \cdot \frac{\partial a^{(L)}}{\partial z^{(L)}} \cdot \frac{\partial z^{(L)}}{\partial w^{(L)}}
$$
deriving these 3 expressions (**by w**)
first: cost function
$$\large
\frac{\partial C}{\partial a^{(L)}} = -2\left(y-a^{(L)}\right) = 2\left(a^{(L)} - y\right)
$$

second: derive activation function 
$$\large
\begin{split}
\frac{\partial a^{(L)}}{\partial z^{(L)}} = \sigma'(z^{(L)})  &= \frac{\partial }{\partial w^{(L)}} \left(1+e^{-z^{(L)}}\right)^{-1} = (-1) e^{-z^{(L)}} (-1) \left(1+e^{-z^{(L)}}\right)^{-2} =  \frac{e^{-z^{(L)}}}{(1+e^{-z^{(L)}})^2} \\
&=\frac{1}{1+e^{-z^{(L)}}} \cdot \frac{e^{-z^{(L)}} + 1 - 1}{1+e^{-z^{(L)}}} =\frac{1}{1+e^{-z^{(L)}}} \left( \frac{1+e^{-z^{(L)}}}{1+e^{-z^{(L)}}} - \frac{1}{1+e^{-z^{(L)}}} \right) \\
&=\frac{1}{1+e^{-z^{(L)}}} \left( 1- \frac{1}{1+e^{-z^{(L)}}}\right) = \sigma(z^{(L)}) \left(1 - \sigma(z^{(L)}) \right)
\end{split}
$$

third: partial derivative of $z$ in repsect to weight $w$
$$\large
\frac{\partial z^{(L)}}{\partial w^{(L)}} = a^{(L-1)}
$$
**combining all three**
$$\Large
\frac{\partial C}{\partial w^{(L)}} = \underbrace{2\left(a^{(L)} - y\right)}_{\frac{\partial C}{\partial{a^{(L)}}}} \cdot \underbrace{\sigma(z^{(L)}) \left(1 - \sigma(z^{(L)}) \right)}_{\frac{\partial a^{(L)}}{\partial z^{(L)}}} \cdot \underbrace{a^{(L-1)}}_{\frac{\partial z^{(L)}}{\partial w^{(L)}}}
$$


**now repeat but paritally derive by the bias b**

(blue can be reused)
$$\large
\frac{\partial C}{\partial b^{(L)}} =
{\color{blue}\frac{\partial C}{\partial a^{(L)}} }
\cdot {\color{blue}\frac{\partial a^{(L)}}{\partial z^{(L)}} }
\cdot \frac{\partial z^{(L)}}{\partial b^{(L)}}
$$


third: activation function in respect to bias
$$\large
\frac{\partial z^{(L)}}{\partial b^{(L)}} = \frac{\partial }{\partial b^{(L)}} \left( w^{(L)}\cdot a^{(L-1)} + b^{(L)} \right) = 1
$$


**again combined**
$$\Large
\frac{\partial C}{\partial b^{(L)}} = {\color{blue} 2\left(a^{(L)} - y\right) \cdot \sigma(z^{(L)}) \left(1 - \sigma(z^{(L)}) \right) } \cdot 1
$$

### following layers

![[backprop_ex_2nd.png]]

again partially derive by weight w, blue terms are reused
$$\large
\frac{\partial C}{\partial w^{(L-1)}} =
{\color{blue} \frac{\partial C}{\partial a^{(L)}} }
\cdot {\color{blue} \frac{\partial a^{(L)}}{\partial z^{(L)}} }
\cdot \frac{\partial z^{(L)}}{\partial a^{(L-1)}}
\cdot \frac{\partial a^{(L-1)}}{\partial z^{(L-1)}}
\cdot \frac{\partial z^{(L-1)}}{\partial w^{(L-1)}}
$$

preactivation z in last layer in respect to activation in this layer
$$\large
\frac{\partial z^{(L)}}{\partial a^{(L-1)}} = w^{(L)}
$$
activation function for this layer:
$$\large
\frac{\partial a^{(L-1)}}{\partial z^{(L-1)}} = \sigma\left(z^{(L-1)}\right) \left(1 - \sigma\left(z^{(L-1)}\right) \right)
$$
preactivation for this layer in repsect to weight
$$\large
\frac{\partial z^{(L-1)}}{\partial w^{(L-1)}} = a^{(L-2)}
$$

resulting in the **combined** Cost functions in respect to
weight:
$$\Large
\frac{\partial C}{\partial w^{(L-1)}} =
{\color{blue}
2\left(a^{(L)} - y\right) \cdot \sigma(z^{(L)}) \left(1 - \sigma(z^{(L)}) \right)
}
\cdot w^{(L)}
\cdot \sigma\left(z^{(L-1)}\right) \left(1 - \sigma\left(z^{(L-1)}\right) \right)
\cdot a^{(L-2)}
$$ and bias:
$$\Large
\frac{\partial C}{\partial b^{(L-1)}} =
{\color{blue}
2\left(a^{(L)} - y\right) \cdot \sigma(z^{(L)}) \left(1 - \sigma(z^{(L)}) \right)
\cdot w^{(L)}
\cdot \sigma\left(z^{(L-1)}\right) \left(1 - \sigma\left(z^{(L-1)}\right) \right)
}
\cdot 1
$$



Continuing with layer $L - 2$...
$$\Large
\frac{\partial C}{\partial w^{(L-2)}} =
{\color{blue} \frac{\partial C}{\partial a^{(L)}} }
\cdot {\color{blue} \frac{\partial a^{(L)}}{\partial z^{(L)}}  
\cdot \frac{\partial z^{(L)}}{\partial a^{(L-1)}}
\cdot \frac{\partial a^{(L-1)}}{\partial z^{(L-1)}}
}
\cdot \frac{\partial z^{(L-1)}}{\partial a^{(L-2)}}
\cdot \frac{\partial a^{(L-2)}}{\partial z^{(L-2)}}
\cdot \frac{\partial z^{(L-2)}}{\partial w^{(L-2)}}
$$
$$\Large
\frac{\partial C}{\partial b^{(L-2)}} =
{\color{blue} \frac{\partial C}{\partial a^{(L)}} }
\cdot {\color{blue} \frac{\partial a^{(L)}}{\partial z^{(L)}}  
\cdot \frac{\partial z^{(L)}}{\partial a^{(L-1)}}
\cdot \frac{\partial a^{(L-1)}}{\partial z^{(L-1)}}
\cdot \frac{\partial z^{(L-1)}}{\partial a^{(L-2)}}
\cdot \frac{\partial a^{(L-2)}}{\partial z^{(L-2)}}
}
\cdot \frac{\partial z^{(L-2)}}{\partial b^{(L-2)}}
$$



## Backpropagation with Multiple Neurons

![[backprop_multiple_neurons.png]]


## Vanishing & Exploding Gradient Problem

- happens especially for many hidden layers
- long chains of multiplications can cause the gradient to numerically "explode"


## Dealing With Overfitting

### Dropout

- in each training iteration a percentage of neurons (with their connections) are **temporarily** deactivated/ignored
- next iteration ignores a different subset
- avoids the model relying too heavily on certain neurons
- typical ranges: 20-50%

### Early Stopping

- periodically evaluate performance (e.g. all 5 epochs) on the validation set
- if performance on the validation starts to decrease -> indicates overfitting
- training will be stopped early in this case

### Data Augmentation

- gain more training data without gathering data
- do so through **meaningful** transformations 
	- crop / resize / flip image
	- add random noise
	- synonym replacement for text
	- translation between languages


