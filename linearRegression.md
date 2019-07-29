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

