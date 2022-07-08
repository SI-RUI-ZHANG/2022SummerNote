# Lecture 7

---

so far:
Linear regression (OLS loss)

- gradient descent (batch, stochastic)
- normal equations
- regularization
  - best subset selection
  - Ridge
  - Lasso
- Statistical intuition
- Evaluation of the MSE and Bias/Variance decomposition as a function of model complexity
- Linear Classification
  - Ordinary Least Square Classifier
  - Extensions to Multiple classes (on vs one, one vs rest, limitations)
  - Single $ k $ class discriminant classifier (lease squares), using one hot encoding

---

## Logistic regression

Recall the least square loss

$$
l(\beta ) = \frac{1}{N} \sum_{i=1}^{N} ( t ^{(i)} - \beta ^{\top} \tilde{ x } ^{(i)}) ^{2}
$$

$ \rightarrow $ 2 issue:

- output is real (unbounded) while we would prefer a binary or confidence measure
- risk of misclassification in the presence of outliers

$ \rightarrow $ One fix is to introduce an ==activation function==
One possibility to improve is to choose a function that outputs a value in $ [0, 1] $ (can then be considered as measure of confidence)

$$
\begin{align*}
y(x) &= 1 \rightarrow x \in C ^{1} \text{ with } 100 \% \text{ certainty}\\
y(x) &= 0 \rightarrow x \in C ^{0} \text{ with } 100 \% \text{ certainty}\\
y(x) &\in (0, 1) \rightarrow \text{there is risk of misclassification}
\end{align*}
$$

An example of such function is the sigma function $ \sigma(x) $

---

$$
\sigma(x) = \frac{-1}{1 + e ^{-x}}
$$

---

Wherever we are with respect to the decision boundary, the decision remains bounded.

From this, we can define our logistic regression classifier as
$$
h _{\beta } (x) = \sigma ( \beta ^{\top} \tilde{ x }) = \frac{-1}{1 + e ^{- \beta ^{\top} \tilde{ x }}}
$$
$ \rightarrow $ since our classifier outputs a value in $ [0, 1] $ we can interpret this output as a probability.

Letting
$$
\begin{align*}
p (t ^{(i)} \in C _{0} | x ^{(i)}) &= h _{\beta } (x ^{(i)})\\
p (t ^{(i)} \in C _{1} | x ^{(i)}) &= 1 - h _{\beta } (x ^{(i)})
\end{align*}
$$

## Training (learn mapping from feature to label)

we can $ (1) $ consider the probability of observing our complete set of training pairs $ \left\{ x ^{(i)}, t ^{(i)} \right\} _{i=1} ^{N} $, and then look at the weight vector $ \beta  $ which maximizes this probability.

$$
\begin{align*}
p \left( \left. \left\{ t ^{(i)} \right\} _{i=1} ^{N} \right\vert \left\{ x ^{(i)} \right\} _{i=1} ^{N} ; \beta  \right) &=
\prod _{i=1} ^{N}
p \left( t(x ^{(i)})= t ^{(i)} | x ^{(i)} ; \beta  \right) \quad\\
&\text{provided that examples are independent}\\
&=\prod _{i=1} ^{N}
\begin{cases}
p ( t (x ^{(i)}) = 1 | x ^{(i)}; \beta ) \quad \text{if} \quad t ^{(i)} = 1\\
p ( t (x ^{(i)}) = 0 | x ^{(i)}; \beta ) \quad \text{if} \quad t ^{(i)} = 0\\
\end{cases}\\
&=\prod _{i=1} ^{N} p\left(t (x ^{(i)})=1 | x ^{(i)}; \beta \right) ^{t ^{(i)}} p\left(t (x ^{(i)})=0 | x ^{(i)}; \beta \right) ^{1 - t ^{(i)}}
\end{align*}
$$

$ \rightarrow $ taking the log and maximizing, we get

$$
\begin{align*}
\beta _{MLE} &= \text{argmax} _{\beta }
\log (\prod _{i=1} ^{N} h _{\beta } ( x ^{(i)}) ^{t ^{(i)}} (1 - h _{\beta }(x ^{(i)})) ^{t ^{(i)}})\\
&= \text{argmax} _{\beta } \sum_{i=1}^{N} t ^{(i)} \log ( h _{\beta } (x ^{(i)})) + ( 1 - t ^{(i)}) \log(1 - h _{\beta }(x ^{(i)}))\\
&= \text{argmin} _{\beta } \underbrace{ - \sum_{i=1}^{N} t ^{(i)} \log ( h _{\beta } (x ^{(i)})) + ( 1 - t ^{(i)}) \log(1 - h _{\beta }(x ^{(i)}))\\ } _{\text{Log loss}= \text{Binary cross entropy}(*)}
\end{align*}
$$

---
---
**Binary Cross Entropy** (log loss)

$$
-\frac{1}{N}
\sum_{i=1}^{N} t ^{(i)}
\log ( h _{\beta } (x ^{(i)})) +
( 1 - t ^{(i)}) \log(1 - h _{\beta }(x ^{(i)}))\quad\quad(*)
$$

**goal**: find $ \beta  $ that minimize the log loss through gradient descent

$$
\begin{align*}
\beta _{MLE}&= \text{argmax} _{\beta } \sum_{i=1}^{N} t ^{(i)} \log ( h _{\beta } (x ^{(i)})) + ( 1 - t ^{(i)}) \log(1 - h _{\beta }(x ^{(i)}))\\
&= \text{argmin} _{\beta } - \sum_{i=1}^{N} t ^{(i)} \log ( h _{\beta } (x ^{(i)})) + ( 1 - t ^{(i)}) \log(1 - h _{\beta }(x ^{(i)}))
\end{align*}
$$

---
---

$ \rightarrow $ the minimizer to $ (*) $ can then be found through gradient descent. Taking the gradient of the **Binary cross entropy loss** with respect to $ \beta  $,

First computing the derivative $ \frac{\partial l}{\partial h _{\beta }} $ we get

$$
\begin{align*}
\frac{\partial }{\partial h _{\beta }}&
\left\{
    - t ^{(i)} \log ( h _{\beta } (x ^{(i)})) + (1 - t ^{(i)}) \log ( 1 - h _{\beta } ( x ^{(i)}))
 \right\}\\
 &= - t ^{(i)} \frac{\frac{\partial }{\partial \beta } h _{\beta } ( x ^{(i)})}{ h _{\beta }(x ^{(i)})}
 -(1 - t ^{(i)}) \cdot
 \frac{- \frac{\partial }{\partial \beta } h _{\beta }(x ^{(i)})}{1 - h _{\beta }( x ^{(i)})}(**)\\
\frac{\partial }{ \partial \beta } h _{\beta }(x ^{(i)}) &=
\frac{\partial }{\partial \beta } \sigma ( \beta  ^{\top} \tilde{ x } ^{(i)})
=\frac{\partial }{\partial \beta }( \frac{1}{1 + e ^{- \beta ^{\top} \tilde{ x } ^{(i)}}}) (*)\\
(*)&= \frac{1}{(1 + e ^{- \beta ^{\top} \tilde{ x } ^{(i)}}) ^{2}}\cdot
(\tilde{ x } ^{(i)} \cdot e ^{- \beta ^{\top} \tilde{ x } ^{(i)}})\\
&= \frac{1}{(1 + e ^{- \beta ^{\top} \tilde{ x } ^{(i)}})}\cdot
(1 - \frac{1}{1 + e ^{- \beta ^{\top}}\tilde{ x } ^{(i)}}) \cdot \tilde{ x }^{(i)}
\end{align*}
$$

$$
\sigma'(x) = \sigma(x)(1-\sigma(x)) \Rightarrow \frac{\partial }{\partial \beta }(\sigma(\beta ^{\top} \tilde{ x } ^{(i)}))
= \sigma(\beta ^{\top} \tilde{ x } ^{(i)})(1-\sigma(\beta ^{\top} \tilde{ x }^{(i)})) \dots \tilde{ x } ^{(i)}
$$

Substituting this in $ (**) $ we get

$$
\frac{\partial l}{\partial \beta } = \frac{-t ^{(i)}}{\sigma(\beta ^{\top} \tilde{ x } ^{(i)})}
\cdot \sigma (\beta ^{\top} \tilde{ x } ^{(i)})(1-\sigma ( \beta ^{\top} \tilde{ x } ^{(i)})) \tilde{ x }^{(i)}
-\frac{(1 - t ^{(i)})}{1 - \sigma(\beta ^{\top} \tilde{ x } ^{(i)})}
\sigma(\beta ^{\top} \tilde{ x }^{(i)}) ( 1 - \sigma(\beta ^{\top}\tilde{ x } ^{(i)} )) \tilde{ x }^{(i)}
$$

therefore

$$
\begin{align*}
\frac{\partial l}{\partial \beta }&= - t ^{(i)} ( 1 - \sigma (\beta ^{\top} \tilde{ x } ^{(i)})) -
(1 - t ^{(i)})\sigma ( \beta ^{\top} \tilde{ x } ^{(i)}) \tilde{ x } ^{(i)}\\
&= t ^{(i)} - \sigma(\beta ^{\top} \tilde{ x } ^{(i)}) \tilde{ x } ^{(i)}
\end{align*}
$$

From which we can find $ \beta _{MLE} $ from gradient descent

$$
\begin{align*}
\beta (k + 1) = \beta ^{k} - \eta ( t ^{(i)} - \sigma(\beta ^{\top}\tilde{ x } ^{(i)})) \tilde{ x } ^{(i)}
\end{align*}
$$
