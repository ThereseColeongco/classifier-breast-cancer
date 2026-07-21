# Breast Cancer Classifier

This project uses scikit-learn's random forest and the Wisconsin breast cancer dataset to predict whether breast tumor cells are benign or malignant.

## Decision tree jargon
- Root node - training data is fed at root node -> ask T/F at each node to get to next node, rinse and repeat until you get final conclusion for the tree.
- Splitting - mechanism that builds a decision tree (recursive binary splitting); there are several methods we can use to decide the optimal split. The algorithm searches every feature and potential threshold to find the split that maximizes data homogeneity in the resulting child nodes (maximal data homogeneity means the child nodes are most similar to each other). This process repeats top-down until a stopping criterion is met.
- Decision node - a point in a decision tree where a choice must be made or a data attribute is evaluated to split the data into smaller groups
- Leaf node - conclusion for tree

## How Random Forests Work

Random forests are made of multiple decision trees. For classification problems like this, the final decision of the random forest is the conclusion that the majority of the trees in the random forest came to. (If it was a regression problem, i.e. one where we need to predict a continuous numerical variable, the final decision of the random forest would be the mean of all the conclusions of the trees in the forest.)

Each tree in a random forest uses a subset of the data. This subset is taken using "random sampling with replacement." Random sampling means you take random columns (features) of random rows (samples/individuals) of data. Replacement means you can have repeated rows (i.e. you can have the same sample appear more than once in a tree, and you can have that same sample appear in other trees) because after a sample is randomly selected from the pool, it is returned to the pool before the next draw; it is "replaced."

These subsets are also called bootstrap datasets. Aggregating the results of these datasets to get the final conclusion (whether it is the majority vote for classification problems or the mean for regression problems) is called bootstrap aggregation aka bagging (this is one kind of ensemble technique; another popular one used for other models is called boosting). The name "bootstrap" comes from the saying "pull yourself up by your bootstraps" which means to succeed entirely through your own efforts, without relying on outside help. Because you create new datasets using nothing but the data you already have, it's kind of like pulling yourself up by your bootstraps.

## How feature selection is done

- Classification: square root of total number of all features = the number of features in each decision tree (e.g. if 15 features are fed into the random forest model, there are 3 or 4 features per decision tree)
- Regression: total number of all features / 3 = the number of features in each decision tree (e.g. if 15 features are fed into the random forest model, there are 5 features per decision tree)

## Some commonly used splitting methods

- Gini impurity (default on RandomForestClassifier from sklearn) predicts liklihood that a randomly selected example would be incorrectly classified by a specific node
  - degree range: 0 to 1, 0 = all elements belong to 1 class, 1 = only 1 class exists, 0.5 = elements are uniformly distributed across classes
- Information gain = difference in entropy before and after split; feature is selected that provides the most info about a class
  - Entropy = measure of randomness or uncertainty in data
    - As you move from root node to leaf node, entropy of the data decreases as you eliminate certain possibilities as you go down the tree. Lower entropy means easier to make predictions and more likely your predictions will be more accurate.

## Why Random Forest?

### Pros:
The larger the dataset, the deeper a single decision tree becomes, which increases the risk of overfitting. However, with multiple decision trees built on random data subsets and by restricting each split in the tree to a random subset of features, you get low variance. This makes the model stable, so if the training data changes slightly, the model's predictions will hardly shift, preventing the model from memorizing noise. This makes the model highly generalizable (good accuracy) and reduces overfitting. Additionally, because decision trees work based on thresholds and sorting rather than calculating spatial distances or gradients, you don't need to scale the data (i.e. normalize it) before feeding it into the model. If you were to compare how the scaled and unscaled features affect model performance, there is no difference.

### Cons:
- More training time required because you have many decision trees to make
- Interpretation becomes complex with multiple decision trees. (interpretation, i.e. where does splitting occur, what features are being selected, which features are the ones that lead to the final conclusion?)
- More trees require more memory to be used
- Training and storing multiple decision trees -> computationally expensive
