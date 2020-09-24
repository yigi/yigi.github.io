# building a model

- all in (prior knowledge)
- backward elimination
	- select significance level to say in the model (e.g. SL = 0.05 5%
	- fit the full model with all possible predictors
	- consider the predictor with the highest P-value (if P > SL go STEP 4 else go FIN )
	- remove the predictor
	- fit the model without this variable
	FIN Your Model Is Ready
- forward selection
	- select significance level to enter the model (e.g. SL = 0.05 5%
	- fit all simple regression models. Select the one with the lowest P-value
	- keep this variable and fit all possible models. add to the you already have. keep adding.
	- consider the predictor with the lowest P-value. ( if P < SL go step 3 else go FIN )
	FIN Keep the previous model not the current one
- bidirectional elimination
	- select significance level to enter and to stay in the model (e.g. SLENTER / SLSTAY = 0.05 5%
	- add new variables but new variable must have P < SLENTER to enter
	- perform all steps of Backward Elimination ( old variables must have P < SLSTAY to stay ) 
	- no variables can enter and no old variables can exit
	FIN Your Model Is Ready
- all possible models
	- construct all possible regression models 2^n - 1 combination :( 
