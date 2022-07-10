# Lecture 8

---
Bayes Rule:

$$
p(A|B) = p(A)\frac{p(B|A)}{p(B)}
$$

---

## Discriminative vs. Generative

$ \rightarrow $ Discriminative classifier
(given a feature vector $ x ^{(i)} $, a discriminative model outputs a decision)
$$
\text{learns a model for }  p(t|x)
$$

$ \rightarrow $ Generative classifier
learns a representation of what the object on the two classes looks like, and then classify a new example based on how it compares to out model of what typical instance should look like
$$
\text{learns a model for }  p(x|t)
$$

Probabilistic classifier

- Discriminative classifier $ p(t|x) $
- Generative classifier $ p(x|t) $
  - Gaussian Discriminant Analysis (GDA)
  - Quadratic Discriminant Analysis (QDA)
  - Linear Discriminant Analysis (LDA)
- LDA and Logistic Regression Comparison

---

## Generative Classifier

> $$
> \begin{align*}
> &x \in \mathbb{R}^{D}\\
> &\left\{ x ^{(i)}, t ^{(i)} \right\} _{i= 1} ^{N}
> \end{align*}
> $$

1. learn a model for $ p(x|t) $
2. to classify a new prototype, use Bayes rule
$$
\begin{align*}
p(t|x) &= \frac{p(x|t)p(t)}{p(x)}
&=
\frac{p(x|t)p(t)}{\sum_{\forall c}^{}p(x|t=c)p(t=c)}
\end{align*}
$$

in order to determine the class of a new point $ x ^{(i)} $ we maximize $ p(t = t _{c}|x ^{(i)}) $ over $ t _{c} $

$$
t (x ^{(i)}) = \text{argmax} _{t _{c}} p(t=t _{c} | x ^{(i)}) = \text{argmax} _{t _{c}}
\frac{p(x ^{(i)}|t= t _{c}) p(t = t _{c})}{\underbrace{ \sum_{\forall c'}^{} p(x ^{(i)}|t = t _{c'})p(t = t _{c'}) } _{denominator}}
$$

the denominator is constant across the $ t _{c}'s $, we can just focus on the numerator, and define our class as
> $$
> t (x ^{(i)}) = \text{argmax} _{t _{c}} p(x ^{(i)}| t = t _{c}) p(t = t _{c})
> $$
> $ \rightarrow $ to determine the class of a new prototype $ x ^{(i)} $ based on a generative classifier, we therefore need a model for $ p(x|t) $ and for $ p(t) $

$ \rightarrow $ One of the simplest model for $ p(x|t) $  is the Multivariate Normal Distribution ==Gaussian Distribution==
For $ p(t) $ a reasonable to use Binomial Distribution
$$
\begin{align*}
p(t=0) &= \Pi _{0}\\
p(t = 1) &= \Pi _{1} \\
&= 1 - \Pi _{0}
\end{align*}
$$

$$
\begin{align*}
p(x|t=t _{c}) = \frac{1}{(2 \pi) ^{D/2} \left| \sum \right| ^{1/2}}
\exp(-\frac{1}{2}(x - \mu _{c}) ^{\top} \sum_{c}^{-1}(x - \mu _{c}))
\end{align*}
$$

$ \rightarrow $ Together these models describe the Gaussian Discriminant Analysis generative classifier

In logistic regression we trained our model following a Maximum likelihood approach on $ p(t|x)$

> Joint Distribution:
> When training generative classifier we will again use a Maximum likelihood approach but this time on $ p(\left\{ x, t \right\}) $

For the GDA model, recall that we have

$$
\begin{align*}
p(x|t=t _{c}) &= \frac{1}{(2 \pi) ^{D/2} \left| \sum \right| ^{1/2}}
\exp(-\frac{1}{2}(x - \mu _{c}) ^{\top} \sum_{c}^{-1}(x - \mu _{c}))\\
p(t = t _{c}) &= \Pi _{c}\\
p(\left\{ x, t \right\}) &= p(x|t)p(t)
\end{align*}
$$

Assume all of our example are independent, we can write $ p(\left\{x ^{(i)}, t ^{(i)} \right\}) _{i=1} ^{N} $ as
$$
\begin{align*}
p\left(\left\{ x ^{(i)}, t ^{(i)} \right\} _{i=1} ^{N}\right) =
\prod _{i=1} ^{N} p\left(\left\{ x ^{(i)}, t(x ^{i}) = t ^{(i)} \right\}\right)\quad (*)
\end{align*}
$$

notice that

$$
p\left(\left\{ x ^{(i)}, t (x ^{(i)}) = c \right\}\right)=
\begin{cases}
p\left(x ^{(i)}| t (x ^{(i)}) = c\right)
p \left( t (x ^{(i)}) = c \right) &\quad\text{if } c = t ^{(i)}\\
0 &\quad\text{otherwise}
\end{cases}
$$

then

$$
\begin{align*}
p \left( \left\{ x ^{(i)}, t ^{(i)} \right\} _{i=1} ^{N} \right)=
\left(
 p\left(x ^{(i)}| C _{0}) = 0\right)
 p ( C _{0} )
\right)^{1 - t ^{(i)}}
\left(
 p\left(x ^{(i)}| C _{1}) = 0\right)
 p ( C _{1} )
\right)^{t ^{(i)}}
\end{align*}
$$

> For LDA Setting, we get closed form expressions for each of the $ \mu _{0}, \mu _{1}, \Sigma, \Pi _{0} $ by computing the derivative and setting to $ 0 $
> $$
> \begin{align*}
> \phi &= \frac{\sum _{i=1} ^{m} y ^{(i)}}{m}\\
> &=\frac{\sum _{i=1} ^{m}1\left\{ y ^{(i)}=1 \right\}}{m}\\
> \mu _{0} &=
> \frac{\sum_{i=1}^{m}1\left\{ y ^{(i)} =0 \right\} x ^{(i)}}
> {\sum_{i=1}^{m}1 \left\{ y ^{(i)} = 0 \right\}}\\
> \mu _{1} &=
> \frac{\sum_{i=1}^{m}1\left\{ y ^{(i)} =1 \right\} x ^{(i)}}
> {\sum_{i=1}^{m}1 \left\{ y ^{(i)} = 1 \right\}}\\
> \Sigma &=
> \frac{1}{m} \sum_{i=1}^{m}
> (x ^{(i)}- \mu _{y ^{(i)}})
> (x ^{(i)}-\mu _{y ^{(i)}})^{\top}
> \end{align*}
> $$
> _from Andrew_

In our lecture

$$
\begin{align*}
\Pi _{0} &= \frac{N _{0}}{N _{0} + N _{1}}\\
\mu _{0} &= \frac{1}{N _{0}} \sum_{i\in C _{0}} x ^{(i)}\\
\mu _{1} &= \frac{1}{N _{1}} \sum_{i\in C _{1}} x ^{(i)}\\
\Sigma &= \frac{1}{N}
\left\{
\sum_{i\in C _{0}}(x ^{(i)} - \mu _{0})(x ^{(i)- \mu _{0}})^{\top}
+
\sum_{i\in C _{1}}(x ^{(i)} - \mu _{1})(x ^{(i)- \mu _{1}})^{\top}
\right\}
\end{align*}
$$
