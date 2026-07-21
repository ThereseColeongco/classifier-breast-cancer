# Breast Cancer Classifier

This project uses scikit-learn's random forest and the Wisconsin breast cancer dataset to predict whether breast tumor cells are benign or malignant.

## How Random Forests Work

Random forests are made of multiple decision trees. For classification problems like this, the final decision of the random forest is the conclusion that the majority of the trees in the random forest came to. (If it was a regression problem, i.e. one where we need to predict a continuous numerical variable, the final decision of the random forest would be the mean of all the conclusions of the trees in the forest.)

Each tree in a random forest uses a subset of the data. This subset is taken using "random sampling with replacement." Random sampling means you take random columns (features) of random rows (samples/individuals) of data. Replacement means you can have repeated rows (i.e. you can have the same sample appear more than once in a tree, and you can have that same sample appear in other trees) because after a sample is randomly selected from the pool, it is returned to the pool before the next draw; it is "replaced."

These subsets are also called bootstrap datasets. Aggregating the results of these datasets to get the final conclusion (whether it is the majority vote for classification problems or the mean for regression problems) is called bootstrap aggregation aka bagging (this is one kind of ensemble technique).

## How feature selection is done

- Classification: square root of total number of all features = the number of features in each decision tree (e.g. if 15 features are fed into the random forest model, there are 3 or 4 features per decision tree)
- Regression: total number of all features / 3 = the number of features in each decision tree (e.g. if 15 features are fed into the random forest model, there are 5 features per decision tree)

## Splitting methods

- Gini impurity predicts liklihood that a randomly selected example would be incorrectly classified
  - (degree range: 0 to 1, 0 = all elements belong to 1 class, 1 = only 1 class exists, 0.5 = elements are uniformly distributed across classes)
- Information gain - feature is selected that provides the most info about a class; uses entropy
  - Entropy = meausre of randomness or uncertainty in data; lower entropy means easier to make predictions and more likely your predictions will be more accurate

They are called "bootstrap" datasets because the technique comes from the idiom "to pull oneself up by one's bootstraps". In statistics, you draw multiple new samples from a single, original dataset. Because the method creates new data samples using nothing but the data you already have, it metaphorically resembles lifting yourself by your own bootstraps.According to Wikipedia, this name originates from the tall tales of Baron Munchausen, who supposedly pulled himself out of a swamp by his own bootstraps

Sample table of subsets that could be made from the breast tumor cell data:
| Header 1 | Header 2 | Header 3 |
| --- | --- | --- |
| Row 1, Col 1 | Row 1, Col 2 | Row 1, Col 3 |
| Row 2, Col 1 | Row 2, Col 2 | Row 2, Col 3 |

| Header 1 | Header 2 | Header 3 |
| --- | --- | --- |
| Row 1, Col 1 | Row 1, Col 2 | Row 1, Col 3 |
| Row 2, Col 1 | Row 2, Col 2 | Row 2, Col 3 |

| Header 1 | Header 2 | Header 3 |
| --- | --- | --- |
| Row 1, Col 1 | Row 1, Col 2 | Row 1, Col 3 |
| Row 2, Col 1 | Row 2, Col 2 | Row 2, Col 3 |

Ensemble technique (bootstrap aggregation/bagging)
How feature selection is done in classification and regression problems
How best split is chosen
  - based on Gini impurity or Information gain methods.


Root node - training data is fed at root node -> ask T/F at each node to get to next node and ultimately conclusion for the tree. 
Splitting - gini andentropy methods to decide optimal split
Decision node - link to lead node
leaf node - conclusion for tree

## Why Random Forest?

### Pros:
- Low variance because it builds many decision trees on random data subsets and restricts each split in tree to a random subset of features. This makes the model stable, so if the training data changes slightly, the model's predictions will hardly shift, preventing the model from memorizing noise. This makes the model highly generalizable (good accuracy) and reduces overfitting.
- Normalization not needed
- Good accuracy (generalizes well)

The larger the dataset, the deeper a single decision tree becomes, which increases the risk of overfitting.
