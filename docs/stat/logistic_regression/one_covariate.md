---
title: One covariate Model
---
# One covariate Model
## Introduction

In the general model with one covariate:

$$
ln \left( \frac{P(Y_{i}=1)}{1-P(Y_{i}=1)} \right) = \beta_{0} + \beta_{1} X_{i}
$$



which means

$$
\begin{aligned}
P(Y_{i}=1) &=& \frac{exp(\beta_{0} + \beta_{1}  X_{i})}{1+exp(\beta_{0} + \beta_{1}  X_{i})} \\
&=& \frac{1}{1+exp[-(\beta_{0} + \beta_{1}  X_{i})]}
\end{aligned}
$$



-  If $\beta_{1}$ is positive, we get the S-shape that goes to 1 as $X_{i}$ goes to $\infty$ and goes to 0 as $X_{i}$ goes to $-\infty$ (as in the lead example).
- If $\beta_{1}$ is negative, we get the opposite S-shape that goes to 0 as $X_{i}$ goes to $\infty$ and goes to 1 as $X_{i}$ goes to $-\infty$.

Another way to think of logistic regression is that we're modeling a Bernoulli random variable occurring for each $X_{i}$, and the Bernoulli parameter $\pi_{i}$ depends on the covariate value.

Then,  $Y_{i}|X_{i} \sim Bernoulli(\pi_{i})$ where  $\pi_{i}$ represents $P(Y_{i}=1|X_{i})$
$E(Y_{i}|X_{i})=\pi_{i}$ and  $V(Y_{i}|X_{i})=\pi_{i}(1-\pi_{i})$. 

We're thinking in terms of the conditional distribution of $Y|X$ (we don't have constant variance across the $X$ values, mean and variance are tied together).

Writing $\pi_{i}$ as a function of $X_{i}$

$$\pi_{i} = \frac{exp(\beta_{0} + \beta_{1}  X_{i})}{1+exp(\beta_{0} + \beta_{1}  X_{i})}$$

## Interpretation of parameters
For the lead levels example.
###  Intercept $\beta_{0}$
When $X_{i}=0$, there is no lead in the soil in the backyard.  Then,
$$
ln \left( \frac{P(Y_{i}=1)}{1-P(Y_{i}=1)} \right) = \beta_{0} 
$$

So, $\beta_{0}$ is the log-odds that a randomly selected child with no lead in their backyard has a high lead blood level. Or, $\pi_{i}=\frac{e^{\beta_{0}}}{1+e^{\beta_{0}}}$ is the chance that a kid with no lead in their backyard has high lead blood level.

For this data,
\indent \tab \tab $\hat{\beta}_{0}=-1.5160$ \tab or \tab $\hat{\pi_{i}}=0.1800$

### Coefficient $\beta_{1}$
Consider the log$_{e}$ of the odds ratio ($O.R.$) of having high lead blood levels for the following 2 groups...
-  1) those with exposure level of $x$
-  2) those with exposure level of $x+1$

$$
\begin{aligned}
log_{e} \left( \frac{\frac{\pi_{2}}{1-\pi_{2}}}{\frac{\pi_{1}}{1-\pi_{1}}} \right)&=log_{e} \left( \frac{e^{\beta_{0}}e^{\beta_{1}(x+1)}}{e^{\beta_{0}}e^{\beta_{1}x}} \right)
&=&log_{e}\left( e^{\beta_{1}} \right)
&=&\beta_{1}
\end{aligned}
$$


$\beta_{1}$ is the log$_{e}$ of $O.R.$ for a 1 unit increase in $x$.

Or, un-doing the log,  $e^{\beta_{1}}$ is the $O.R.$ comparing the two groups.
For this data $\hat{\beta}_{1}=0.0027$  or  $e^{0.0027}=1.0027$ A 1 unit increase in X increases the odds of having a high lead blood level by a factor of 1.0027.
Though this value is small, the range of the  $X$ values is large(40 to 5255), so it can have a substantial impact when you consider the full spectrum of $x$ values.


## Prediction
What is the predicted probability of high lead blood level for a child with $X=500$.

$$
\begin{aligned}
P(Y_{i}=1) &=& \frac{exp(-1.5160 + 0.0027  X_{i})}{1+exp(-1.5160 + 0.0027  X_{i})} \\
&=& \frac{1}{1+exp[-(-1.5160 + 0.0027  X_{i})]} \\
&=& \frac{1}{1+exp[1.5160 - 0.0027 \times 500]} \\ 
&=&   0.4586 \\
\end{aligned}
$$

What is the predicted probability of high lead blood level for a child with $X=4000$.
$$
P(Y_{i}=1) = \frac{1}{1+exp[1.5160 - 0.0027 \times 4000]} =  0.9999
$$

What is the predicted probability of high lead blood level for a child with $X=0$.

$$
P(Y_{i}=1) = \frac{1}{1+exp[1.5160]} =  0.1800
$$

So, there's still a chance of having high lead blood level even when the backyard doesn't have any lead.  This is why we don't see the low-end of our fitted S-curve go to zero.

