---
title: Introduction
---

#  Regression Model

## Linear Models (linear in the parameters) 
 Simple linear relationship: Model the conditional mean response of a continuous variable using a linear relationship to a single continuous variable assuming normal errors

$$
Y=\beta_{0} +\beta_{1}X + \epsilon_{i}  \quad epsilon\sim N(n,\sigma^2)
$$

Given X, Y has a normal distribution with a mean(center) of 𝛽_0+𝛽_1 𝑋 and a variance of 𝜎^2 . Also, it can be written as 
$$
Y|X \sim N(\beta_{0} +\beta_{1}X,\sigma^2)
$$

## Quadratic relationship:
Model the conditional mean response of a continuous variable as a quadratic relationship to a single continuous variable (this is still a linear model as it’s linear in the parameters) 

$$
Y=\beta_{0} +\beta_{1}X + \beta_2X^2 \epsilon \quad \epsilon\sim N(n,\sigma^2)
$$


## Multiple linear relationships
Model the conditional mean response of a continuous variable as a linear relationship with each of two continuous variables (no interaction) 

$$
Y=\beta_{0} +\beta_{1}X_1 + \beta_2X_2 \epsilon \quad \epsilon\sim N(n,\sigma^2)
$$

## Non-Linear Models
A specific relationship: 
$$
Y=\beta_{0} +\beta_{1}X^{\beta_3} + \beta_2X_2^{\beta_4} \epsilon \quad \epsilon\sim N(n,\sigma^2)
$$


## Nonparametric regression
The Nonparametric regression estimate the function
$$
Y_i=f(X_i)+\epsilon_i 
$$

LOWESS (locally weighted scatterplot smoother) 

The predicted  𝑌_𝑖 for a given 𝑋_𝑖  is determined by considering only ‘local’ points in ‘window’ around  𝑋_𝑖. 
- Often a simple linear regression is fit to the local points, and the prediction falls in this line
- Researcher chooses width of window
