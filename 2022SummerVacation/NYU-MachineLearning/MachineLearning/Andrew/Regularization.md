# Regularization

underfitting model tends to have high bias
overfitting model tends to have high variance
bias vs. variance tradeoff

## Address overfitting

Collect more data
Select features to include/exclude
Regularization

---

$$
\begin{align*}
J (\vec{w}, b) =
\underbrace{ \frac{1}{2m} \sum_{i=1}^{m} (f _{\vec{w}, b} (\vec{x} ^{(i)} ) - y ^{(i)})^{2} } _{\text{mean square loss}}
+
\underbrace{ \frac{\lambda}{2m} \sum_{j=1}^{n} w _{j} ^{2} }
_{\text{regularization term}}
\end{align*}
$$

## Gradient Descent

$$
\begin{align*}
J (\vec{w}, b) =
\underbrace{ \frac{1}{2m} \sum_{i=1}^{m} (f _{\vec{w}, b} (\vec{x} ^{(i)} ) - y ^{(i)})^{2} } _{\text{mean square loss}}
+
\underbrace{ \frac{\lambda}{2m} \sum_{j=1}^{n} w _{j} ^{2} }
_{\text{regularization term}}
\end{align*}
$$

**gradient descent implementation:**

repeat
$$
\begin{align*}
w _{j} &= w _{j} - \alpha \frac{\partial }{\partial w _{j}} J (\vec{w}, b)\\
b &= b - \alpha \frac{\partial }{\partial b} J (\vec{w}, b)\\
\end{align*}
$$

where

$$
\begin{align*}
\frac{\partial }{\partial w _{j}} J ( \vec{w}, b) &= \frac{ 1}{m}
\sum_{i=1}^{m}
\left( f _{\vec{w}, b} (\vec{x} ^{(i)}) - y ^{(i)} \right) x _{j} ^{(i)} + \frac{\lambda}{m} w _{j}\\
\frac{\partial }{\partial b} J ( \vec{w}, b) &= \frac{ 1}{m}
\sum_{i=1}^{m}
\left( f _{\vec{w}, b} (\vec{x} ^{(i)}) - y ^{(i)} \right)
\end{align*}
$$

> Math:
> $$
> \begin{align*}
> \frac{\partial }{\partial w _{j}} J (\vec{w}, b) &=
> \frac{\partial }{\partial w _{j}}
> \left[
> \frac{1}{2m} \sum_{i=1}^{m} (f (\vec{x} ^{(i)}) - y ^{(i)}) ^{2}
> +\frac{\lambda}{2 m} \sum_{j=1}^{n} w _{j} ^{2}
> \right]\\
> &= \frac{1}{2m} \sum_{i=1}^{m}
> \left[
> (\vec{w} \cdot \vec{x} ^{(i)} + b - y ^{(i)}) 2 x _{j} ^{(i)}
> \right]
> +\frac{\lambda}{2m} 2 w _{j}\\
> &= \frac{1}{m} \sum_{i=1}^{m}
> \left[
> (f _{\vec{w}, b} (\vec{x} ^{(i)}) - y ^{(i)}) x _{j} ^{i}
> \right]
> +\frac{\lambda}{m} w _{j}
> \end{align*}
> $$

## Regularized logistic regression

$$
J(\vec{w}, b)=-\frac{1}{m} \sum_{i=1}^{m}
\left[
    y ^{(i)} \log(f _{\vec{w}, b} (\vec{x} ^{(i)})) + (1 - y ^{(i)})
    \log(1 - f _{\vec{w}, b} ( \vec{x} ^{(i)}))
\right]
+\frac{\lambda}{2m} \sum_{j=1}^{n} w _{j} ^{2}
$$

repeat
$$
\begin{align*}
w _{j} &= w _{j} - \alpha \frac{\partial }{\partial w _{j}} J (\vec{w}, b)\\
b &= b - \alpha \frac{\partial }{\partial b} J (\vec{w}, b)\\
\end{align*}
$$

where

$$
\begin{align*}
\frac{\partial }{\partial w _{j}} J ( \vec{w}, b) &= \frac{ 1}{m}
\sum_{i=1}^{m}
\left( f _{\vec{w}, b} (\vec{x} ^{(i)}) - y ^{(i)} \right) x _{j} ^{(i)} + \frac{\lambda}{m} w _{j}\\
\frac{\partial }{\partial b} J ( \vec{w}, b) &= \frac{ 1}{m}
\sum_{i=1}^{m}
\left( f _{\vec{w}, b} (\vec{x} ^{(i)}) - y ^{(i)} \right)
\end{align*}
$$

notice that the definition for $ f _{\vec{w}, b} (\vec{x} ^{(i)}) $ is different from that for linear regression
