---
title:  "Normal distribution and its derivatives"
date:   2023-08-01
permalink: /posts/normal-dist-and-its-derivatives
---

## Elementary area and volume in the spherical coordinate system
In the spherical coordinate system, the points of $n$ dimensional space are determined by the Euclidean distance from the coordinate origin $r$ and $n-1$ angles $\phi_{i}$. Indeed, if we start from the orthogonal base $(u_{1},\cdots, u_{n})$, the coordinate $r$ is simply the square root of the sum of squares of coordinates in that orthogonal base. Next, we define $\phi_{n-1}$ as the angle between the position vector of the point and the basis vector $u_{n}$ such that $x_{n} = r\cos{\phi_{n-1}}$. When we fix this angle, with the already fixed radius, we can examine the projection of the hypersphere on the subspace determined by the remaining base vectors $u_{1},\cdots,u_{n-1}$. That projection is also a hypersphere, only in a space one dimension smaller and with a radius scaled by $\sin{\phi_{n-1}}$ . Therefore, we can repeat the same process until we reach a simple circle in 2D. So, the transformation from Cartesian to spherical coordinates looks like this:


$$\begin{align*}
     x_{i} &= r\cos{\phi_{i-1}}\prod_{j=i}^{n-1}\sin^{j-i+1}{\phi_{j}},\quad i=2,\cdots,n \\
     x_{1} &= r\prod_{j=1}^{n-1}\sin^{j}{\phi_{j}}
\end{align*}$$


If $dA_{n}(r)$ denotes the elementary surface of a sphere of radius $r$ on which points can be determined using $n$ angles (thus, the sphere itself is located in $n+1$-dimensional space), then the following recursive relation hold:


$$\begin{equation*}
     dA_{n}(r) = rd\phi_{n}\,dA_{n-1}(r\sin{\phi_{n}})
\end{equation*}$$


with the initial condition $dA_{1}(r) = rd\phi_{1}$. From there it follows:


$$\begin{equation*}
     dA_{n}(r) = r^{n}\prod_{i=1}^{n}d\phi_{i}\sin^{i-1}{\phi_{i}}
\end{equation*}$$


For $n = 2$, which represents an ordinary sphere (in 3D), the polar angle $\phi_{2}$ is usually denoted in physics by $\theta$, and the azimuth $\phi_{1}$ by $\phi$ , the formula $dA = r^{2}\sin{\theta}$ is obtained, which corresponds to the known expression.
The elementary volume in $n$-dimensional space is obtained as:


$$\begin{equation*}
     dV_{n}(r) = drA_{n-1}(r)
\end{equation*}$$


## Estimation of standard deviation given mean is known
Suppose we analyze the random variable $X \sim \mathcal{N}(\mu, \sigma^{2})$. Let's explore what distribution the following statistic has:


$$\begin{equation*}
     S = \frac{\sqrt{\sum_{i=1}^{n}(X_{i}-\mu)^{2}}}{\sigma}
\end{equation*}$$


Introducing change of variables:


$$\begin{align*}
     z_{i} &= \frac{x_{i}-\mu}{\sigma} \\
     dz_{i} &= \frac{dx_{i}}{\sigma}
\end{align*}$$


the probability that the value of the statistic $S$ belongs to the interval $(s, s+ds)$ is equal to:


$$\begin{equation*}
     P(s \leq S < s+ds) = \underset{s < \sqrt{\sum_{i=1}^{n}z_{i}^{2}} < s + ds }{\int\cdots \int}\frac{1}{\sqrt{2\pi}^{n}}e^{-\frac{z_{1}^{2}+\cdots+z_{n}^{2}}{ 2}}dz_{1}\cdots dz_{n}
\end{equation*}$$


Then we switch to spherical coordinates:


$$\begin{align*}P(s \leq S < s + ds) &= \int_{s}^{s+ds}\int_{0}^{\pi}\int_{0}^{\pi} \cdots \int_{0}^{2\pi}\frac{1}{\sqrt{2\pi}^{n}}e^{-\frac{r^{2}}{2}}r^ {n-1}\prod_{i=1}^{n-1}d\phi_{i}\sin^{i-1}{\phi_{i}}dr \\ &=\int_{s}^ {s+ds}e^{-\frac{r^{2}}{2}}r^{n-1}\left(\int_{0}^{\pi}\int_{0}^{\pi}\cdots \int_{0}^{2\pi}\frac{1}{\sqrt{2\pi}^{n}}\prod_{i=1}^{n-1}d\phi_{ i}\sin^{i-1}{\phi_{i}}\right) dr \\ &\propto e^{-\frac{s^{2}}{2}}s^{n-1} ds\end{align*}$$


For further analysis it will be useful to analyze the following integral:


$$\begin{align*}I_{n} &= \int_{0}^{\infty}e^{-\frac{s^{2}}{2}}s^{n}ds \\ &= \int_{0}^{\infty}e^{-u}\left(2u\right)^{\frac{n-1}{2}}du \\ &= 2^{\frac{n-1} {2}}\Gamma\left ( \frac{n+1}{2} \right ) &\end{align*}$$


We get the proportionality coefficient from the condition that the probabilities of all non-overlapping intervals add up to unity:


$$\begin{align*}1 &= \int_{0}^{\infty}Ae^{-\frac{s^{2}}{2}}s^{n-1}ds \\ A &= \frac{1}{I_{n-1}}\end{align*}$$


Also, in this way we have effectively calculated the integral in the parenthesis:


$$\begin{equation*}
     \int_{0}^{\pi}\int_{0}^{\pi}\cdots \int_{0}^{2\pi}\frac{1}{\sqrt{2\pi}^{n} }\prod_{i=1}^{n-1}d\phi_{i}\sin^{i-1}{\phi_{i}} = \frac{1}{I_{n-1}} = \frac{1}{2^{\frac{n}{2}-1}\Gamma\left ( \frac{n}{2} \right )}
\end{equation*}$$


So finally we have:


$$\begin{equation*}
     \frac{d}{ds}P(S<s) = \frac{1}{2^{\frac{n}{2}-1}\Gamma\left ( \frac{n}{2} \right )}e^{-\frac{s^{2}}{2}}s^{n-1}
\end{equation*}$$


Expectation and other moments can also be expressed using the mentioned integral:


$$\begin{align*}E[S] &= \frac{1}{I_{n-1}}\int_{0}^{\infty}se^{-\frac{s^{2}}{2 }}s^{n-1}ds = \frac{I_{n}}{I_{n-1}} = \sqrt{2}\frac{\Gamma\left ( \frac{n+1}{2 } \right )}{\Gamma\left ( \frac{n}{2} \right )} \\ E[S^{2}] &= \frac{1}{I_{n-1}}\int_ {0}^{\infty}s^{2}e^{-\frac{s^{2}}{2}}s^{n-1}ds = \frac{I_{n+1}}{ I_{n-1}} = 2\frac{\Gamma\left ( \frac{n}{2} +1\right )}{\Gamma\left ( \frac{n}{2} \right )} = n\end{align*}$$


It should be noted that the probability distribution characterized by the mentioned law is called Chi distribution.
In the literature, the so-called Chi-square distribution which represents the distribution of the squares of previously analyzed statistics - so $S^{2}$. We can easily derive it:


$$\begin{align*}\frac{d}{d(s^{2})}P(S^{2} < s^{2}) &= \frac{ds}{d(s^{2} )}\frac{d}{ds}P(S < s) \\ &= \frac{1}{2s} \frac{1}{2^{\frac{n}{2}-1}\Gamma \left(\frac{n}{2}\right)}e^{-\frac{s^{2}}{2}}s^{n-1} \\ \frac{d}{d(s ^{2})}P(S^{2} < s^{2}) &= \frac{1}{2^{\frac{n}{2}}\Gamma\left(\frac{n} {2}\right)}e^{-\frac{s^{2}}{2}}(s^{2})^{\frac{n}{2}-1}\end{align*}$$


## Estimation of standard deviation given mean is unknown
We still analyze the random variable $X \sim \mathcal{N}(\mu, \sigma^{2})$. This time we look at the statistics:


$$\begin{equation*}
     S = \frac{\sqrt{\sum_{i=1}^{n}\left(X_{i} - \overline{X_{n}}\right)^{2}}}{\sigma}
\end{equation*}$$


The probability that the value of the statistic $S$ belongs to the interval $(s, s+ds)$ is equal to:


$$\begin{equation*}
     P(s \leq S < s+ds) = \underset{s < \frac{\sqrt{\sum_{i=1}^{n}\left(x_{i} - \overline{x_{n}} \right)^{2}}}{\sigma} < s + ds }{\int\cdots\int}\frac{1}{\sqrt{2\pi}^{n}\sigma^{n}} e^{-\frac{(x_{1}-\mu)^{2}+\cdots+(x_{n}-\mu)^{2}}{2\sigma^{2}}}dx_{1 }\cdots dx_{n}
\end{equation*}$$


Introducing change of variables:


$$\begin{align*}
     z_{i} &= \frac{x_{i}-\mu}{\sigma} \\
     dz_{i} &= \frac{dx_{i}}{\sigma}
\end{align*}$$


the integral is simplified:


$$\begin{equation*}
     P(s \leq S < s+ds) = \underset{s < \sqrt{\sum_{i=1}^{n}\left(z_{i} - \overline{z_{n}}\right) ^{2}} < s + ds }{\int\cdots\int}\frac{1}{\sqrt{2\pi}^{n}}e^{-\frac{z_{1}^{2 }+\cdots+z_{n}^{2}}{2}}dz_{1}\cdots dz_{n}
\end{equation*}$$


Bearing in mind that the mean value $\overline{z_{n}}$ can be written via the scalar product:


$$\begin{equation*}
     \overline{z_{n}} = \frac{e^Tz}{e^{T}e}
\end{equation*}$$


The statistics themselves can also be expressed in vector notation:


$$\begin{equation*}
     S = \left\|\left(I-\frac{ee^{T}}{e^{T}e}\right)z\right\|
\end{equation*}$$


Therefore, if we consider $z$ as a random vector in the $n$-dimensional space, then the statistic $S$ is the length of the projection of that vector onto the plane perpendicular to the vector $e$. If we perform change of variables corresponding to the rotation $\zeta = R^{T}z$ so that the first column of the matrix $R$ is the unit vector $e$, we get:


$$\begin{align*}P(s \leq S < s+ds) &= \underset{s < \sqrt{\sum_{i=2}^{n}\zeta_{i}^{2}} < s + ds }{\int\cdots\int}\frac{1}{\sqrt{2\pi}^{n}}e^{-\frac{\zeta_{1}^{2}+\cdots+\zeta_ {n}^{2}}{2}}d\zeta_{1}\cdots d\zeta_{n} \\ &= \underset{s < \sqrt{\sum_{i=2}^{n}\zeta_{i}^{2}} < s + ds }{\int\cdots\int}\frac{1}{\sqrt{2\pi}^{n-1}}e^{-\frac{\zeta_{2}^{2}+\cdots+\zeta_{n}^{2}}{2}}\left ( \int_{-\infty}^{\infty}\frac{1}{\sqrt{2 \pi}}e^{-\frac{\zeta_{1}^{2}}{2}} d\zeta_{1}\right )d\zeta_{2}\cdots d\zeta_{n} \\ &= \underset{s < \sqrt{\sum_{i=2}^{n}\zeta_{i}^{2}} < s + ds }{\int\cdots\int}\frac{1}{ \sqrt{2\pi}^{n-1}}e^{-\frac{\zeta_{2}^{2}+\cdots+\zeta_{n}^{2}}{2}}d\zeta_ {2}\cdots d\zeta_{n}\end{align*}$$


This is the same integral as in the previous case when the deviation from the true expectation was calculated, except that $n-1$ appears everywhere instead of $n$. So, it is a Chi distribution, this time with $n-1$ degrees of freedom. Using the previous results, we can immediately write:


$$\begin{align*} \frac{d}{ds}P(S<s) &= \frac{1}{2^{\frac{n}{2}-1}\Gamma\left ( \frac{ n}{2} \right )}e^{-\frac{s^{2}}{2}}s^{n-2} \\ E[S] &= \sqrt{2}\frac{\Gamma\left ( \frac{n}{2} \right )}{\Gamma\left ( \frac{n-1}{2} \right )} \\ E[S^{2}] & = n- 1\end{align*}$$


Because the expectation of the squared statistic is $n-1$ and not $n$, the corrected sample variance is a better estimate of the true variance in the sense that its expectation is equal to the true variance:


$$\begin{align*} E\left [ \frac{1}{n-1}\sum_{i=1}^{n}\left(X_{i} - \overline{X_{n}}\right) ^{2}\right ] &= E\left [ \frac{\sigma}{n-1} S^{2}\right ] \\ &= \frac{\sigma}{n-1}E[S ^{2}] \\ &= \sigma\end{align*}$$


## Estimation of mean given standard deviation is unknown
We once again consider the random variable $X \sim \mathcal{N}(\mu, \sigma)$. The subject of our analysis this time is statistics:


$$\begin{equation*}
     S = \sqrt{n}\frac{\overline{X_{n}}-\mu}{\sqrt{\frac{1}{n-1}\sum_{i=1}^{n}\left( X_{i}-\overline{X_{n}}\right)^{2}}}
\end{equation*}$$


The probability that the value of the statistic $S$ belongs to the interval $(s, s+ds)$ is equal to:


$$\begin{equation*}
     P(s \leq S < s+ds) = \underset{s < \sqrt{n}\frac{\overline{x_{n}}-\mu}{\sqrt{\frac{1}{n-1 }\sum_{i=1}^{n}\left(x_{i}-\overline{x_{n}}\right)^{2}}} < s + ds }{\int\cdots\int} \frac{1}{\sqrt{2\pi}^{n}\sigma^{n}}e^{-\frac{(x_{1}-\mu)^{2}+\cdots+(x_{ n}-\mu)^{2}}{2\sigma^{2}}}dx_{1}\cdots dx_{n}
\end{equation*}$$


If we introduce a change of variables:


$$\begin{align*}
     z_{i} &= \frac{x_{i}-\mu}{\sigma} \\
     dz_{i} &= \frac{dx_{i}}{\sigma}
\end{align*}$$


the above integral simplifies to:


$$\begin{equation*}
     P(s \leq S < s+ds) = \underset{s < \sqrt{n}\frac{\overline{z_{n}}}{\sqrt{\frac{1}{n-1}\sum_ {i=1}^{n}\left(z_{i}-\overline{z_{n}}\right)^{2}}} < s + ds }{\int\cdots\int}\frac{ 1}{\sqrt{2\pi}^{n}}e^{-\frac{z_{1}^{2}+\cdots+z_{n}^{2}}{2}}dz_{1 }\cdots dz_{n}
\end{equation*}$$


We can present the numerator and denominator in vector form:


$$\begin{align*}\sqrt{n}\overline{z_{n}} &= \sqrt{e^{T}e}\frac{e^{T}z}{e^{T}e} = \frac{e^{T}z}{\left\| e\right\|} = z_{e} \\ \sqrt{\sum_{i=1}^{n}\left(z_{i}-\overline{z_{n}}\right)^{2} } &= \left\|\left(I-\frac{ee^{T}}{e^{T}e}\right)z\right\|\end{align*}$$


Considering that the numerator is the projection of the vector $z$ onto the direction of vector $e$, and the denominator is the magnitude of the projection onto the hyperplane perpendicular to this direction, if we mark the angle between the vector $z$ and the vector $e$ with $\theta$, we get:


$$\begin{equation*}
     P(s \leq S < s+ds) = \underset{s < \sqrt{n-1}\cot{\theta} < s + ds }{\int\cdots\int}\frac{1}{\sqrt{2\pi}^{n}}e^{-\frac{z_{1}^{2}+\cdots+z_{n}^{2}}{2}}dz_{1}\cdots dz_ {n}
\end{equation*}$$


We can find the distribution for the angle $\theta$ by switching to spherical coordinates:


$$\begin{align*}P(\theta \leq \Theta < \theta + d\theta) &= \int_{\theta}^{\theta+d\theta}\int_{0}^{\pi}\cdots \int_{0}^{2\pi}\int_{0}^{\infty}\frac{1}{\sqrt{2\pi}^{n}}e^{-\frac{r^{ 2}}{2}}r^{n-1}dr\prod_{i=1}^{n-1}d\phi_{i}\sin^{i-1}{\phi_{i}} \\ &=\int_{\theta}^{\theta+d\theta}\sin^{n-2}{\phi_{n-1}} \left(\int_{0}^{\pi}\cdots \int_{0}^{2\pi}\int_{0}^{\infty}\frac{1}{\sqrt{2\pi}^{n}}e^{-\frac{r^{2 }}{2}}r^{n-1}dr\prod_{i=1}^{n-2}d\phi_{i}\sin^{i-1}{\phi_{i}}\right ) d\phi_{n-1} \\ &\propto \sin^{n-2}{\theta}d\theta\end{align*}$$


Then we easily find the distribution for the statistic $S$ itself:


$$\begin{align*}\frac{d}{ds}P(S < s) &\propto \left|\frac{d\theta}{ds}\right| \frac{d}{d\theta}P(\Theta < \theta) \\ &= \frac{d\theta}{\sqrt{n-1}\frac{d\theta}{\sin^{2 }{\theta}}}\sin^{n-2}{\theta} \\ &= \frac{1}{\sqrt{n-1}}\sin^{n}{\theta} \\ \frac{d}{ds}P(S < s) &\propto \frac{1}{\sqrt{n-1}}\left ( 1+\frac{s^{2}}{n-1} \right )^{-\frac{n}{2}}\end{align*}$$


The number $n-1$ represents number of degrees of freedom and it often appears in literature denoted by $\nu$:


$$\begin{equation*}
    \frac{d}{ds}P(S < s) \propto \frac{1}{\sqrt{\nu}}\left (1+s^{2}/\nu\right)^{-\frac {\nu+1}{2}}
\end{equation*}$$


This probability density distribution law represents the well-known Student's t distribution. In order to calculate the normalization coefficient, we need either to calculate the integral of the density distribution function or calculate the integral in the parentheses. We will do the latter:


$$\begin{align*}&\int_{0}^{\pi}\cdots \int_{0}^{2\pi}\frac{1}{\sqrt{2\pi}^{n}}\left (\int_{0}^{\infty}e^{-\frac{r^{2}}{2}}r^{n-1}dr\right)\prod_{i=1}^{n- 2}d\phi_{i}\sin^{i-1}{\phi_{i}} \\ &= \frac{I_{n-1}}{\sqrt{2\pi}}\int_{0 }^{\pi}\cdots \int_{0}^{2\pi}\frac{1}{\sqrt{2\pi}^{n-1}}\prod_{i=1}^{n- 2}d\phi_{i}\sin^{i-1}{\phi_{i}} \\ &= \frac{I_{n-1}}{\sqrt{2\pi}I_{n-2 }} \\ &= \frac{2^{\frac{n}{2}-1}\Gamma\left ( \frac{n}{2} \right )}{\sqrt{2\pi}2^ {\frac{n-3}{2}}\Gamma\left ( \frac{n-1}{2} \right )} \\ &= \frac{\Gamma\left ( \frac{n}{2 } \right )}{\sqrt{\pi}\Gamma\left ( \frac{n-1}{2} \right )} \end{align*}$$


Here is the result:


$$\begin{equation*}
     \int_{-\infty}^{\infty}\frac{1}{\sqrt{\nu}}\left (1+s^{2}/\nu\right)^{-\frac{\nu+ 1}{2}} ds= \frac{\sqrt{\pi}\Gamma\left ( \frac{\nu}{2} \right )}{\Gamma\left ( \frac{\nu+1}{2 } \right )}
\end{equation*}$$


For $\nu=1$ the integral is elementary (the indefinite integral is $\arctan{s}$) and is equal to $\pi$. This means that we can indirectly calculate the value of the gamma function at the point $1/2$:


$$\begin{align*}\pi &= \frac{\sqrt{\pi}\Gamma\left ( \frac{1}{2} \right )}{\Gamma\left (1 \right )} \\ \Gamma\left ( \frac{1}{2} \right ) &= \sqrt{\pi}\end{align*}$$


Going back to the Student's distribution, we finally have:


$$\begin{equation*}
   \frac{d}{ds}P(S < s) =  \frac{\Gamma\left ( \frac{\nu+1}{2} \right )}{\sqrt{\nu\pi}\Gamma\left ( \frac{\nu}{2} \right )}\left (1+s^{2}/\nu\right)^{-\frac{\nu+1}{2}}
\end{equation*}$$


It is interesting that the Student's distribution tends to the normal distribution when $n\to\infty$:


$$\begin{equation*}
     \displaystyle \lim_{\nu \to \infty}\left (1+s^{2}/\nu\right)^{-\frac{\nu+1}{2}} = e^{-\frac{ s^{2}}{2}}
\end{equation*}$$


From here we can also infer something else about the Gamma function:


$$\begin{equation*}
     \displaystyle \lim_{\nu \to \infty}\frac{\Gamma\left ( \frac{\nu+1}{2} \right )}{\sqrt{\nu}\Gamma\left ( \frac{ \nu}{2} \right )} = \frac{1}{\sqrt{2}}
\end{equation*}$$


## Discussion
The previous chapters may have been too abundant with mathematical formulas, symbols and expressions in which the reader can lose the idea of the very essence of the performance and the results reached. That's why it's always good to try to use a less formal and rigorous, but more comprehensible language to clarify what was meant to be conveyed by mathematical notation.

In the previous chapters, we considered certain statistics, that is, functions of several random variables where each of them had a normal probability distribution. The main subject of our research was the probability distribution of those statistics. In each of them, we treated a series of random variables as a vector in a high-dimensional space.

The first statistic we considered was the mean of the random variables. We have shown that the mean value can be represented as a projection onto the direction determined by the vector $e = \begin{bmatrix}1 & \cdots & 1 \end{bmatrix}$ divided by $\sqrt{n}$. Since the normal distribution (Gaussian function) is spherically symmetric, each projection also has a normal probability distribution. However, considering that the required statistic is obtained when the projection is divided by $\sqrt{n}$, the resulting distribution is narrower for that factor, i.e. the standard deviation of the distribution is smaller $\sqrt{n}$ times. This is why statisticians can get better estimates of the true mean of a population the larger the sample.

Another statistic we covered is the square root of the sum of squares of the random variables. This statistic is used in estimating the standard deviation. It geometrically represents the norm (length) of a vector of random variables. Again, taking into account the spherical symmetry of the Gaussian function, we arrive at a probability distribution density function that is proportional to $r^{n-1}\exp{(r^{2}/2)}$. The first factor comes from the fact that the volume of the thin spherical shell is proportional to exactly $r^{n-1}$. Although the Gaussian distribution gives a higher probability to smaller norm vectors, the more distant are more numerous so that the mode of the distribution (most likely value) is greater than zero.

The third statistic was the square root of the sum of the squares of the deviations of the variable values from their mean value. We have shown that this corresponds geometrically to the norm of the projection of the vector of random variables onto the space orthogonal to the vector $e = \begin{bmatrix}1 & \cdots & 1 \end{bmatrix}$. Considering that, we got almost the same probability distribution function, except that $n-1$ occured instead of $n$, considering that it is the length of the vector with one less dimension.

The fourth statistic, like the first, concerns the mean value of the random variables, but this time taking the corrected dispersion estimate instead of the true dispersion. We have shown that this statistic corresponds to the cotangent of the angle between the vector of random variables and the vector $e = \begin{bmatrix}1 & \cdots & 1 \end{bmatrix}$. Given that all vectors of fixed length that subtend the same angle $\theta$ form some kind of hypersphere (in 3 dimensions, it is a ring) whose radius is proportional to $\sin^{n-2}\theta$, the density of probability distribution of cotangent of the angle $\theta$ is proportional to $\sin^{n}\theta$. The resulting probability distribution is known as the Student's distribution.
## Volume of Hypersphere
Using the results from the previous chapters, one can easily calculate the volume of a ball in a space of any number of dimensions:


$$\begin{align*}V_{n} &= \int_{0}^{R}\int_{0}^{\pi}\cdots\int_{0}^{2\pi}r^{n-1 }dr\prod_{i=1}^{n-1}d\phi_{i}\sin^{i-1}{\phi_{i}} \\ &= \frac{\sqrt{2\pi} ^{n}}{I_{n-1}}\int_{0}^{R}r^{n-1}dr \\ &= \frac{\pi^{\frac{n}{2}} 2^{\frac{n}{2}}}{2^{\frac{n}{2}-1}\Gamma\left ( \frac{n}{2} \right )}\frac{R^ {n}}{n}\\ &= \frac{\pi^{\frac{n}{2}}}{\Gamma\left ( \frac{n}{2}+1 \right )}R^ {n}\end{align*}$$

