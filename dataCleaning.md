### Drop Multiple Columns
 df.drop(column_names, axis = 1, inplace = True)
### Change dtypes (to save memory)
 df[column_int] = df[cloumn_int].astype('int32')
 df[column_float] = df[cloumn_float].astype('float32')
### Convert categorical variable to numerical
 num_encode = { 'column1' : {'YES' : 1, 'NO' : 0},
                'column2' : {'WIN' : 1, 'LOSE' : 0} }
 df.replace( num_encode, inplace = True)
### Check missing data
  df.isnull().sum().sort_values(ascending = False)
### Remove whitespace 
  df[col] = df[col].str.lstrip()
### Convert timestamp (from string to datetime)
  date_str1 = 'Wednesday, June 6, 2018'
  date_str2 = '6/6/18'
  date_str3 = '06-06-2018'

  date_dt1 = datetime.strptime(date_str1, '%A, %B %d, %Y')
  date_dt2 = datetime.strptime(date_str2, '%m/%d/%y')
  date_dt3 = datetime.strptime(date_str3, '%m-%d-%Y')

________________________________________________________________________________________________________________


- Data Cleaning -> Data Modeling -> Performance Tuning
- Expectation Maximization: method to figure out parameters that will affect model outcome
- null hypothesis: opposite to altervative hyp. [ y= c + a.x + u ]
   - (null) h0: a=0 (duşun seks üzerinde bir etkisi yok)
   - (alternative) h1: a>0 (duşun seks üzerinde pozitif bir etkisi var.
- statistical significance: you cant say 51% over 49% can decide the probability.
- Little's MCAR test: figure out whether your data that is not missing at random -> if sig is greater than 0.05 there is no statistical sig. This mean that you accept the null hypot. that "Data is completely missing at random". If MAR and MCAR delete. Otherwise, impute. 

0.05’den daha büyük > İstatistiksel olarak anlamlı değil. 
0.01-0.05 arası > İstatistiksel olarak anlamlı
0.001-0.01 arası > Yüksek düzeyde istatistiksel olarak anlamlı

- Listwise deletion can introduce bias into dataset
- Pairwise deletion related with below.
- Drop variableif 60% of the data is missing. But can affect the other variables. You can not know that.
- Categorical var. gender -> create new level such as no gender if there is missing data and use logistic regression, KNN to estimate data
- Continuous var. salary -> use mean median and linear regression, KNN to estimate data
- Mean median reduces the variance of the imputed variables. shrinks the standart error.
