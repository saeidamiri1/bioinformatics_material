---
title: Multiple covariate Model
---
# Multiple covariate Model


In general,  when the response variable is binary, We model the log of the odds for Yi = 1

$$
ln \left( \frac{P(Y_{i}=1)}{1-P(Y_{i}=1)} \right) = \beta_{0} + \beta_{1}X_{1i}+\cdots + \beta_{k}X_{ki}
$$

Which can be converted to

$$
\begin{aligned}
P(Y_{i}=1) &=& \frac{exp(\beta_{0} + \beta_{1}X_{1i}+\cdots + \beta_{k}X_{ki})}{1+exp(\beta_{0} + \beta_{1}X_{1i}+\cdots + \beta_{k}X_{ki})}\\
&=& \frac{1}{1+exp[-(\beta_{0} + \beta_{1}X_{1i}+\cdots + \beta_{k}X_{ki})]}
\end{aligned}
$$

Unlike OLS regression, logistic regression does not assume...

- linearity between the independent variables and the dependent.
-  normally distributed errors.
-  homoscedasticity.

It does assume...

- we have independent observations
- that the independent variables be linearly related to the logit of the dependent variable (somewhat difficult to check

