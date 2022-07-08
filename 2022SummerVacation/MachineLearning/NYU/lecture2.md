# Lecture 2

## General Notation

---

$$
\begin{align*}
&\text{data set} \coloneqq D = \left\{ x ^{(i)}, t ^{(i)}\right\} _{i=1} ^{N} && \text{Number of training example}\\
& x ^{(i)} = \left[ x _{1} ^{(i)}, x _{2} ^{(i)}, \dots, x _{D} ^{(i)} \right] =
\begin{bmatrix}
x _{1} ^{(i)}\\
x _{2} ^{(i)}\\
\vdots \\
x _{D} ^{(i)}
\end{bmatrix}
\in \mathbb{R} ^{D} = \mathbb{R}^{D \times 1}
&& D=\text{Number of features}
\end{align*}
$$

---

$ t ^{(i)} \in \mathbb{R} $: labels | annotations | output variables
$ \left( x ^{(i) } , t ^{(i)}\right) =$ training sample
$ \left\{ x ^{(i)}, t ^{(i)} \right\} _{i=1} ^{N} $ is called the **training set**
$ x: \text{input space} \subseteq \mathbb{R}^{D} $
$ y: \text{output space} \subseteq \mathbb{R} $

**General idea in supervised learning:** learn a mapping $ h $
from $ x $ to $ y $ such that $ h \left( x ^{(i)} \right) $ is a good prediction for $ t ^{(i)} $

$ h: $ hypothesis
$ \rightarrow $ how to represent and show the hypothesis?
$ \rightarrow $ reasonable idea: limit ourselves to limit number of parameters

## Linear Regression

How to learn a good model $ h $ on $ \left\{ x ^{(i)}, t ^{(i)} \right\} _{i = 1} ^{N} $, such that $ h \left( x ^{(i)} \right) \approx t ^{(i)} $

Question $ 1 $: what would be a good representation for $ h $?
Question $ 2 $: how can we learn the representation?

Q1: How about we take $ h $ to be a linear combination of the features:

$$
\begin{align*}
h (x ^{(i)}) &= \beta_{0} + \beta_{1} x ^{(i)}\quad (D = 1)\\
h (x ^{(i)}) &= \beta_{0} + \beta_{1} x _{1} ^{(i)} + \beta_{2} x _{2} ^{(i)} + \dots + \beta_{D} x _{D} ^{(i)}
\end{align*}
$$

**NOTATION**:

**linear model**:

$$
\begin{align*}
h(x ^{(i)}) = \beta _{0} + \sum_{j=1}^{D} x _{j} ^{(i)} \beta _{j}
\end{align*}
$$

For a more compact representation, we consider introduce a new notation:

==Notation==

---

$$
\begin{align*}
\tilde{ x }^{(i)} &= [1, x ^{(i)}]\\
&= \left[ 1, x _{1} ^{(i)}, x _{2} ^{(i)}, \dots, x _{D} ^{(i)} \right]\\
&=
\begin{bmatrix}
1 \\
x _{1} ^{(i)}\\
\vdots\\
x _{D} ^{(i)}
\end{bmatrix}
\in \mathbb{R}^{D}
\end{align*}
$$

---

thanks to this notation, we can now write $ h(x ^{(i)}) $ as

$$
\begin{align*}
h(x ^{(i)}) &= \beta ^{T} \tilde{ x } ^{(i)} &&= \beta_{0}\cdot 1 + \beta_{1} \tilde{ x _{1} }  ^{(i)} + \beta_{2} \tilde{ x _{2}  }  ^{(i)} + \dots + \beta_{D} \tilde{ x _{D} } ^{(i)}\\
&&&= \beta_{0} + \beta_{1} x _{1} ^{(i)} + \beta_{2} x _{2} ^{(i)} + \dots + \beta_{D} x _{D} ^{(i)}\\
&= \left<\beta, \tilde{ x } ^{(i)}\right> &&= \sum_{j=1}^{D} \beta _{j} \tilde{ x } _{j} ^{(i)}
\end{align*}
$$

Q2:Now that we have a representation for $ h $, how can we learn this representation

In order to assess the quality of a model, we need a cost function. ( = loss function of our learning algorithm )

==cost function== it's a function determines how well a Machine Learning model performs for a given set of data. The Cost Function calculates the difference between anticipated and expected values and shows it as a single real number.

$ \rightarrow $ our approach is to measure distance between $ h(x ^{(i)}) $ and $ t ^{(i)} $ for example by considering the sum of the squares of those deviations.

$$
\text{loss function:}\quad J(\beta) = \frac{1}{2N} \sum_{i=1}^{N} (t ^{(i)} - h(x ^{(i)})) ^{2}
$$

In this case $ J(\beta) $ is know as the ordinary least squares (OLS) loss. It is also sometimes knows as Residual Sum of Squares loss (RSS).

Question 2b: how can we use $ J(\beta) $ in order to learn $ h $?

Approach I: Minimize $ J(\beta) $ with respect to $ \beta _{0}, \beta _{1}, \dots, \beta _{D} $

$ \rightarrow $ to achieve this minimization, we can turn to the `Gradient descent algorithm`

Seeing back to $ J (\beta) $, how can we apply this idea?

> start from an arbitrary initial guess $ (\beta _{0} ^{(0)}, \beta _{1} ^{(0)} ) $ and then move in the direction opposite the gradient (the steepest descent direction)

Step 1: generate initial value for $ \beta _{0}, \beta _{1}, \dots, \beta _{D} $
Step 2: find the derivative of $ J(\beta) $ with respect to $ \beta _{0}, \beta _{1}, \dots, \beta _{D} $

$$
\begin{align*}
\frac{\partial J}{\partial \beta _{k} } &= \frac{\partial }{\partial \beta _{k}} \frac{1}{2N} \sum_{i=1}^{N} \left( t ^{(i)} -\left( \beta _{0} + \beta _{1} x ^{(i)} _{1} + \dots + \beta _{D} x ^{(i)} _{D} \right) \right) ^{2}\\
&= \frac{1}{N} \sum_{i =1}^{N} \left( t ^{(i)} - \left( \beta _{0} + \beta _{1} x ^{(i)} _{1} + \dots + \beta _{D} x ^{(i)} _{D} \right) \right) \cdot (- \tilde{ x _{k}  }^{(i)} )
\end{align*}
$$

Step 3: define the gradient as the vector of all $ \frac{\partial J}{\partial \beta _{k}} $
$$
\text{grad } = \left[ \frac{\partial J}{\partial \beta _{0}}, \dots, \frac{\partial J}{\partial \beta _{D}} \right]
$$

Step 4: Move one step in the direction opposite the gradient

$$
\beta ^{l + \eta} \leftarrow \beta ^{l} - \eta \cdot grad _{\beta}J\quad (*)
$$

$ \eta $: the learning rate (step size)

Repeat

$ (*) $ is know as the LHS (lease mean square) or Window Hoff Update

---

When implementation gradient descent, there are two main approaches

1. `Batch Gradient descent`: carry out each step by processing the whole set of training example $ \left\{ t ^{(i)}, x ^{(i)} \right\} _{i=1} ^{N} $ (convergence more accurate but more costly)
2. `Stochastic Gradient descent`: only use one example at each gradient step

`Batch Gradient descent:`

For  $iter < MaxIter$

$$
\beta \leftarrow \beta - \eta \sum_{i = 1 }^{N} (t ^{(i)} - h _{\beta} (x ^{(i)})) (-\tilde{ x } ^{(i)})
$$

`Stochastic Gradient descent`

For $ epoch < MaxNumEpochs $

reshuffle the set $ \left\{ t ^{(i)}, x ^{(i)} \right\} _{i =1} ^{N} $

For $ i \in [1,\dots, N] $

$$
\beta \leftarrow \beta - \eta \left( t ^{(i)} - h _{\beta} (x ^{(i)}) \right) (- \tilde{ x } ^{(i)} )
$$
