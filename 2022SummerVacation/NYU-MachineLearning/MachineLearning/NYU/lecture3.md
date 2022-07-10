# Lecture 3

## Important

we make no distinction between **$ \mathbb{R}^{n} $ and $ \mathbb{R}^{n \times 1} $**

## supervised learning

$ x $: feature
$ t $: label

$$
\left\{ x ^{(i)} \in \mathbb{R} ^{D}, t ^{(i)} \in \mathbb{R} \right\} _{i=1} ^{N} = \text{training set}
$$

## general model

$$
h _{\beta} (x) = \beta _{0} + \beta _{1}x _{1} ^{(i)} + \dots + \beta _{D} x _{D} ^{(i)}
$$

## loss function

$$
l(h _{\beta}) = l(\beta) = \frac{1}{2N} \sum_{i=1}^{N}
(t ^{(i)} - (\beta _{0} + \beta _{1} x _{1} ^{(i)} + \dots + \beta _{D} x _{D} ^{(i)})) ^{2} \quad (*)
$$

## goal

$ \rightarrow $ to learn $ h _{\beta}(x) $ from $ \left\{  x ^{(i)} \in \mathbb{R} ^{D}, t ^{(i)} \in \mathbb{R} \right\} $ that minimize $ (*) $

**Notice:** $ \boldsymbol{x} ^{(i)}\in \mathbb{R} ^{D} $ is equivalent to $ \boldsymbol{x} ^{(i)}\in \mathbb{R}^{D \times 1} $

## method

start from a random initial guess of $ \beta _{j} $, we then move iteratively in the direction $ d = -\text{grad} _{\beta } l(\beta ) $

$$
\begin{align*}
\beta ^{(k+1)} &= \beta (k) - \eta \cdot \text{grad}_{\beta } l(\beta )\\
\beta ^{(k+1)} &= \beta (k) - \eta
\frac{1}{N} \sum_{i=1}^{N} (t ^{(i)} - h _{\beta } (x ^{(i)}))\cdot (- \tilde{ x } ^{(i)})
\end{align*}
$$

where

$$
\begin{align*}
\tilde{ x } ^{(i)} &= [1, \boldsymbol{x} ^{(i)}]\\
&=
\left[ 1, x _{1} ^{(i)}, x _{2} ^{(i)}, \dots, x _{D} ^{(i)}  \right]\\
&=
\begin{bmatrix}
1 & x _{1}^{(i)} & x _{2} ^{(i)} &\dots & x _{D}  ^{(i)}
\end{bmatrix}
^{\top}
\\
\beta &= [\beta _{0}, \beta _{1}, \dots, \beta _{D}] \\
&=
\begin{bmatrix}
\beta ^{0} & \beta _{1} & \dots & \beta _{D}
\end{bmatrix}
^{\top}
\\
h _{\beta }(x) &= \beta _{0} + \sum_{j=1}^{D} \beta _{j} x _{j}\\
&= \beta ^{\top} \tilde{ x }\\
&=
\begin{bmatrix}
\beta _{0} & \beta _{1} & \dots & \beta _{D}
\end{bmatrix}
\begin{bmatrix}
1 \\ x _{1}\\ \vdots \\ x _{D}
\end{bmatrix}
\end{align*}
$$

==there are several confusion regarding the dimension of $ \beta  $ and $ \boldsymbol{x} $ in the lecture note, they are defined more precisely in the Jupiter notebook==

## 2 main possibilities

### Batch gradient descent

### Stochastic gradient descent

OLS: ordinary least square

- Alternative approach Minimization to Normal Equations
- Statistical intuition to the least square loss (why is a good idea to use the OLS loss?)
- Non linear data
- Bias Variance tradeoff
- Regularization

## Today $ \rightarrow $

### alternative way to solve the equation

OLS loss

$$
\begin{align*}
l(\beta) &= \frac{1}{2N} \sum_{i=1}^{N} \left( t ^{(i)} - \left( \beta _{0} + \beta _{1} x _{1} ^{(i)} + \dots + \beta _{D} x _{D} ^{(i)} \right) \right) ^{2}\\
&= \frac{1}{2N} \sum_{i=1}^{N} e _{i} ^{2} = \frac{1}{2N} \vec{ e } ^{T} \vec{ e }\\
e _{i} &= (t ^{(i)} - (\beta _{0} + \beta _{1} x _{1} ^{(i)} + \dots + \beta _{D} x _{D} ^{(i)})), \quad \tilde{ x } ^{(i)} = [1, \boldsymbol{x} ^{(i)}]\\
&= ( t ^{(i)} - \beta ^{T} \tilde{ x } ^{(i)}) \\
\vec{ e } &= [e _{1}, e _{2}, \dots, e _{N}]
\end{align*}
$$

At the $ \beta $ that minimizes the function, the $ l(\beta) $ 's derivative is zero
To find the $ \beta $ that minimizes $ l(\beta) $, we can compute the

$$
\text{grad } l (\beta) = \left[ \frac{\partial l}{\partial \beta _{0}}, \frac{\partial l}{\partial \beta _{1}}, \dots, \frac{\partial l}{\partial \beta _{D}} \right]
$$

and then solve the equation grad $ l(\beta) = 0 $ for $ \beta $

Recall that

$$
l(\beta) = \frac{1}{2N} \vec{e} ^{T}\vec{e} = \frac{1}{2N} \sum_{i=1}^{N}\left( t ^{(i)} - \beta ^{T} \tilde{ x } ^{(i)}  \right) ^{2}
$$

and that

$$
\begin{align*}
\vec{e} &= \begin{bmatrix}
e _{1} \\ e _{1} \\ \dots \\ e _{N}
\end{bmatrix}
= \begin{bmatrix}
t ^{(1)} - \beta ^{T} \tilde{ x } ^{(1)} \\ t ^{(2)} - \beta ^{T} \tilde{ x }  ^{(2)} \\ \vdots \\ t ^{(N)} - \beta ^{T} \tilde{ x } ^{(N)}
\end{bmatrix}
= \begin{bmatrix}
t ^{(1)} \\ \vdots \\ t ^{(N)}
\end{bmatrix}
-\begin{bmatrix}
1 & (x ^{(1)}) ^{T} \\ 1 & \vdots \\ 1 & (x ^{(N)}) ^{T}
\end{bmatrix}
\begin{bmatrix}
\beta _{0} \\ \vdots \\ \beta _{D}
\end{bmatrix}\\
&= \begin{bmatrix}
t ^{(1)} \\ \vdots \\ t ^{(N)}
\end{bmatrix}
-\begin{bmatrix}
1 &x _{1} ^{1} &x _{2} ^{2} &\dots & x _{D} ^{(1)}\\
1 &\vdots &\vdots &\vdots &\vdots\\
1 &x _{N} ^{N} &x _{2} ^{2} &\dots &x _{D} ^{(N)}
\end{bmatrix}
\begin{bmatrix}
\beta _{0} \\ \vdots \\  \beta _{D}
\end{bmatrix}\\
&= \vec{ t } - \tilde{ \underline{\underline{X}} } \vec{ \beta }
\end{align*}
$$

$ \vec{ t } $: target vector
$ \tilde{ \underline{\underline{X}} } $ feature vector (where rows are the feature vector augmented with a '1')

$$
\begin{align*}
\tilde{ \underline{\underline{X}} } =
\begin{bmatrix}
1 &x _{1} ^{(1)} &x _{2} ^{(1)} &\dots & x _{D} ^{(1)}\\
1 &\vdots &\vdots &\vdots &\vdots\\
1 &x _{1} ^{(N)} &x _{2} ^{(N)} &\dots &x _{D} ^{(N)}
\end{bmatrix}
\end{align*}
$$

From this, $ l(\beta ) $ can read as

$$
\begin{align*}
l(\beta ) = \frac{1}{2N} \vec{e} ^{\top} \vec{e} =
\frac{1}{2 N} ( \vec{t} - \tilde{ \underline{\underline{X}} } \beta ) ^{\top} (\vec{t} - \tilde{ \underline{\underline{X}} }\beta )
\end{align*}
$$

if we expand the loss

$$
\begin{align*}
l(\beta ) &= \frac{1}{2N} \vec{t} ^{\top} \vec{t} +
\frac{1}{2N} \beta ^{\top} \tilde{ \underline{\underline{X}} } ^{\top} \tilde{ \underline{\underline{X}} } \beta -
\underbrace{\frac{1}{2N} \vec{t} ^{\top} \tilde{ \underline{\underline{X}} } \beta} _{\text{same}} -
\underbrace{\frac{1}{2N} \beta ^{\top} \tilde{ \underline{\underline{X}} } \vec{t}} _{\text{same}}\\
&= \frac{1}{2N} \vec{t} ^{\top} \vec{t} +
\frac{1}{2N}\beta ^{\top} \tilde{ \underline{\underline{X}} } ^{\top} \tilde{ \underline{\underline{X}} } \beta -
\frac{1}{N} \underbrace{\vec{t} ^{\top} \tilde{ \underline{\underline{X}} } \beta } _{w ^{\top} \beta }
\end{align*}
$$

to get the gradient

$$
\text{grad} = \left[ \frac{\partial l}{\partial \beta _{0}}, \dots, \frac{\partial l}{\partial \beta _{D}} \right]
$$

==one:== the gradient of $ w ^{\top} \beta $

$$
\begin{align*}
w ^{\top} \beta &= \vec{t} ^{\top} \tilde{ \underline{\underline{X}} } \beta\\
&= w _{0} \beta _{0} + w _{1} \beta _{1} + \dots + w _{D} \beta _{D}
\end{align*}
$$

to get the gradient

$$
\begin{align*}
\frac{\partial(w ^{\top})\beta }{\partial \beta _{0} } &= w _{0} \dots
\frac{\partial(w ^{\top})\beta }{\partial \beta _{1} } = w _{1} \dots
\frac{\partial(w ^{\top})\beta }{\partial \beta _{D} } = w _{D}\\
\rightarrow \text{grad}_{\beta } (\vec{t}^{\top} \tilde{ \underline{\underline{X}} } \beta )
&= \text{grad}_{\beta } (w)\\
&=  \tilde{ \underline{\underline{X}} } ^{\top}\vec{t}
\end{align*}
$$

==two:== the gradient of $ \beta ^{\top} \tilde{ \underline{\underline{X}} } ^{\top} \tilde{ \underline{\underline{X}} } \beta $ with respect to $ \beta $

$$
\begin{align*}
\rightarrow &\left[ \beta _{0}, \beta _{1} \right]
\underbrace{
\begin{bmatrix}
M _{11} & M _{12}\\
M _{21} & M _{22}\\
\end{bmatrix}
} _{\boldsymbol{M}}
\begin{bmatrix}
\beta _{0}\\
\beta _{1}
\end{bmatrix} \text{ (since the matrix is symmetric)}\\
=&
\left[ \beta _{0}, \beta _{1} \right]
\begin{bmatrix}
M _{11} & M _{12}\\
M _{12} & M _{22}\\
\end{bmatrix}
\begin{bmatrix}
\beta _{0}\\
\beta _{1}
\end{bmatrix}\\
=& \beta _{0}^{2} M _{11} + \beta _{1}\beta _{0} M _{12} + \beta _{1} ^{2} M _{22 } + \beta _{1}\beta _{0} M _{12 } \\
&\rightarrow \frac{\partial l}{\partial \beta _{0}} = 2 \beta _{0} M _{11} + 2 \beta _{1}M _{12 }\\
&\rightarrow \frac{\partial l}{\partial \beta _{1}} = 2 \beta _{1} M _{11} + 2 \beta _{0}M _{12 }\\
\text{grad}& l =
\begin{bmatrix}
\frac{\partial l}{\partial \beta _{0}} \\
\frac{\partial l}{\partial \beta 1}
\end{bmatrix}
= 2 \boldsymbol{M} \beta
\end{align*}
$$

therefore, the gradient is simply given by

$$
2 \tilde{ \underline{\underline{X}} } ^{\top} \tilde{ \underline{\underline{X}} } \beta
$$

Combing ==one== and ==two==, the gradient of $ l (\beta ) $ w.r.t $ \beta  $ is given by
$$
\frac{1}{N} \tilde{ \underline{\underline{X}} } ^{T}\tilde{ \underline{\underline{X}} } \beta -
\frac{1}{N} \tilde{ \underline{\underline{X}} } ^{\top} \vec{t} = \text{grad} _{\beta } l(\beta )
$$

In order to find the $ \beta  $ that minimizes $ l(\beta ) $, we solve for
$$
\begin{align*}
\text{grad} _{\beta }l(\beta ) &= 0\\
\frac{1}{N} \tilde{ \underline{\underline{X}} } ^{T}\tilde{ \underline{\underline{X}} } \beta -
\frac{1}{N}\tilde{ \underline{\underline{X}} } ^{\top} \vec{t} &= 0\\
\tilde{ \underline{\underline{X}} } ^{T}\tilde{ \underline{\underline{X}} } \beta
&= \tilde{ \underline{\underline{X}} } ^{\top} \vec{t}\quad \text{Normal equations}\\
\beta &=  (\tilde{ \underline{\underline{X}} } ^{T}\tilde{ \underline{\underline{X}} })^{-1}
\tilde{ \underline{\underline{X}} } ^{\top}
\end{align*}
$$

this method of solving for minimum loss requires $ \tilde{ \underline{\underline{X}} } $ to be invertible

### why it is a good idea to choose $ \beta $ as the model that minimizes the least square loss?

Assume ==one==
$$
t ^{(i)} = \beta _{0} + \beta _{1} x _{1}^{(i)} + \dots + \beta _{D} x _{D} ^{(i)} + \varepsilon ^{(i)}
$$

further assume ==two==
$$
\varepsilon ^{(i)} = N(0, \sigma)
$$

finally assume ==three==
$$
\varepsilon (i) \quad\text{independent}
$$

Only randomness in $ t ^{(i)}$'s is due to $ \varepsilon ^{(i)} $.
In particular, the probability of observing a $ t ^{(i)} $ is given by
$$
\begin{align*}
p(t ^{(i)}) &= p ( \varepsilon ^{(i)} =
t ^{(i)} - (\beta f0 + \beta _{1} x _{1}^{(i)} + \dots + \beta _{D} x _{D} ^{(i)}))\\
&= \frac{1}{\sqrt{2\pi}\sigma}\exp \left(  \frac{-(t ^{i} - \beta ^{\top} \tilde{ x } ^{(i)}) ^{2}}{2\sigma ^{2}} \right)
\end{align*}
$$

Then, from assumption ==three== the probability of obtaining $ \left\{ t ^{(i)} \right\} _{i=1}^{N} $ given $ \left\{ x ^{(i)}  \right\}_{i=1} ^{N} $ is given by
$$
p\left(\left . \left\{  t ^{(i)}\right\} _{i=2} ^{N} \right \vert x ^{(i)}  \right) =
\prod _{i=1} ^{N} p(t ^{(i)}) = \prod _{i=1} ^{N} \frac{1}{\sqrt{2\pi}\sigma} \exp
\left(  \frac{-(t ^{(i)}- \beta ^{\top} \tilde{ x } ^{(i)}) ^{2}}{2 \sigma ^{2}} \right)
$$

a good approach to learn the model is to look for the value of $ \beta  $ that maximize $ p(\left\{ t ^{(i)} \right\})_{i=1}^{N} $

we can first get rid of the producer by taking the log, since looking for $ \text{argmax} _{\beta } l(\beta ) $ is equivalent to $ \text{argmax} _{\beta }\log(l(\beta )) $

Applying the idea and get rid of unrelated variables, we find that we can find $ \beta  $ by maximizing

$$
-\sum_{i=1}^{N} \frac{(t ^{(i)}- \beta ^{\top} \tilde{ x } ^{(i)})^{2}}{2 \sigma ^{2}}
$$

$ \rightarrow $ the $ \beta  $ that maximize the likelihood is the $ \beta  $ that minimize the OLS.
