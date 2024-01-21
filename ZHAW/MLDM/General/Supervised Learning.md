

## Feature Vector

- relevant properties of the input data
- usually n-dim vector of numbers

### Representation of different Data

see also [[Encoding]]

#### Images
- 2D Array of grayscale pixels
- 3D Array of pixels + their R, G & B values

#### Audio: Mel Frequency Cepstral Coefficients (MFCC)

Split long wave into window and then using Discrete Cosine Transform represent energy patterns

#### Text: Bag of Words (BoW)
- Define an Index for each word
- Store the number of occurences of that word at the designated index



## Algorithm Selection

No free lunch theorem **NFL** -> there is no universally best learner across problems

### Quality Measures

#### Accuracy
see [[Classification (Logistic Regression)#Proportion-Correct Accuracy]]

#### Precision

Percentage of positively predicted examples that actually were positive
$$
\textrm{precision} = \frac{PredictedPositive \; \cap \; ActualPositive}{PredictedPositive}
$$
#### Recall

Percentage of positive examples that the model also predicted as positive

$$
\textrm{recall} = \frac{PredictedPositive \; \cap \; ActualPositive}{ActualPositive}
$$


#### Precision-Recall Curve

Vary threshold over $[0, 1]$ gives precision-recall curve.
A perfect model would follow the top and right edge (1.0)


![[precision recall curve.png]]




#### F-Score

Combines precision and recall for a given threshold $\tau$
$$\large
F_\beta = (1 + \beta^2) * \frac{precision * recall}{(\beta^2 * precision*) + recall} 
$$


The value of $\beta$ can be used to influence the importance of precision / recall on the score.
With $\beta = 1$ both are weighted equally, known as **F1** score.






## Data Partitioning

- Training
- Validation: for Hyperparam optimization
- Test: validate chosen model

#### Fixed data splits

e.g. 80% training and 20% testing

#### k-fold Cross Validation (CV)

for smaller datasets, needs to run iteratively

Data gets divided into $k$ folds and then we rotate which fold we use for testing and which for training.