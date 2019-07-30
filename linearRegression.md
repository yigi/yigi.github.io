# Theory 
## Dependent / Independent 

<img align="left" width="400" height="300" src="https://miro.medium.com/max/422/1*MUYXO8-4jVJ2VnW4Hy6QmA.png">
- Our independent variables are independent because we cannot mathematically determine the years of experience. But, we can determine / predict salary column values (Dependent Variables) based on years of experience. If you look at the data, the dependent column values (Salary in 1000$) are increasing / decreasing based on years of experience.

## Sum of Squared Errors (SSE)
In order to fit the best intercept line between the points in the above scatter plots, we use a metric called “Sum of Squared Errors” (SSE) and compare the lines to find out the best fit by reducing errors. The errors are sum difference between actual value and predicted value.
To find the errors for each dependent value, we need to use the formula below.

<img align="left" width="300" height="200" src="https://miro.medium.com/max/283/1*0NY9Kv6eQUqTI_5bx3XAww.png">
<img align="center" width="300" height="500" src="https://miro.medium.com/max/457/1*V542U5UybPsf9g1c7lTKIg.png">

The sum of squared errors SSE output is 5226.19. To do the best fit of line intercept, we need to apply a linear regression model to reduce the SSE value at minimum as possible. To identify a slope intercept, we use the equation
y = mx + b,
‘m’ is the slope
‘x’ → independent variables
‘b’ is intercept
We will use Ordinary Least Squares method to find the best line intercept (b) slope (m)

 
## Linear Regression
The goal of Regression is to explore the relation between the input Feature with that of the target Value and give us a continuous Valued output for the given unknown data. 
```python
import pandas
#load csv file
df=pandas.read_csv('./DataSet/HousePrice.csv')
df=df[['Price (Older)', 'Price (New)']]
#Define feature list (X) target(Y)
X=df[['Price (Older)']]
Y=df[['Price (New)']]
#load predefined linearRegression model
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
xTrain,xTest,yTrain,yTest=train_test_split(X,Y)
Lreg=LinearRegression().fit(xTrain,yTrain)
#   formula=(W1*x+b)
print('Coef(W1):',Lreg.coef_)
print('Intercept(W0/b):',Lreg.intercept_)
W1=Lreg.coef_
b=Lreg.intercept_
#ploting the same
import matplotlib.pyplot as plt
plt.scatter(X,Y)
plt.plot(X,W1*X+b,'r-')
plt.show()
#You can predict a value using
#print(Lreg.predict(someValue))
```
 
<img align="left" width="300" height="250" src="https://miro.medium.com/max/640/1*sFs2I2fOaGf-LSQY-Xj8iw.png">

[Image](https://eksiup.com/p/nt535764uevr)


Skewness: Statistics değeri / Std error değeri bulunur. Çıkan değer > 0 ise sağa çarpıktır (asimetrik ), < 0 ise sola çarpıktır (asimetrik ), = 0 ise çarpıklık yoktur (simetrik dağılım). 
Kurtosis: Statistics değeri / Std error değeri bulunur. Çıkan değer > 3 ise leptokurtic eğri mevcuttur (asimetrik ) ve uç değerlerin olasılığı yüksektir , < 3 ise platykurtic (asimetrik ) mevcuttur veriler normal dağılımdan daha basıktır ve daha geniş bir alana yayılmıştır, = 0 ise basıklık yoktur (mesokurtic, simetrik dağılım). 

The skewness for this dataset is 0.514.  A positive skewness indicates that the size of the right-handed tail is larger than the left-handed tail.
 
<img align="left" width="300" height="500" src="https://www.spcforexcel.com/files/images/Skewness-Kurtosis-Figures/Figure-2.png">
 
If the skewness is between -0.5 and 0.5, the data are fairly symmetrical
If the skewness is between -1 and – 0.5 or between 0.5 and 1, the data are moderately skewed
If the skewness is less than -1 or greater than 1, the data are highly skewed

<img align="left" width="500" height="300" src="https://www.researchgate.net/profile/John_Mitchell2/publication/5570487/figure/fig1/AS:213411729285120@1427892729413/Mesokurtic-leptokurtic-and-platykurtic.png">


# Notebook
