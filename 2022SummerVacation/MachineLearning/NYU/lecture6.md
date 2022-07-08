# Lecture 6

Today:

- Classification
- Binary least squares classifier (separating pane)
- Extensions to Multiple classes
  - One vs. rest / one vs. other / k class discriminate
- Probabilistic classifier (in particular, logistic regression)

General idea: Assign to our feature vectors one of $ k $  discrete classes $ C _{1}, \dots, C _{k} $
$ \rightarrow $ the result of this is a classifier of the input space into decision regions where boundaries are called decision boundaries

We will start with simple model for which the decision boundaries are linear functions of the input vectors
$ \rightarrow $ Datasets whose classes can be separated exactly by linear decision surfaces are called **linear separable**

$ \rightarrow $ one of the most convenient representation for class labels is to take
$$
t ^{(i)} = \left\{ 0, 1 \right\}
$$

For multi-class problems, we will use a one-hot encoding system.
E.g., if we have $ k $ classes, a feature vector from class $ C _{2} $ will be represented as
$$
\vec{t} = [0, 1, 0, \dots, 0] \in \mathbb{R}^{k}
$$

Discriminate function takes a feature vector as input and assigns it to one of the $ k $ classes.

We will start with a linear discriminant of the form
$$
y(x) = \beta ^{\top} x + \beta _{0}
$$
and the **decision boundary** is given by $ y(x) = 0 $

Assuming
$$
\begin{align*}
&t ^{(i)} = 1\rightarrow x ^{(i)} \in C _{1}\\
&t ^{(i)} = -1\rightarrow x ^{(i)} \in C _{2}\\
\end{align*}
$$
a new point will be assigned
$$
\begin{align*}
C _{1} &\text{ if } y(x) > 0\\
C _{2} &\text{ if } y(x) < 0\\
\end{align*}
$$

**General Objective:**
Learn the discriminant function $ y(x) $ that returns a positive value for feature in class $ C _{1} $, negative value for feature in class $ C _{2} $.

$ \rightarrow $ One of the simplest approach to learn our classifier is through the least squares
$$
\beta ^{*} = \text{argmin} _{\beta } \frac{1}{N} \sum_{i=1}^{N}
\left( t ^{(i)} - \left( \beta _{0}+ \beta _{1} x _{1} ^{(i)}+ \dots+ \beta _{D} x _{D} ^{(i)}  \right) \right) ^{2}
$$

How about Multiple class setting?

Solution 1:
Learn $ k-1 $ binary classifiers which separate each of the classes $ c _{1}, \dots, c _{k-1} $ from the rest of the dataset
==(One vs. all | One vs. the rest)==

Solution 2:
Learn a set of $ \frac{k(k-1)}{2} $ classifiers separating class $ C _{i} $ from class $ C _{j} $
$ \rightarrow $ class of a new point is determined based on the outcomes of the $ \frac{k(k-1)}{2} $ classifiers following a majority vote

If we learn each classifier one by one, there might be features be classified as having multiple classes
$ \rightarrow $ In order to reduce those ambiguities, we can rely on a single $ k $ class discriminant function (learn $ k $ discriminant functions at once.)

Solution 3:
Single $ k $ class discriminant classifier (least squares), relying on one hot encoding of the $ t ^{(i)} $

$ \rightarrow $ encode the targets using a $ 1 $ of $ k $ coding scheme
$$
\begin{align*}
t ^{(i)} &=
\begin{bmatrix}
0\\1\\0\\\vdots\\0
\end{bmatrix}
\rightarrow \text{ from which we can define the target matrix}\\
\underline{\underline{T}} &=
\begin{bmatrix}
\vert &\vert &\dots &\vert\\
t ^{(1)}& t ^{(2)}&\dots & t ^{(N)}\\
\vert &\vert &\dots &\vert\\
\end{bmatrix}
\in \mathbb{R}^{k \times N}
\end{align*}
$$

We then consider a set of $ k $ separating planes $ \beta _{k} $ which we store as the rows of $ B $
$$
\begin{align*}
\underline{\underline{B}} =&
\begin{bmatrix}
\vec{\beta } _{1} ^{\top}\\
\vdots\\
\vec{\beta } _{k} ^{\top}\\
\end{bmatrix}\\
&\text{where each } \vec{\beta } _{k} \text{ is a vector}\\
&\vec{\beta } _{k} = [\beta _{k0}, \beta _{k1}, \dots, \beta _{kD}]\in \mathbb{R}^{D+1}
\end{align*}
$$

We can then write the deviations between the targets and the targets and the predictions from the discriminant function as
$$
\begin{align*}
\underline{\underline{T}} - \underline{\underline{B}}\cdot \underline{\underline{\tilde{ X }}}^{\top} &=
\begin{bmatrix}
\vert &\vert &\dots &\vert\\
t ^{(1)}& t ^{(2)}&\dots & t ^{(N)}\\
\vert &\vert &\dots &\vert\\
\end{bmatrix}-
\begin{bmatrix}
\vec{\beta } _{1} ^{\top}\\
\vdots\\
\vec{\beta } _{k} ^{\top}\\
\end{bmatrix}
\underbrace{
    \begin{bmatrix}
    \vert &\dots &\vert\\
    \tilde{ x } ^{(1)} &\dots & \tilde{ x } ^{(N)}\\
    \vert &\dots &\vert\\
    \end{bmatrix}
} _{\underline{\underline{\tilde{ X }}}^{\top}}
\end{align*}
$$

Recall that
$$
\tilde{ \underline{\underline{X}} } =
\begin{bmatrix}
1 &x _{1} ^{(1)} &x _{2} ^{(1)} &\dots & x _{D} ^{(1)}\\
1 &\vdots &\vdots &\vdots &\vdots\\
1 &x _{1} ^{(N)} &x _{2} ^{(N)} &\dots &x _{D} ^{(N)}
\end{bmatrix}
$$

we can then minimize the sum of square loss as before
$$
\frac{1}{Nk} \sum_{i=1}^{N} \sum_{j=1}^{k}
\left( t _{j} ^{(i)} - \vec{\beta } _{j} ^{\top}\tilde{ x }^{(i)} \right) ^{2}
\quad (*)
$$

Notation: trace of a matrix
$$
Tr(\boldsymbol{A}) = \sum_{i=1}^{N} A _{ii}
$$

Minimizing $ (*) $ is equivalent to looking for a set of planes where the plane associated with the $ k ^{th} $ classifier outputs a value as close as possible to $ 1 $ for points that are in $ C _{k} $ and $ 0 $ otherwise.

$$
\begin{align*}
(**) &= \text{sum of squared entries of the matrix } T - \underline{\underline{B}}\cdot\underline{\underline{\tilde{ X }}}\\
&= Tr((\underline{\underline{T}} - \underline{\underline{B}}\cdot \underline{\underline{\tilde{ X }}}^{\top}) ^{\top} (\underline{\underline{T}} - \underline{\underline{B}}\cdot \underline{\underline{\tilde{ X }}} ^{\top}))
\end{align*}
$$

$ \rightarrow $ compute the derivative of $ (**) $ with respect to $ \underline{\underline{B}} $ and setting it to $ 0 $, we get a matrix equivalence of the normal equations which we can solve for $ \underline{\underline{B}} $
$$
\underline{\underline{B}}^{\top} =
\left(
    \underline{\underline{\tilde{ X }}} ^{\top} \underline{\underline{\tilde{ X }}}
 \right)^{-1}
 \underline{\underline{\tilde{ X }}} ^{\top}
 \underline{\underline{T}} ^{\top}
$$
