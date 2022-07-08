# Gaussian Distribution

## Probability Density Function (pdf)

$$
\begin{align*}
&\forall \boldsymbol{x} \in \mathbb{R}^{D}: f(x) \ge 0\\
&\int _{\mathbb{R}^{D}} f(\boldsymbol{x}) d \boldsymbol{x} = 1
\end{align*}
$$

Gaussian distribution for **univariate random variable** has a density given by
$$
p(x|\mu, \sigma ^{2}) = \frac{1}{\sqrt{2\pi \sigma ^{2}}}
\exp \left( -\frac{(x-\mu) ^{2}}{2 \sigma ^{2}} \right)
$$

Gaussian distribution for **multivariate random variable** has a density given by

$$
p(\boldsymbol{x}|\boldsymbol{\mu, \Sigma})=
(2\pi)^{-\frac{D}{2}}
\left| \Sigma \right| ^{-\frac{1}{2}}
\exp \left( - \frac{1}{2}(\boldsymbol{x}-\boldsymbol{\mu})^{\top}
\Sigma ^{-1}
(\boldsymbol{x}-\boldsymbol{\mu})
\right)
$$

- $ \boldsymbol{\mu} $ : mean vector
- $ \Sigma $ : covariance matrix

where $ \boldsymbol{x}\in \mathbb{R}^{D} $, we write
$$
\begin{align*}
&p(\boldsymbol{x})=
N (\boldsymbol{x}| \boldsymbol{\mu}, \Sigma)\\
&\text{or}\\
&X \sim N(\boldsymbol{\mu}, \Sigma)
\end{align*}
$$

variance
$$
\sigma ^{2}= \frac{\Sigma (x-\mu) ^{2}}{N}
$$

covariance:
$$
\begin{align*}
Cov(X, Y) &= E [(X-EX)(Y-EY)] = E[XY] - (EX)(EY)\\
&= \frac{\Sigma (X _{i} - \bar X)(Y _{i} - \bar X)}{N}
\end{align*}
$$
