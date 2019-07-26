## General Data Thoughts

- Is building model or improving data better?
- Get familiar with data first.
- End of the day note the update (what I did and why) and what is next to move on.
- Always work on your own project as a side project.
- Kubeflow: deployments of machine learning workflows on Kubernetes
- Kubernetes: handle docker containers in one place https://eksisozluk.com/entry/74555379
- 20% of your time new things
- Exploration vs. exploitation is the dilemma between trying something new and reapplying what already works.
- Loops in loops? why don't you vectorize it?
- fast.ai
- Know how to apply. When to apply.



### These will transferred to a new page 
- BERT: State of the art language model for NLP
- ULMFIT: https://medium.com/mlreview/understanding-building-blocks-of-ulmfit-818d3775325b

### Things will move to Data Cleaning Section

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
