<img align="left" width="300" height="250" src="https://www.displayr.com/wp-content/uploads/2018/07/Residual_chart_780x480.png"> 

- residual ne kadar artarsa tahminimiz gerçek sonuçtan o kadar uzak demektir.
- y = mx + b [Predicted value/Target Value, Gradient/slope/Weight m, input x, b hiç reklam olmasa bile satış vardır (bias/y-intercept)]
- Least square method: noktalarının birikme gösterdiği noktalardan geçen bir fonksiyonun bulunması yöntemi
- regression line: noktaların tamamına en yakın geçen doğru
- r squared: r arttıkça model uyumu artar. r squared küçükse we ar not able to find a linear relation between the x and y
- standart sapma: Eğer bir çok veri ortalamaya yakın ise standart sapma da düşük olacaktır
- varyans: 1. sınıfta herkesin aldığı not 75. İkinci sınıfta 10 da var 100 de var ortalama yine 75. bu iki sınıfın başarısı aynıdır diyebilir miyiz? Tabi ki hayır. İşte standart sapma ve varyans bu noktada ortalamaya ilave olarak bize sınıf başarısı hakkında kanaat edinmemizi sağlıyor. Bir sınıfta notlar ortalamaya yakın dağılmışken (standart sapma ve varyans düşük), diğer sınıfta ortalamadan çok uzaklara (standart sapma ve varyans büyük) dağılmış.


## Linear Regression sayfasına taşınacaklar
 
- linear regression: The goal of Regression is to explore the relation between the input Feature with that of the target Value and give us a continuous Valued output for the given unknown data. 
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
