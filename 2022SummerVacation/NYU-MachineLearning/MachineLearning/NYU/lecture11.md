# Lecture 11

General architecture

$ w _{ij} ^{l} $ is the weight in the $ i ^{th} $ neuron from layer $ l $ that multiplies the $ j ^{th} $ input to this network

Using our network to encode class probabilities,

$$
\begin{align*}
p(t ^{(i)}= 1|x ^{(i)}) &= y (x ^{(i)}; w)\\
p(t ^{(i)}= 0|x ^{(i)}) &= 1 - y (x ^{(i)}; w)
\end{align*}
$$

we can train the network via a maximum likelihood approach, corresponding to a minimization of the log loss.

$$
l(w) = - \sum_{i=1}^{N}
\left\{
t ^{(i)} \log(y(x ^{(i)}; w)) +
(1- t ^{(i)})\log(1-y(x ^{(i)}; w))
\right\}
$$

$ \rightarrow $ in particular, if we use SGD, optimizing one sample at a time, the loss reduce to

$$
l(w) = -t ^{(i)}\log(y(x ^{(i)}; w)) - (1- t ^{(i)})\log (1-y(x ^{(i)};w))
$$

To implement the training of neural network through SGD, we need the derivatives
$$
\frac{\partial L}{\partial w _{ij} ^{(l)}}
$$

$ \rightarrow $ use the fact that

$$
\begin{align*}
a _{i} ^{l} &= \sum_{j=1}^{N _{l}} w _{ij} ^{l}z _{j} ^{(l-1)}
+w _{i0} ^{l}\\
\rightarrow \text{From this} &
\frac{\partial L}{\partial w _{ij} ^{l}}=
\frac{\partial L}{\partial a _{i} ^{(l)}}\cdot
\frac{\partial a _{i} ^{l}}{\partial w _{ij} ^{(l)}}=
\frac{\partial L}{\partial a _{i} ^{(l)}}\cdot
z _{j} ^{(l-1)}
\end{align*}
$$

We will now use

$$
\delta_{i} ^{(l)} = \frac{\partial L}{\partial a _{i} ^{(l)}}
$$

From this, we get

$$
\begin{align*}
\frac{\partial L}{\partial w _{ij} ^{(l)}} &=
\delta _{i} ^{(l)} z _{j} ^{(l-1)}\\
z _{j}&\rightarrow \text{ can be derived through forward propagation}\\
\delta _{i} ^{(l)} &\rightarrow \text{ can be derived through back propagation}
\end{align*}
$$

step 1
$$
\delta ^{out} = \frac{\partial L}{\partial a _{out}}
\rightarrow \text{can be obtained easily}
$$

note that
$$
\begin{align*}
\frac{\partial L}{\partial  a _{out}}
&=- \frac{\partial }{\partial a _{out}}
(t ^{(i)}\log(\sigma (a _{out})) + (1-t ^{(i)})\log(1-\sigma (a _{out})))\\
\rightarrow \frac{\partial L}{\partial a _{out}} &=
-t ^{(i)} \frac{\sigma '(a _{out})}{\sigma (a _{out})}-
(1- t ^{(i)})\frac{(- \sigma '(a _{out}))}{1 - \sigma (a _{out})}\\
\text{Recall that } \sigma '(x)&= \sigma (x)(1-\sigma (x))
\end{align*}
$$

then we have

$$
\begin{align*}
\delta ^{out} &= \frac{\partial L}{\partial a _{out}} =
-t ^{(i)}(1 - \sigma (a _{out}))+
(1-t ^{(i)})\sigma (a _{out})\\
&= \sigma (a _{out}) - t ^{(i)}\\
&= y (x ^{(i)}; w) - t ^{(i)}
\end{align*}
$$

$ \rightarrow $ Question ?
Given $ \delta ^{out} $, how can we derive $ \delta _{i} ^{l} $ for $ l<L $?

using the chain rule and the fact that the pre-activation $ a _{i} ^{l-1} $ is 'fed' to all the neurons at layer $ l $, we can write

$$
\begin{align*}
\underbrace{ \frac{\partial L}{\partial a _{i} ^{(l-1)}} }
_{\delta _{i} ^{(l-1)}}
&=\sum_{j=1}^{N _{L}}
\underbrace{ \frac{\partial L}{\partial a _{j}^{(l)}}}
_{\delta _{j} ^{(l)}}
\frac{\partial a _{j} ^{(l)}}{\partial a _{i} ^{(l-1)}}\\
&=
\sum_{j=1}^{N _{L}} \delta _{j} ^{(l)}
\frac{\partial a _{j}^{(l)}}{\partial a _{i}^{(l-1)}}
\end{align*}
$$

therefore, we have

---

$$
\delta _{i} ^{l-1}=
\sum_{j=1}^{N _{L}} \delta _{j} ^{(l)}
\frac{\partial a _{j}^{(l)}}{\partial a _{i}^{(l-1)}}
$$
with
$$
a _{j} ^{(l)} = \sum_{i=1}^{N _{L-1}} w _{ji} ^{(l)}
z _{i} ^{(l-2)} + w _{j0} ^{(l)}
$$

we get

$$
\delta _{i} ^{(l-1)} = \sigma '(a _{i} ^{(l-1)})
\sum_{j=1}^{N _{L}} \delta _{j} ^{(l)}w _{ji}^{(l)}
$$

---

$ \rightarrow $ Derivatives w.r.t intercepts $ w _{i0} ^{(l)} $ can be obtained similarly by augmenting the post activation with a $ 1 $

$ \rightarrow $ Backpropagation algorithm

step $ 1 $
Forward propagate input $ x ^{(i)} $ and derive all pre and post activations $ a _{i} ^{(l)}, z _{i} ^{(l)} $

step $ 2 $
Compute $ \delta ^{out} $

step $ 3 $
Back-propagate the $ \delta ^{out} $ to derive all $ \delta _{i} ^{(l)} $

step $ 4 $
Set the gradient as
$$
\frac{\partial L}{\partial w _{ij} ^{(l)}} = \delta _{i} ^{(l)}z _{j} ^{(l-1)}
$$

step $ 5 $
apply update
$$
w _{ij} ^{(l)} \leftarrow w _{ij} ^{(l)} - \eta \frac{\partial L}{\partial w _{ij}^{(l)}}
$$
