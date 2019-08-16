mean ortalama
median sırala ortadaki
mode en çok tekrar eden

**mean**
import numpy as np
incomes = np.random.normal(27000, 15000, 10000)
np.mean(incomes)

**histogram**
import matplob.pyplot as plt
plt.histogram(incomes, 50)
plt.show()

**median**
np.median(incomes)
incomes = np.append(incomes, [100000000])
np.median(incomes)

**mode**
ages = np.random.randint(18, high=90, size=500)

from scipy import stats
stats.mode(ages)

**variance**
how spread out data is
variance is the avarage of the squared differences from the mean
1,3,4,5,8
mean = 1+3+4+5+8 / 5 = 4.4
diff from the mean -3.4, -.4, 0.6, -0.4, 3.6
squared diff 11.56 0.16 ....
avarage of squared diff 11.56 + 0.16 + ... / 5 = **5.04**

**standart deviation** 
root of the variance |/5.04 = 2.24 

incomes.std()
incomes.var()

**uniform distrubition**
values = np.random.uniform(-10, 10, 10000)
plt.hist(values,50)
plt.show()

**normal / gaussian**
#probability distrubition function
from scipy.stats import norm
x = np.arange(-3,3,0.001) 
plt.plot(x, norm.pdf(x))

**exponential PDF**
#probability distrubition function
from scipy.stats import expon

x = np.arange(0, 10, 0.001)
plt.plot(x, expon.pdf(x))

**percentiles**
#in data set what is the point at which X% of the values are less than that values
np.percentile(values, 20) #-0.4
np.percentile(values, 50) #0.05
np.percentile(values, 90) #0.65

**skew**
#distrubition with longer tail on the left will be skewed left, and have negative skew

**kurtosis**
#how tick is the tail, how sharp is the peak. higher peaks have higher kurtosis

**covariance**
#measures how two variables vary in tandem from their means.
#small covariance, close to 0, means there is not much corelation between tow variables
-1 perfect inverse corr 0 no corr 1 perfect corr
divide covariance by the standart deviation

**bayes**
### !!!MISSING
