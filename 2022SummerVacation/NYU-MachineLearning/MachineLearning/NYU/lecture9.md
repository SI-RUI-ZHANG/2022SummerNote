# Lecture 9

Today

Generative Classifier

- Linear Discriminant Analysis
- Connection between LDA & Logistic Regression
- Native Bayes Classifier

> LDA (Linear Discriminant Analysis), or normal discriminant analysis

## Connection between LDA & Logistic Regression

**Notation**:

$$
\propto: \text{ proportion to}
$$

$$
\begin{align*}
\Theta &= ( \Pi _{0}, \mu_{0}, \mu _{1}, \Sigma)\quad \text{(vector of parameters)}\\
c &= \text{class, in binary setting } c \in \left\{ 0, 1 \right\}\\
\end{align*}
$$

In LDA, we'll find that

$$
\begin{align*}
p(t = c| x, \Theta) = \frac{1}{1 + \exp(-\theta ^{\top}x)}
\end{align*}
$$

where $ \theta  $ is some appropriate function of elements of $ \Theta $
> Therefore, LDA can be read as a particular instance of a logistic classifier

## Naive Bayes Classifier

> assume independence of features

$ \rightarrow $ Generative classifier

$$
p(x | y=c, \theta) = \prod _{j=1 } ^{D} p(x _{j}|y = c, \theta _{jc})
$$

Depending on the type of the features we should cite the Gaussian Naive Bayes (features are real valued)

$$
p(x|y = c, \theta ) = \prod _{j=1} ^{D} N (x _{j}| \mu _{jc}, \sigma ^{2} _{jc})
$$

Bernoulli naive bayes (binary features)

$$
p(x|y=c, \theta ) = \prod _{j=1}^{D} Ber(x _{j}| \mu _{jc})
$$

Categorical Naive Bayes (categorical features $ x _{j}\in \left\{ 1, \dots, k \right\} $)

$$
\begin{align*}
&p(x|y=c, \theta ) = \prod _{j=1}^{D} Cat(x _{j}| p _{jc})\\
&\text{pick probabilities with } \Sigma _{k} p _{jck} = 1 \quad
p _{jck} \ge 0
\end{align*}
$$

## Perceptron

$ \rightarrow $ combination of linear model with Heaviside activation

$$
\begin{align*}
\sigma(x) &=
    \begin{cases}
    1 &x>0\\
    -1 &x\le 0
    \end{cases}\\
y(x) &= \sigma (\beta ^{\top} \tilde{ x })
\end{align*}
$$

$ \rightarrow $ model cannot be trained in the usual manner as the gradient vanishes almost everywhere

$$
\text{data set: } \left\{ x ^{(i)}, t ^{(i)} \right\} _{i=1} ^{N}\\
\text{label: } t ^{(i)} \in \left\{ 1, -1 \right\}
$$

we define the loss function as

$$
l(\beta ) = - \sum _{i\in \text{misclassified}} t ^{(i)}
(\beta _{0} + \beta _{1} x _{1} ^{(i)} + \dots + \beta _{D} x _{D} ^{(i)})
$$

we then minimize $ l(\beta ) $ with respect to $ \beta  $ and then recompute the new set of misclassified examples

For a point that is strongly misclassified, we have $ sign(t ^{(i)})\ne sign(\beta ^{\top}\tilde{ x } ^{(i)}) $, hence a large contribution to the loss
Minimizing the loss will then 'correct' value  $ \beta  $ based on the misclassified points

$ \rightarrow $ the loss can be minimize using stochastic gradient descent approach over the misclassified points

$ \rightarrow $ In this setting, the SGD iterations are give by

$$
\begin{align*}
\beta &\leftarrow \beta - \eta \text{ grad} _{\beta } l(\beta )\\
\beta &\leftarrow \beta - \eta \tilde{ x } ^{(i)}t ^{(i)} \quad \text{(perceptron learning rule)}
\end{align*}
$$

$ \rightarrow $ resulting perceptron algorithm applies the step iteratively on the misclassified points

> for every misclassified $ \tilde{ x } ^{(i)} $, do
>$$
>\beta \leftarrow \beta - \eta \tilde{ x } ^{(i)}t ^{(i)} \quad \text{(perceptron learning rule)}
>$$
