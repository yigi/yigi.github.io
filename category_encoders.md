# Encode your Categorical Variables 

**pip3 install category-encoders**

```python
import pandas as pd 
import category_encoders as ce 

# create a Dataframe 
data = pd.DataFrame({ 'gender' : ['Male', 'Female', 'Male', 'Female', 'Female'],
                      'class' : ['A','B','C','D','A'],
                      'city' : ['Delhi','Gurugram','Delhi','Delhi','Gurugram'] }) 
                                                                                      
data.head()
```
<img align="center" width="300" height="200" src="https://i1.wp.com/s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2019/08/dataframe-categorical-feature.png?resize=210%2C171&ssl=1">


```python
# One Hot Encoding 
# create an object of the One Hot Encoder 

ce_OHE = ce.OneHotEncoder(cols=['gender','city']) 

# transform the data 
data = ce_OHE.fit_transform(data) 
data.head()
```
<img align="center" width="300" height="200" src="https://i0.wp.com/s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2019/08/encoded-data.png?resize=331%2C170&ssl=1">



```python
import category_encoders as ce

encoder = ce.BackwardDifferenceEncoder(cols=[...])
encoder = ce.BaseNEncoder(cols=[...])
encoder = ce.BinaryEncoder(cols=[...])
encoder = ce.CatBoostEncoder(cols=[...])
encoder = ce.HashingEncoder(cols=[...])
encoder = ce.HelmertEncoder(cols=[...])
encoder = ce.JamesSteinEncoder(cols=[...])
encoder = ce.LeaveOneOutEncoder(cols=[...])
encoder = ce.MEstimateEncoder(cols=[...])
encoder = ce.OneHotEncoder(cols=[...])
encoder = ce.OrdinalEncoder(cols=[...])
encoder = ce.SumEncoder(cols=[...])
encoder = ce.PolynomialEncoder(cols=[...])
encoder = ce.TargetEncoder(cols=[...])
encoder = ce.WOEEncoder(cols=[...])

encoder.fit(X, y)
X_cleaned = encoder.transform(X_dirty)
```
