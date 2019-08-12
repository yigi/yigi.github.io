## !!!do not use the main dataset for manipulation. make subsets of it

### missing data
```python
from sklearn.preprocessing import Imputer
imputer = Imputer(missing_values = 'NaN'
		 ,strategy = 'mean'
		 ,axis = 0) #impute along columns
imputer = imputer.fit(dataset[:,1:3] #since the NaN values in the 1st and 2nd
dataset[:,1:3] = imputer.transform(dataset[:,1:3])
```
### encoding categorical data
```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder = LabelEncoder()
dataset[:,0] = labelencoder.fit_transform(dataset[:,0])

onehotencoder = OneHotEncoder(categorical_features = [0])
dataset = onehotencoder.fit_transform(dataset).toarray()
```
### split data set into test/training
```python
think you have 4 columns and first 3 is the independent (X) and the last is dependent (y)
from sklearn.cross_validation import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 0 ) # 2 test 8 training 
```

### feature scaling
```python
from sklearn.preprocessing import StandarScaler
scaler_X = StandarScaler()
X_train = scaler_X.fit_transform(X_train)
X_test = scaler_X.fit_transform(X_test)
```

____________________________________________________________________________________________
# and fit your model with Linear Regression

### fitting linear regression to the training set
```python
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit( X_train, y_train )
```
### predicting the test set result
```python
y_pred = regressor.predict(X_test)
```
### visualize the training set result
```python
plt.scatter(X_train, y_train, color = 'red' )
plt.plot(X_train, regressor.predict(X_train), color = 'blue')
plt.title('Salary vs Experience')
plt.xlabel('Years of Experience')
plt.ylabel('Salary')
plt.show()
```
### visualize the test set result,
```python
plt.scatter(X_test, y_test, color = 'red' )
plt.plot(X_train, regressor.predict(X_train), color = 'blue')
plt.title('Salary vs Experience')
plt.xlabel('Years of Experience')
plt.ylabel('Salary')
plt.show()
```

# you dont need to do feature scaling and dummy variable trap. library handles it.
