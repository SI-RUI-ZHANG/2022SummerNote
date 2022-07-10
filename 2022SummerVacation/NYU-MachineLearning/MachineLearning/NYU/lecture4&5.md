# Lecture 4

Today

- overfitting
- Bias Variance Decomposition
- Regularization
  - Best Subset Selection
  - Ridge regression
  - Lasso
- Statistical intuition (Ridge/Lasso)

## Bias Variance Decomposition

$$
\begin{align*}
h _{\beta } (x ; D _{i}) &: \text{hypothesis}/\text{model learned from the training set}\\
& D _{i} \subseteq D = \left\{ (x ^{(i)}, t ^{(i)}) \right\}
\end{align*}
$$

To measure how good a hypothesis $ h _{\beta }(x) $ is for a dataset $ D $, we consider the **MSE**
`MSE`: mean square error

$$
MSE(x) = \mathbb{E} _{D _{i}} \left\{ ( t(x) - h _{\beta }(x; D _{i})) ^{2} \right\}
$$

_How does the model learned from dataset $ D _ {i} $ perform on the whole data set $ D $?_

$$
\begin{align*}
MSE (x) &= \mathbb{E} _{D _{i}} \left\{ (t (x) - \mathbb{E} _{D _{i}} h _{\beta}(x; D _{i}) +  
\mathbb{E} _{D _{i}} h _{\beta } \left( x; D _{i} \right) - h _{\beta }(x; D _{i}) ) ^{2} \right\}\\
&= \mathbb{E}_{D _{i}} \left\{ (t (x) - \mathbb{E}_{D _{i}} h _{\beta } (x; D _{i})) ^{2} \right\}\\
&\quad+
    \mathbb{E} _{D _{i}} \left\{
    (\mathbb{E}_{D _{i}} h _{\beta }(x; D _{i}) - h _{\beta }(x; D _{i})) ^{2}
    \right\}\\
&\quad+
\underbrace{
    2 \mathbb{E}_{D _{i}}
    \left\{
        (t (x) - \mathbb{E}_{D _{i}} h _{\beta }(x; D _{i}))
        (\mathbb{E}_{D _{i}}h _{\beta }(x; D _{i}) - h _{\beta }(x; D _{i}))
    \right\}\\
 } _{=0}\\
 &= \underbrace{ (t (x) -\mathbb{E} _{D _{i}} h _{\beta }(x; D _{i}))^{2} } _{\text{bias}^{2}}
 +\underbrace{ \mathbb{E}_{D _{i}} \left\{ (h _{\beta }(x; D _{i})-\mathbb{E}_{D _{i}} h _{\beta }(x; D _{i})) ^{2}\right\} } _{\text{variance}}\\
 & \text{here the last term is omitted since it's equal to } 0
\end{align*}
$$

How can we automatically select the optimal complexity?

$ \rightarrow $ Regularization

- Best Subset Selection (cannot apply on large data set)
- Ridge Regression
- LASSO

## Best Subset Selection

Find the optimal subset of the features

$ \rightarrow $ Total numbers $ \begin{pmatrix} D\\k \end{pmatrix} $ for every $ k=1,\dots,D $
For each subset:

1. Fit the model to the dataset
2. Evaluate trained model on same new (test) dataset
3. Select the subset of the features that gives the best prediction error

We can select the best model through cross validation ($ k $ fold cross validation)

1. split the data set into $ k $ bins
2. for each $ i= 1,\dots, k $ train the model on all the bins but the $ i ^{th} $ one and evaluate it on the $ k ^{th} $ bin
3. the error for this model if the mean error for each $ i=1,\dots,k $

_Leave-one-out_ cross validation:
Train the model on $ D $ but one example and evaluate $ h _{\beta } $ on the remaining example.
The error for the $ i ^{th} $ example
$$
MSE _{i} = (t ^{i} - h _{\beta } ^{i=k}(x ^{(i)})) ^{2}
$$
The **Cross Validation Error**:
$$
error _{CV} = \frac{1}{N} \sum_{i=1}^{N} MSE _{i}
$$

## Ridge Regression

Recall

$$
\begin{align*}
l _{OSL} (\beta ) &= \frac{1}{N} \sum_{i =1}^{N} ( t ^{(i)} - h _{\beta }(x ^{(i)})) ^{2}\\
&= \frac{1}{N} \sum_{i=1}^{N} ( t^{(i)} - \beta ^{\top}\tilde{ x }^{(i)}) ^{2}
\end{align*}
$$

**Ridge loss**:

$$
l _{Ridge}(\beta ) = \frac{1}{N} \sum_{i=1}^{N} ( t ^{(i)} - \beta ^{\top}\tilde{ x }^{(i)}) ^{2}
+\lambda \underbrace{ \sum_{j=1}^{D} \left| \beta _{j} \right| ^{2} } _{\text{notice that we start from }j = 1}
$$

We do **not** penalize the intercept $ \beta _{0} $

## LASSO Regression

**LASSO LOSS**:

$$
l _{LASSO} (\beta ) = \frac{1}{N} \sum_{i=1}^{N}
(t ^{(i)} - \beta ^{\top}\tilde{ x }^{(i)}) ^{2} +
\lambda \sum_{i=1}^{D} \left| \beta _{j} \right|
$$

## Ridge vs. LASSO

### Ridge

$ \rightarrow $ complexity:
Ridge can be solved through gradient descent (differentiable everywhere).
If fact, we can use the Normal Equation for Linear Regression on Ridge Regression to solve for $ \beta _{Ridge} $ (regression vector that minimizes the Ridge loss)

---

$$
\text{grad} _{\beta } l _{Ridge} =
(\underline{\underline{X}}^{\top}\underline{\underline{X}}+ \lambda I) ^{-1}
\underline{\underline{X}} ^{\top} \tilde{ t }
$$

---

Advantage of Ridge vs OLS: even if $ \underline{\underline{X}}^{\top} \underline{\underline{X}} $ was not invertible, as soon as $ \lambda > 0 $, the matrix
$$
(\underline{\underline{X}}^{\top}\underline{\underline{X}}+ \lambda I)
$$
which shifts the eigenvalue of $ \underline{\underline{X}}^{\top}\underline{\underline{X}} $ by $ \lambda > 0 $ ==is always invertible==

### LASSO

For LASSO, not that $ \left| \beta _{j} \right| $ is not differentiable as zero

$ \rightarrow $ gradient descent will not work
$ \rightarrow $ $ \beta _{LASSO} $ cannot be obtained from solving a linear system (like OSE and Ridge)
$ \rightarrow $ However, LASSO will be better at performing feature selection
