### backward elimination
think we have 4 columned model.  1 0 23424 31333 313 423143

```python
import statsmodel.formula.api as sm
X = np.append(arr = np.ones(50,1)).astype(int), values = X, axis = 1)
X_opt = X[:, [0,1,2,3,4,5]]
regressor_OLS = sm.OLS( endog = y, exog = X_opt ).fit() #ordinary least squares
regressor_OLS.summary()
X_opt = X[:, [0,1,2,4,5]]
regressor_OLS = sm.OLS( endog = y, exog = X_opt ).fit() #ordinary least squares
regressor_OLS.summary()
X_opt = X[:, [0,1,4,5]]
regressor_OLS = sm.OLS( endog = y, exog = X_opt ).fit() #ordinary least squares
regressor_OLS.summary()
#since p is over 0.005
```
