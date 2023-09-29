---
title:  "Linear regression"
date:   2023-09-14
categories: probability theory
permalink: posts/linear-regression
---
This post builds upon an [earlier post](/posts/normal-dist-and-its-derivatives) about Chi-squared and Student distribution. You might want to check it out before proceeding.
## Orthodox statistics' perspective
In regression, we start from the model which proposes a conditional probability distribution of target variable given $p-1$ predictor variables (covariates). With linear regression, this is usually normal distribution with mean being the linear function of predictors and some, unknown, variance. That is, we have:

$$\begin{equation*}

    P\left(Y=y | X_{1}=x_{1}, \cdots, X_{p-1}=x_{p-1}\right) = \mathcal{N}\left(\beta_{0} + \sum_{j=1}^{p-1}\beta_{j}x_{j}, \sigma^2\right)

\end{equation*}$$

In case of $n$ samples, we can switch to vector notation in the following way:




- We define a vector $y \in \mathrm{R}^{n}$ to be the vector whose $i^{th}$ element is a target value of the $i^{th}$ sample.

- We define a matrix $X \in \mathrm{R}^{n\times p}$ to be the matrix whose $i^{th}$ row is a vector of predictor variables for $i^{th}$ sample prepended by 1.

- We define a vector $\beta \in \mathrm{R}^{p}$ to be a vector whose $i^{th}$ element is $\beta_{i}$. 




Now, we can rewrite the above equation in vector-matrix form:

$$\begin{equation*}

    P\left(Y=y | X\right) = \mathcal{N}\left(X\beta, \sigma^{2}I\right)

\end{equation*}$$

We can estimate parameters $\beta$ by maximizing the likelihood of observed samples which, in case of normal distribution, comes down to least squares problem. That is, we ought to solve:

$$\begin{equation*}

    \hat{\beta} = \arg \min_{\beta} \| X\beta - y\|^{2} 

\end{equation*}$$

This is a well-known problem, but we'll still briefly explain one way to solve it. The key thing to realize is that $X\beta$ is some vector in the space spanned by columns of $X$. Thus, we have to find a vector from that space which is closest to $y$. By geometric intuition it is obvious that this is the orthogonal projection of $y$ onto that space. Put differently, the difference $y-X\beta$ must be orthogonal to that space ie. it must be orthogonal to each column of matrix $X$. Thus, we arrive at the equation:

$$\begin{align*}

    &X^{T}\left(y - X\hat{\beta}\right) = o \\

    &\hat{\beta} = \left(X^{T}X\right)^{-1}X^{T}y

\end{align*}$$

Of course, this works only if $X^{T}X$ is of full rank ie. $X$ has $p$ linearly independent columns. Otherwise, the solution is not unique.

Since $y$ is a random vector variable, so is $\hat{\beta}$. We can inspect what its distribution is. Plugging $y = X\beta + \epsilon$ where $\epsilon \sim \mathcal{N}(0,\sigma^{2}I)$, we get:

$$\begin{align*}

    \hat{\beta} &= \left(X^{T}X\right)^{-1}X^{T}\left(X\beta + \epsilon\right) \\ &= \beta + \left(X^{T}X\right)^{-1}X^{T}\epsilon

\end{align*}$$

Here we can readily see that $E\left[\hat{\beta}\right] = \beta$. Furthermore, it's obvious that the distribution is also normal since the second term is a vector whose elements are linear combinations of normally distributed random variables. On the other hand, how covariance matrix looks like is less clear, although it's clear that it is not diagonal in general. It is nevertheless relatively simple to derive it:

$$\begin{align*}

    \Sigma &= E\left[\left(\hat{\beta} - \beta\right)\left(\hat{\beta} - \beta\right)^{T}\right] \\ &= E\left[\left(\left(X^{T}X\right)^{-1}X^{T}\epsilon\right)\left(\left(X^{T}X\right)^{-1}X^{T}\epsilon\right)^{T}\right] \\ &= \left(X^{T}X\right)^{-1}X^{T}E\left[\epsilon\epsilon^{T}\right]X\left(X^{T}X\right)^{-1} \\ &= \left(X^{T}X\right)^{-1}X^{T}\sigma^{2}I X\left(X^{T}X\right)^{-1} \\ &= \sigma^{2}\left(X^{T}X\right)^{-1}

\end{align*}$$

Thus, we have $\hat{\beta} \sim \mathcal{N}\left(\beta, \sigma^{2}\left(X^{T}X\right)^{-1} \right)$.


Naturally, we might want to calculate confidence interval, although at first it's not really clear how to do it now that we are in high-dimensional space. Before we proceed, let's see what is the distribution of a sum of squared residuals. Residuals can be represented as a vector:

$$\begin{align*}

    \hat{r} &= y - X\hat{\beta} \\ &= y - X\left(X^{T}X\right)^{-1}X^{T}y \\ &= \left(I-H\right)y \\ &= \left(I-H\right)\left(X\hat{\beta}+\epsilon\right) \\ &= (I-H)\epsilon

\end{align*}$$

where $H = X\left(X^{T}X\right)^{-1}X^{T}$ is a projection matrix onto space spanned by columns of $X$. Thus, $(I-H)\epsilon$ is a projection of $\epsilon$ onto space orthogonal to that one - its dimension is $n-p$. Then, as we know from our earlier investigations:

$$\begin{equation*}

    \frac{\|\hat{r}\|^{2}}{\sigma^{2}} \sim \chi_{n-p}

\end{equation*}$$

Thus, we can use this fact to find unbiased estimator for $\sigma^{2}$:

$$\begin{equation*}

    \hat{\sigma}^{2} = \frac{\|\hat{r}\|^{2}}{n-p}

\end{equation*}$$

Returning back to the problem of finding confidence interval for $\beta$ coefficients, there's an obvious generalization to interval estimation for the whole set of parameters. However, these won't be independent intervals, but we could say with certain probability that parameters lie inside some hyper-ellipsoid determined by the covariance matrix $\Sigma$.

The other approach is to find marginalized distribution for each parameter $\beta_{j}$. In that case, we have:

$$\begin{equation*}

    \hat{\beta_{i}} \sim \mathcal{N}\left(\beta_{j}, \sigma^{2}\left(X^{T}X\right)^{-1}_{jj} \right)

\end{equation*}$$

and $z$-score reads:

$$\begin{equation*}

    \frac{\hat{\beta}_{j}-\beta_{j}}{\sqrt{\sigma^{2}\left(X^{T}X\right)^{-1}_{jj}}}.

\end{equation*}$$

However, often times we don't know $\sigma$. We must then revert to mean of squared residuals, expecting to arrive at student distribution. We now proceed to demonstrate that this is indeed the case.

As we previously showed, student distribution arises when we look at the ratio between two projections of random vector which are mutually orthogonal. By substituting $\|\hat{r}\|^{2}/(n-p)$  for $\sigma^{2}$, we'll have $\|(I-H)\epsilon\|^{2}$ in the denominator. That means that we "need" some projection belonging to the column space of $H$ in the numerator. Also, this projection should be proportional to $\hat{\beta_{j}}-\beta_{j}$. We already know that:

$$\begin{equation*}

    X(\hat{\beta}-\beta) = H\epsilon

\end{equation*}$$

We would like to find a vector $q$ such that $q^{T}X \propto e_{j}^{T}$ where $e_{j}$ is $j^{th}$ basis vector. This means that $q$ should be such that it is orthogonal to all the columns of $X$ except for the $j^{th}$ one. This essentially means that if we perform Gram-Schmidt process on columns of $X$ such that $j^{th}$ column comes last, then $q$ has to be a multiple of the last orthogonal vector. Without loss of generality, let's assume that $j=p$ and let $X=QR$ be a QR decomposition of $X$ where $Q\in\mathrm{R}^{n\times p}, Q\in\mathrm{R}^{p\times p}$ (there's really special in the order of covariates). Then, $q=q_{p}$ and consequently:

$$\begin{align*}

    q^{T}X &= q_{p}^{T}QR \\ &= e_{p}^{T}R \\ &= r_{pp}e_{n}^{T}.

\end{align*}$$

At the same time, we have:

$$\begin{align*}

    (X^{T}X)^{-1}_{pp} &= (R^{T}R)^{-1}_{pp} \\ &= \left(R^{-1}(R^{-1})^{T}\right)_{pp} \\ &= \left(\frac{\prod_{k\neq p}r_{kk}}{\prod_{k}r_{kk}}\right)^{2} \\ &= \frac{1}{r_{pp}^{2}},

\end{align*}$$

where we exploited the fact that $R$ is full-rank and upper-triangular. Plugging all the pieces together, we get:

$$\begin{align*}

    &\frac{\hat{\beta}_{p}-\beta_{p}}{\sqrt{\frac{\|\hat{r}\|^{2}}{n-p}\left(X^{T}X\right)^{-1}_{pp}}} \\ =& \sqrt{n-p}\frac{r_{pp}e_{n}^{T}(\hat{\beta}-\beta)}{\|\hat{r}\|} \\ =& \sqrt{n-p}\frac{q^{T}H\epsilon}{\|(I-H)\epsilon\|}

\end{align*}$$

Since $q$ belongs to column space of $H$, it holds that $H^{T}q = Hq = q$. Finally, we end up with a statistic:

$$\begin{equation*}

    \sqrt{n-p}\frac{q^{T}\epsilon}{\|(I-H)\epsilon\|}

\end{equation*}$$

In the numerator we have a projection on the space of dimension 1, whereas in the denominator we have a projection on the space of dimension $n-p$, orthogonal to the former. Again, in our earlier investigations, we saw that this leads to a Student distribution with $n-p$ degrees of freedom. Thus, we have:

$$\begin{equation*}

    \frac{\hat{\beta}_{j}-\beta_{j}}{\sqrt{\hat{\sigma}^{2}\left(X^{T}X\right)^{-1}_{jj}}} \sim t_{n-p}

\end{equation*}$$

This is the statistic commonly used to test the significance of $j^{th}$ predictor's influence on the target variable.
