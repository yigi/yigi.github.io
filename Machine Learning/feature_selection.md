Feature selection is a process which helps you identify those variables which are statistically relevant. 

## 1 – USING LASSO TO IDENTIFY IMPORTANT FEATURES
Let us see which all variables are the most important features in predicting the house price. For this example, we are using Boston dataset which is available in the sklearn package

```python
# Importing required packages
import numpy as np
 
from sklearn.datasets import load_boston
from sklearn.feature_selection import SelectFromModel
from sklearn.linear_model import LassoCV
 
# Load the boston dataset.
boston = load_boston()
 
# Getting the meta-information
print(boston.DESCR)
```

```python
# Printing the feature names 
print(boston.feature_names)
```

```python
# Getting the data and target variable
X, y = boston['data'], boston['target']
 
# We use the base estimator LassoCV
clf = LassoCV(cv=3)
 
# Set a minimum threshold of 0.70
sfm = SelectFromModel(clf, threshold=0.70)
sfm.fit(X, y)
n_features = sfm.transform(X).shape[1]
 
# Extracting the index of important features
feature_idx = sfm.get_support()
 
# Using the index to print the names of the important variables
boston.feature_names[feature_idx]
```

## 2 – USING RECURSIVE FEATURE ELIMINATION (RFE) METHOD FOR FEATURE SELECTION

The dataset is about flowers, and we use the RFE method to identify which attributes of a flower helps in predicting the species of the flower


```python

# Importing the required packages
from sklearn.datasets import load_iris
from sklearn.linear_model import LogisticRegression
from sklearn.feature_selection import RFE

# loading the iris dataset
iris = load_iris()

# Colleting data for only two flowers and corresponding target variable
x = iris.data[0:99]
y = iris.target[0:99]

# Creating a logistic model object
model = LogisticRegression()

# Identifying top 2 variables our of 4
rfe_model = RFE(model, 2)
rfe_fit = rfe_model.fit(x, y)

# Print the names of the most important features
for feature_list_index in rfe_fit.get_support(indices=True):
    print(iris.feature_names[feature_list_index])
```

So according to our model, ‘sepal width (cm)’ and ‘petal width (cm)’ turned out to be the most important attributes in identifying the Species of the flower.

## 3 – USING RANDOM FOREST FOR FEATURE SELECTION

The random forest algorithm is also among one of the most popular methods used for features selection. The tree-based models are naturally capable of identifying the important variables as they select the variables for classification based on how well they improve the purity of the node

```python
import numpy as np
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.feature_selection import SelectFromModel

# loading the iris dataset
iris = load_iris()

# Colleting data and target variables
x = iris.data
y = iris.target

# Create a random forest classifier
rfc = RandomForestClassifier(random_state = 0, n_jobs = -1)

# Fitting the classifier
rfc.fit(x, y)

# Printing the name of each feature along with the gini value
for feature in zip(feat_labels, rfc.feature_importances_):
    print(feature)
```

Now that we have the Gini index and variable names we can use this information to identify the most critical variables. We can use the below code to print the list of significant variables out of all the variables present in the iris dataset.


```python
# Finally selecting the most important features
sfm = SelectFromModel(rfc, threshold=0.15)
sfm.fit(x, y)
 
# Printing the names of the most important features
for feature_list_index in sfm.get_support(indices=True):
    print(iris.feature_names[feature_list_index])
```

Feature section provides information on the importance and relevance of the features with respect to the contribution of an individual feature to the model. Feature selection process provides other benefits like, it reduces the overfitting problem, improves accuracy, and reduces training time.
