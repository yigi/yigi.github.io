<img align="left" width="300" height="250" src="https://www.displayr.com/wp-content/uploads/2018/07/Residual_chart_780x480.png"> 

- residual ne kadar artarsa tahminimiz gerçek sonuçtan o kadar uzak demektir.
- y = mx + b [Predicted value/Target Value, Gradient/slope/Weight m, input x, b hiç reklam olmasa bile satış vardır (bias/y-intercept)]
- Least square method: noktalarının birikme gösterdiği noktalardan geçen bir fonksiyonun bulunması yöntemi
- regression line: noktaların tamamına en yakın geçen doğru
- r squared: r arttıkça model uyumu artar. r squared küçükse we ar not able to find a linear relation between the x and y
- standart sapma: Eğer bir çok veri ortalamaya yakın ise standart sapma da düşük olacaktır
- varyans: 1. sınıfta herkesin aldığı not 75. İkinci sınıfta 10 da var 100 de var ortalama yine 75. bu iki sınıfın başarısı aynıdır diyebilir miyiz? Tabi ki hayır. İşte standart sapma ve varyans bu noktada ortalamaya ilave olarak bize sınıf başarısı hakkında kanaat edinmemizi sağlıyor. Bir sınıfta notlar ortalamaya yakın dağılmışken (standart sapma ve varyans düşük), diğer sınıfta ortalamadan çok uzaklara (standart sapma ve varyans büyük) dağılmış.

For more details see [Linear Regression Page](https://ylglt.github.io/linearRegression.md).

___________________________________________________________________________________________________________________________

## Supervised & Unsupervised

<img align="" width="700" height="300" src="https://miro.medium.com/max/700/1*ASYpFfDh7XnreU-ygqXonw.png">
Supervised learning -> is typically done in the context of classification, when we want to map input to output labels, or regression, when we want to map input to a continuous output. ~predict the answer for new, unknown values.~

Unsupervised -> In all of these cases, we wish to learn the inherent structure of our data without using explicitly-provided labels.

___________________________________________________________________________________________________________________________

## Cost Function

In ML, cost functions are used to estimate how badly models are performing. Put simply, a cost function is a measure of how wrong the model is in terms of its ability to estimate the relationship between X and y.
Minimizing the cost function: Gradient descent
Now that we know that models learn by minimizing a cost function, you may naturally wonder how the cost function is minimized — enter gradient descent. Gradient descent is an efficient optimization algorithm that attempts to find a local or global minima of a function.

___________________________________________________________________________________________________________________________

# TIPS
- FP we predict it positive but it was false LESS DANGEROUS 
- FN we predict it negative but it was false (think person is cancer but you say person is not cancer )


- z score = coeff / std. err


- you can interpret coefficient signs: + contributes - detracts
- you canNOT interpret magnitudes of the coefficient


- transform dependent variables in order to increase accuracy 


- multicollinearity using VIF
- collinearity is not always good and may break the model


- r squared is bias
- more variables added to model greater r squared value we have
  - that doesn't mean if we add unnecessary variables to the model r square and model prediction will increase in that case adjusted r squared comes up
  
- polyld polyfit x y 8 yerine x y 1
- naive bayes: use classifier = MultinomialNB()
- entropy: if all animals are iguana entropy = 0 & H(S) = -p1 ln p1 -p2 ln p2
