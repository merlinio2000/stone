### General Principle of Ensemble Methods

![[rand_forest_ensemble.png]]


# Random Forests

an Ensemble Method [[#General Principle of Ensemble Methods]] based on [[Decision Trees]]

The individual models need to be **independent** of eachother, see [[#Bagging]]

## Bagging

**B**ootstrapping the data during training
\+ **AGG**regat**ING**
![[rand_forest_bagging.png]]


#todo Out-of-Bag Error


### Hyperparameters

In addition to normal decision trees:
- number of sub-models (trees/estimators)
- sample size: fraction of samples for each sub tree