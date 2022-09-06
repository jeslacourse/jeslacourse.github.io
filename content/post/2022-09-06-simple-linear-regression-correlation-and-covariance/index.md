---
title: Simple Linear Regression - Correlation and Covariance
date: '2022-09-06'
slug: /covariance/
categories: regression
tags: ['correlation', 'covariance' ]
---

## Covariance 

Given the random variables $(X,Y)$ **covariance** is defined as: 

$$cov(X,Y) = E[(X -\mu_x)(Y-\mu_y)]$$

with **sample covariance**

$$\hat{cov}(X,Y) = \frac{\Sigma(X_i - \bar{X})(Y_i-\bar{Y})^2}{n-1} $$

## Correlation 

**Correlation** is defined on the scale $-1 \leq corr(X,Y) \leq 1$ where: 

$$corr(X,Y) = \frac{cov(X,Y)}{\sqrt{var(X)var(Y)}}$$

### Rules for Expectation [Roll into prior post]

Given random variables $X$ and $Y$ and constants $a,b,$ & $c$: 

1. $E(c) = c$
2. $E(cX) = cE(X)$
3. $E(X+Y) = E(X) + E(Y)$


An example: 
$$E(a+bX+cY) \\ = a + bE(X) + cE(Y)$$

### Rules for Variance

1. $var(a) = 0$ 
2. $var(aX) = a^2 var(X)$
3. $var(X+Y)  = var(X) + var(Y) + 2cov(X,Y)$ 

An example:

$$var(a+bX-cY) \\= var(a) + var(bX-cY) + 2cov(X,Y)\\= 0 + var(bX)+ var(-cY) \\=b^2var(X) + c^2var(Y)+2[(-bc)cov(X,Y)]$$

### Rules for Covariance 

1. $cov(X,Y) = cov(Y,X)$
2. if $X ⫫ Y \Rightarrow cov(X,Y) = 0$, if the random variables are independent of one another, then we cannot predict their variability
3. if $cov(X,Y)= 0 \Rightarrow$ may or may not $X ⫫ Y$
4. $cov(a,b) = 0$
5. $cov(a, X) = 0$ 
6. $cov(aX, Y) = a cov(X,Y)$ 
7. $cov(aX, bY) = ab cov(X,Y)$
8. $cov(X, Y+Z) = cov(X,Y)+cov(X,Z)$
9. $cov(X,X) = var(X)$
