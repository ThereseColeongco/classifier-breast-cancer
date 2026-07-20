# Breast Cancer Classifier

This project uses scikit-learn's random forest and the Wisconsin breast cancer dataset to predict whether breast tumor cells are benign or malignant.

## How Random Forests Work

Random forests are made of multiple decision trees. For classification problems like this, the final decision of the random forest is the conclusion that the majority of the trees in the random forest came to. (If it was a regression problem, i.e. one where we need to predict a continuous numerical variable, the final decision of the random forest would be the mean of all the conclusions of the trees in the forest.)

Each tree in a random forest uses a subset of the data. This subset is taken using "random sampling with replacement." Random sampling means you take random columns (features) of random rows (samples/individuals) of data. Replacement means you can have repeated rows (i.e. you can have the same sample appear more than once in a tree, and you can have that same sample appear in other trees) because after a sample is randomly selected from the pool, it is returned to the pool before the next draw; it is "replaced."

These subsets are also called bootstrap datasets. Aggregating the results of these datasets is called bootstrap aggregation.

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

The larger the dataset, the deeper a single decision tree becomes, which increases the risk of overfitting.
