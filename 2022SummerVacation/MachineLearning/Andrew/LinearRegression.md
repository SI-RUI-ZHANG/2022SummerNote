# Linear Regression

Univariate linear regression: only one variable

$$
\begin{align*}
f _{w,b} (x ) &= wx + b\\
f (x ) &= wx + b
\end{align*}
$$

$ \hat{y} $ is the predicted value

$$
\begin{align*}
\hat{y} &= f _{w,b} (x ^{(i)})\\
f _{w,b} (x ^{(i)}) &= w x ^{(i)} + b
\end{align*}
$$

goal:
find $ w,b $ such that $ \hat{y } ^{(i)} $ is close to $ y ^{(i)} $ for all $ ( x ^{(i)}, y ^{(i)}) $

to do that, we need a cost function

**Squared error cost function**:

$$
\begin{align*}
J (w, b)&=\frac{1}{2m} \sum_{i =1 }^{m} (\underbrace{ \hat{y} ^{(i)} - y ^{(i)} } _{error}) ^{2}\\
J (w, b)&=\frac{1}{2m} \sum_{i =1 }^{m} (f _{w, b} (x ^{(i)} )- y ^{(i)}) ^{2}\\
\end{align*}
$$

$ m $ number of training examples

==goal==

$$
\text{minimize} _{w,b} J (w, b)
$$

![picture 1](../../../images/3731b69644b38624e54a481e839cf53ec74e8e224145ad7a07ad1b689da2b346.png)  

## Gradient Descent

Goal:
have: $ J(w,b) $
want: $ \min _{w,b}J(w,b) $
or: $ \min _{w _{1}, \dots, w _{n}, b} = J (w _{1}, \dots, w _{n}, b) $

**Gradient descent algorithm**:

$$
\begin{align*}
w = w - \alpha \frac{\partial }{ \partial w}  J (w, b)\\
b = b - \alpha \frac{\partial }{ \partial b}  J (w, b)
\end{align*}
$$

- $ \alpha $: learning rate
- $ \frac{\partial }{\partial w} J(w,b) $: derivative
- $ \frac{\partial }{\partial b} J(w,b) $: derivative

You want to simultaneously update $ b, w $

**Batch**: Each step of gradient descent uses al the training examples

## Linear Regression with multiple features

$ \boldsymbol{x} _{j} = j ^{th} $ feature
$ n = $ number of features
$ \vec{\boldsymbol{x}} ^{(i)} = $ feature of $ i ^{th} $ training example
$ \boldsymbol{x} _{j} ^{(i)} = $ value of feature $ j $ in $ i ^{th} $ training example

Model:

$$
\begin{align*}
f _{w,b} (x) = w _{1} x _{1} + w _{2} x _{2} + w _{3} x _{3} + \dots + b
\end{align*}
$$

rewrite:

$$
\begin{align*}
f _{w, b} &= w _{1} x _{1}+  w _{2} + x _{2} + \dots + w _{n} x _{n} + b\\
& \vec{w} =
\begin{bmatrix}
w _{1} & w _{2} & w _{3} & \dots & w _{n}
\end{bmatrix} ^{\top}\\
& b \text{ is a number}\\
& \vec{x} =
\begin{bmatrix}
x _{1} & x _{2} & x _{3} & \dots & x _{n}
\end{bmatrix} ^{\top}\\
\rightarrow& f _{\vec{w}, b} (\vec{x}) = \underbrace{ \vec{w} \cdot \vec{x} } _{\text{dot product}} + b\\
\end{align*}
$$

### Vectorization

$$
\begin{align*}
f _{\vec{w}, b} &= \vec{w} \cdot \vec{x} + b\\
&= \left( \sum_{j=1}^{n} w _{j} x _{j} \right) + b
\end{align*}
$$

```python
w = np.array([1.0, 2.5, -3.3])
b = 4
x = np.array([10, 20, 30])
f = np.dot(w, x) + b
```

### Gradient descent for multiple features with vectorization

$$
\begin{align*}
\vec{w} &=
\begin{bmatrix}
w _{1} & w _{2} & \dots & w _{n}
\end{bmatrix}\\
b &\text{ a number}\\
f _{\vec{w}, b} (\vec{x }) &= \vec{w } \cdot \vec{x} + b
\end{align*}
$$

![picture 2](../../../images/a3acbb1602b53ba92ea88514ee7bf409f9197b637b41aae53321ed52d5f8e0a0.png)  

### An alternative to gradient descent

Normal equation

- Only for linear regression
- Solve for $ w, b $ without iterations

Disadvantages

- Doesn't generalize to other learning algorithms
- Slow

## Feature Scaling

Mean normalization

$$
\begin{align*}
x _{1} &= \frac{x _{1} - \mu _{1}}{\max(x _{1}) - \min (x _{1})}\\
& \mu: \text{ mean of } x _{1}
\end{align*}
$$

Z-score normalization

$$
\begin{align*}
x _{1} &= \frac{x _{1} - \mu _{1}}{\sigma _{1}}\\
\sigma&: \text{standard deviation}
\end{align*}
$$

## Feature Engineering

$$
\dots
$$
