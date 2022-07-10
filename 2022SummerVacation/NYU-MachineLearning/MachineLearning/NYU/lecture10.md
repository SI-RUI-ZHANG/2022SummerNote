# Lecture 10

So far we have covered a collection of classifiers, which can all read as the general form "activation + linear model"

$$
\begin{align*}
\rightarrow \text{linear model: }
&\sigma (\beta _{0}+\beta _{1}x _{1}+\dots+\beta _{D}x _{D})\\
&\sigma (x) = x\\
\rightarrow \text{logistic regression: }
&\sigma (\beta _{0}+\beta _{1}x _{1}+\dots+\beta _{D}x _{D})\\
&\sigma (x) = \frac{1}{1 + e ^{-x}}\\
\rightarrow \text{perceptron: }
&\sigma (\beta _{0}+\beta _{1}x _{1}+\dots+\beta _{D}x _{D})\\
&\sigma (x) =
    \begin{cases}
    1 \quad& x\ge0\\
    -1 \quad& x<0
    \end{cases}
\\
\end{align*}
$$

$ \rightarrow $ general structure can be captured by a simple diagram (neuron)

Backpropagation

$ \rightarrow $ we consider a simple binary classification setting (just like logistic regression except that this time class probability is defined by the network)

$$
\begin{align*}
y(x)\text{denoting the network}&\\
p(t ^{(i)}=1|x ^{(i)}) &= y (x ^{(i)})\\
p(t ^{(i)}=0|x ^{(i)}) &= 1- y (x ^{(i)})
\end{align*}
$$

Feed Forward Fully Connected Neural Network

At $ k ^{th} $ unit from layer $ l $ can be encoded by a combination
"linear combination + activation function" as
$$
\begin{align*}
a _{k} ^{(l)} &=
\sum_{j=1}^{N _{l} - 1} w _{kj} ^{(l)} z _{j} ^{(l-1)}
\rightarrow \text{pre-activation}
\\
z _{k} ^{(l)} &= \sigma (a _{k} ^{(l)})
\rightarrow \text{post-activation}
\end{align*}
$$

$ \rightarrow $ the network's weights can be learned (like logistic regression) by maximizing the likelihood defined on the training sets
$$
\left\{ x ^{(i)}, y ^{(i)} \right\} _{i=1} ^{N}
$$

## Probability of observing the training sets

$$
\begin{align*}
p(\left\{ x ^{(i)}, t ^{(i)} \right\} _{i=1} ^{N}) &=
\prod _{i=1} ^{N} y (x ^{(i)}) ^{t ^{(i)}} (1- y (x ^{(i)})) ^{1 - t ^{(i)}}\\
\log\left(p(\left\{ x ^{(i)}, t ^{(i)} \right\} _{i=1} ^{N}) \right)&=
\underbrace{ \sum_{i=1}^{N} t ^{(i)} \log (y (x ^{(i)})) + (1- t ^{(i)})\log(1-y(x ^{(i)})) }
_{\text{binary cross entropy/log loss}}
\end{align*}
$$

$ \rightarrow $ In order to train the network through gradient descent, we then need compute the gradient of the log loss with respect to the network's parameters which are hidden in the expression of $y(x ^{(i)})$
