Feature selection is a technique where we choose those features in our data that contribute most to the target variable. In other words we choose the best predictors for the target variable.

The classes in the sklearn.feature_selection module can be used for feature selection/dimensionality reduction on sample sets, either to improve estimators’ accuracy scores or to boost their performance on very high-dimensional datasets.

### Important

Reduces Overfitting: Less redundant data means less possibility of making decisions based on redundant data/noise.
Improves Accuracy: Less misleading data means modeling accuracy improves.
Reduces Training Time: Less data means that algorithms train faster.

```python
#Imports
import pandas as pd
import numpy as np
```

```python
# Load the data
data_clf=pd.read_csv('../input/iris/Iris.csv') # for classification problem
data_reg=pd.read_csv('../input/50-startups/50_Startups.csv') # for regression problem
```

```python
# Check first five datapoints by using head() method
print(data_clf.head(2))
print(data_reg.head(2))
```

```python
   Id  SepalLengthCm     ...       PetalWidthCm      Species
0   1            5.1     ...                0.2  Iris-setosa
1   2            4.9     ...                0.2  Iris-setosa

[2 rows x 6 columns]
   R&D Spend  Administration  Marketing Spend       State     Profit
0   165349.2       136897.80        471784.10    New York  192261.83
1   162597.7       151377.59        443898.53  California  191792.06
```

```python
# Create feature and target variable for Classification problem
X_clf=data_clf.iloc[:,1:5] # features: SepalLengthCm', 'SepalWidthCm', 'PetalLengthCm', 'PetalWidthCm'
y_clf=data_clf.iloc[:,5] # Target variable: Iris species
```

```python
# Create feature and target variable for Regression problem
X_reg=data_reg.iloc[:,0:3] # features: R&D Spend, Administration, Marketing Spend
# I have not considered 'State' in feature set. You can use it after label encoding.
y_reg=data_reg.iloc[:,4] # Target variable: Profit
```

Feature selection method: SelectKBest

Score function:
For regression: f_regression, mutual_info_regression
For classification: chi2, f_classif, mutual_info_classif



```python
# Import SelectKBest, chi2(score function for classification), f_regression (score function for regression)
from sklearn.feature_selection import SelectKBest, chi2, f_regression
```

```python
# Create the object for SelectKBest and fit and transform the classification data
# k is the number of features you want to select [here it's 2]
X_clf_new=SelectKBest(score_func=chi2,k=2).fit_transform(X_clf,y_clf)
```

```python
# Check the newly created variable for top two best features
print(X_clf_new[:5])
[[1.4 0.2]
 [1.4 0.2]
 [1.3 0.2]
 [1.5 0.2]
 [1.4 0.2]]
```
From the above we see that the best two predictors for Iris species are:

PetalLengthCm
PetalWidthCm


```python
# Create the object for SelectKBest and fit and transform the regression data
X_reg_new=SelectKBest(score_func=f_regression, k=2).fit_transform(X_reg,y_reg)
```

```python
# Check the newly created variable for top two best features
print(X_reg_new[:5])
[[165349.2  471784.1 ]
 [162597.7  443898.53]
 [153441.51 407934.54]
 [144372.41 383199.62]
 [142107.34 366168.42]]
```


From the above we see that the best two predictors for start up profit are:

R&D Spend
Marketing Spend
