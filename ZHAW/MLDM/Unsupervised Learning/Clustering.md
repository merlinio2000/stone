**Unsupervised** -> training data has no output (target) values
Goal is to model the underlying distribution of the data $X$
	- problem statement is "fuzzier"
	- evaluation is more difficult

Clustering groups a set of objects in such a way that object int the same group (**cluster**) are more similar (in any sense) to each other than objects in other clusters.
E.g. finding a group of "similar patients" can help identify cancer origins

# Definition

$\large M$ data points $\large X=\{x^{(1)}, x^{(2)}, \ldots, x^{(M)}\}$
$\large n$ features in each data point $\large x^{(i)} = (x_{1}^{(i)}, \ldots, x_{N}^{(i)}) \in \mathbb{R}^{N}$
$\large K$ output clusters
\+ a distance measure $\large d$

A **clustering** is a collection of subsets of **X** (**clusters**)

Similarity in a cluster is determined by having small values for the distance measure $d$



# Clustering Types

## Hard Clustering

each data point belongs to **ONLY** one cluster

we focus on the hard clustering methods [[#K-Means]] and [[#DBSCAN]]
## Soft Clustering

each data point $\large m$ is assigned a probability $\large p_{km}$ that it belongs to cluster $\large k$
For these $\large K$ probabilities the following must hold:
$$\large
\sum_{k=1}^{K}p_{km}=1
$$


# K-Means

https://github.zhaw.ch/pages/doem/mldm_book/09_clustering.html#the-k-means-algorithm

a type of [[#Hard Clustering]]

number of clusters $\large K$ must be predetermined, there is no obvious "correct" answer, see [[#Elbow Method]]

Creates a more or less random **centroid** for each cluster $k$,  $\large C = \{c_1, \ldots, c_K\}$
1. For each data point:
- assign closest centroid
2. For each centroid:
- recompute centroids as mean of all points assigned to it
3. repeat with 1. until convergence
#### Potential Function

quality of [[#K-Means]] is measured using the **potential function** $\Large \Phi$ , (centroids $C$)

measures the squared distance between each data point and its closest centroid

$$\large
\Phi(C, X) = \sum_{m = 1}^{M} min_{c \in C} (d(x^{(m)}, c)^{2})
$$



## Selection of initial centroids

- random points in $\mathbb{R}^{n}$
- **Forgy**-method: choose $K$ random observation from the dataset
- **Random-Partition**-method: puts random points into a cluster and chooses their mean as the centroid
- more sophisticated: [[#K-Means++]]
### K-Means++

- randomly select first centroid from data points
- for each data point
	- compute distance to nearest, previously chosen centroid
- select next centroid from data points such that 
	"the probability of choosing a point as a centroid is directly proportional
	 to its distance to the nearest, previously chosen centroid"
	 -> the point with max distance from the nearest centroid will become the next centroid 
		 -> centroids are spread far appart
- repeat until $K$ centroids were found


## Elbow Method

run [[#K-Means]] with different values of $K$ and plot their [[#Potential Function]]

The value of $K$ where the plot significantly decreases, "where the elbow would be", is a good choice for the number of clusters
	(K = 4 in the example below)
![[clustering_elbow_method.png]]


## Silhouette Method


(might not perform as expected) on ring shaped (non circular in general) groups)

plots the [[#Silhouette Core]] for a range of different $K$ values

Select the one that produces the highest Average Silhouette Score

### Silhouette Core

(higher values are better)
Measure how well the clusters are formed by comparing
- $\large a_m$  the average distance of a point $x_m$ to other points in the cluster
- $\large b_m$  the smallest distance of $x_m$ to all points in any other cluster

Defined as 
$$\large s_m=\frac{b_m-a_m}{max(b_m, a_m)} \in [-1, 1]$$

Average Silhouette Score (Width) = $\large \frac{1}{M}\sum_{m=1}^{M}s_m$

Ideally we wan't smaller $\large a_m$ and larger $\large b_m$ values.
	This means that clusters are dense and far apart from each other



# DBSCAN

https://github.zhaw.ch/pages/doem/mldm_book/09_clustering.html#dbscan

a type of [[#Hard Clustering]], but only **PARTIAL** clustering, noise points will not be assigned

Parameters:
- minPts: threshold of min points to form a cluster
- $\Large \epsilon$: threshold to define max distance for two points to be neighbors
	- point $x$ is **reachable** from $y$ if  distance(x, y) < $\large \epsilon$

Basic idea: Clusters form dense regions and are separated by **relatively** empty areas
- points in the dense region are called **core points**
	-> at least minPts withinin distance $\large \epsilon$  from itself
- **border points** have at least one core point in distance $\large \epsilon$ 
- **noise points** are neither of both






# Distance Metrics

### Manhattan distance (L1)

$\large L_1$ metric
$$\large
d_1(p,q)=\sum_{i}|p_i-q_i|
$$
![[clustering_distance_manhattan.png]]


### Maximum Metric (Linf)

$\large L_{inf}$ 
$$\large
d_{\inf}(p,q)=\max_{i}\{|p_i-q_i|\}
$$

### Cosine similarity

Quantifies similarity among two vectors by only accounting for the angle between them and ignoring their lengths.
Equals the cosine of the angle between the vectors -> orthogonal = 0, proportional = 1, and opposite = -1


$$\large
d_{cos}(p,q)=\frac{\sum_{i=1}^{N}p_iq_i}{\sqrt{\sum_{i=1}^{N}p_{i}^2}\sqrt{\sum_{i=1}^{N}q_{i}^2}}§
$$