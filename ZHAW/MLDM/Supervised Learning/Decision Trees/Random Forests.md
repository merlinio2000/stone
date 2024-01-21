### General Principle of Ensemble Methods

![[rand_forest_ensemble.png]]


# Random Forests

an Ensemble Method [[#General Principle of Ensemble Methods]] based on [[Decision Trees]]

The individual models need to be **independent** of eachother, see [[#Bagging]]

## Bagging

**B**ootstrapping the data during training
\+ **AGG**regat**ING**
![[rand_forest_bagging.png]]


## Out-of-Bag Error

- out-of-bag (OOB): samples that were not used for training this specific sub-model
- OOB Error: proportion of OOB samples that were incorrectly classified

![[out_of_bag_error.png]]

### Hyperparameters

In addition to normal decision trees:
- number of sub-models (trees/estimators)
- sample size: fraction of samples for each sub tree