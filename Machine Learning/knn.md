 In k-NN classification, the output is a class membership
 
 KNN has three basic steps.
1. Calculate the distance.
2. Find the k nearest neighbours.
3. Vote for classes

Importance of K; 
You can’t pick any random value for k. The whole algorithm is based on the k value. Even small changes to k may result in big changes. Like most machine learning algorithms, the K in KNN is a hyperparameter. You can think of K as a controlling variable for the prediction model.

U — Shaped <img align="left" width="600" height="450" src="https://miro.medium.com/max/330/1*EuYh3kBfY5ewpWJBmbhtkg.png">

Two set concentric circles <img align="left" width="600" height="450" src="https://miro.medium.com/max/329/1*WEE7yBtKxG0DFk3RUqHi8A.png">

XOR <img align="left" width="600" height="450" src="https://miro.medium.com/max/329/1*1Rs16dKS4AphdbKOsEKLbg.png">

Linearly separable <img align="left" width="600" height="450" src="https://miro.medium.com/max/329/1*LRT7nPgxo3mX9CrOKs15-Q.png">

Outliers <img align="left" width="600" height="450" src="https://miro.medium.com/max/321/1*vdlSWk294GM6Oq7-fX2ONA.png">


__________________________________________________________________________________________

```python
import matplotlib.pyplot as plt
import pandas as pd
from sklearn import datasets, neighbors
from mlxtend.plotting import plot_decision_regions
```

```python
def knn_comparison(data, k):
 x = data[[‘X’,’Y’]].values
 y = data[‘class’].astype(int).values
 clf = neighbors.KNeighborsClassifier(n_neighbors=k)
 clf.fit(x, y)
# Plotting decision region
 plot_decision_regions(x, y, clf=clf, legend=2)
# Adding axes annotations
 plt.xlabel(‘X’)
 plt.ylabel(‘Y’)
 plt.title(‘Knn with K=’+ str(k))
 plt.show()
```

### clf = neighbors.KNeighborsClassifier(n_neighbors=k)

## U Shaped

```python
data1 = pd.read_csv(‘ushape.csv’)
for i in [1,5,20,30,40,80]:
    knn_comparison(data1, i)
```
<img align="left" width="600" height="450" src="https://miro.medium.com/max/368/1*xdO0y2-iTOYuxjCgzJWKGw.png">


In all the datasets we can observe that when k=1, we are overfitting the model. That is, each point is classified correctly, you might think that it is a good thing, well as the saying goes “ too much is too bad”, overfitting essentially means that our model is training way too well to an extent that it negatively impacts the model.
In all the datasets we can observe that when k = 60 (a large number), we are underfitting the model. Underfitting refers to a model that can neither model the training data nor generalize to new data. An underfit machine learning model is not a suitable model. In the case of outlier dataset, for k=60, our model did a pretty good job. How can we tell this? Because we know that those points are outliers and the data is linearly separable, but that’s not the case every time, we cannot be sure. Also in the XOR dataset, the value of k is not affecting the model to a great extent, unlike other models.

Research has shown that there is no optimal value of hyperparameter(k ) that suits all kind of data sets. Each dataset has it’s own requirements. In the case of a small k, the noise will have a higher influence on the result, and a large k will make it computationally expensive. Research has also shown that a small k is most flexible fit which will have low bias but the high variance and a large k will have a smoother decision boundary which means lower variance but higher bias.
Overfitting and underfitting are the two biggest causes for the poor performance of machine learning algorithms.

### Conclusion
When K is small, we are restraining the region of a given prediction and forcing our classifier to be “blind” to the overall distribution. A small value for K provides the most flexible fit, which will have low bias but high variance. Graphically, our decision boundary will be more jagged as we observed above. On the other hand, a higher K averages more points in each prediction and hence is more resilient to outliers. Larger values of K will have smoother decision boundaries which mean lower variance but increased bias.
