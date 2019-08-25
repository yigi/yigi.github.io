The cumulative accuracy profile (CAP) is used in data science to visualize the discriminative power of a model. 

```python
#importing libraries
import numpy as np
import pandas as pd
from matplotlib import cm

#loading the dataset
dataset = pd.read_csv('dataset-4.csv')
#X = dataset.iloc[:,0:6].values
X = dataset.iloc[:,0:3].values
y = dataset.iloc[:,len(dataset.iloc[0])-1].values

#train/test
from sklearn.cross_validation import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=1)

#fitting the classifier to the training set
from sklearn.ensemble import RandomForestClassifier
classifier = RandomForestClassifier(n_estimators = 100, criterion='entropy', random_state=0)
classifier.fit(X_train, y_train)


Then we create the CAP Curve with the following code :

y_pred_proba = classifier.predict_proba(X=X_test)
capcurve(y_values=y_test, y_preds_proba=y_pred_proba[:,1])

The ‘capcurve’ function that builds and shows the CAP curve is defined as follows :

import matplotlib.pyplot as plt
from scipy import integrate
def capcurve(y_values, y_preds_proba):
num_pos_obs = np.sum(y_values)
num_count = len(y_values)
rate_pos_obs = float(num_pos_obs) / float(num_count)
ideal = pd.DataFrame({'x':[0,rate_pos_obs,1],'y':[0,1,1]})
xx = np.arange(num_count) / float(num_count - 1)

y_cap = np.c_[y_values,y_preds_proba]
y_cap_df_s = pd.DataFrame(data=y_cap)
y_cap_df_s = y_cap_df_s.sort_values([1], ascending=False).reset_index('index', drop=True)

print(y_cap_df_s.head(20))

yy = np.cumsum(y_cap_df_s[0]) / float(num_pos_obs)
yy = np.append([0], yy[0:num_count-1]) #add the first curve point (0,0) : for xx=0 we have yy=0

percent = 0.5
row_index = np.trunc(num_count * percent)

val_y1 = yy[row_index]
val_y2 = yy[row_index+1]
if val_y1 == val_y2:
val = val_y1*1.0
else:
val_x1 = xx[row_index]
val_x2 = xx[row_index+1]
val = val_y1 + ((val_x2 - percent)/(val_x2 - val_x1))*(val_y2 - val_y1)

sigma_ideal = 1 * xx[num_pos_obs - 1 ] / 2 + (xx[num_count - 1] - xx[num_pos_obs]) * 1
sigma_model = integrate.simps(yy,xx)
sigma_random = integrate.simps(xx,xx)

ar_value = (sigma_model - sigma_random) / (sigma_ideal - sigma_random)
#ar_label = 'ar value = %s' % ar_value

fig, ax = plt.subplots(nrows = 1, ncols = 1)
ax.plot(ideal['x'],ideal['y'], color='grey', label='Perfect Model')
ax.plot(xx,yy, color='red', label='User Model')
#ax.scatter(xx,yy, color='red')
ax.plot(xx,xx, color='blue', label='Random Model')
ax.plot([percent, percent], [0.0, val], color='green', linestyle='--', linewidth=1)
ax.plot([0, percent], [val, val], color='green', linestyle='--', linewidth=1, label=str(val*100)+'% of positive obs at '+str(percent*100)+'%')

plt.xlim(0, 1.02)
plt.ylim(0, 1.25)
plt.title("CAP Curve - a_r value ="+str(ar_value))
plt.xlabel('% of the data')
plt.ylabel('% of positive obs')
plt.legend()
plt.show()
```
<img align="center" width="900" height="600" src="http://www.semspirit.com//wp-content/uploads/sites/17154/2017/11/Test-Set-CAP-Curve-1024x555.png">
