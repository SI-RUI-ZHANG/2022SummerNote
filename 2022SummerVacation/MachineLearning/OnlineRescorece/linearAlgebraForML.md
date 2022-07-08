# Linear Algebra for Machine Learning

[youtube video](https://www.youtube.com/watch?v=LlKAna21fLE&t=57s)

## Data Representation

How can we represent data (images, text, user preference, etc.) in a way that computer can understand?

==idea==

Organize information into vector

A _vector_ is a 1-dimensional array of numbers. It has both a _magnitude_ (length) and a _direction_.

The totality of all vectors with $ n $ entries is an $ n $- dimensional vector space.

"$3$-dimensional space" consists of all vectors with $ 3 $ entries:

$$
\begin{bmatrix}
\quad*\quad\\*\\*
\end{bmatrix}
$$

### In the context of machine learning

==feature vector==

a vector whose entries represent the "features" of some object.

==feature space==

the vector space containing the feature vector, like vector space.

### Common Examples in machine learning

#### images

In black and white images, black and white pixels correspond to $ 0s $ and $ 1s $. Grayscale pixels are numbers between $ 0 $ and $ 255 $. Both assemble into a $ 1 $-dimensional array of numbers.

![picture 2](../../../images/7ac32e91cb3de1eb8b33c29452b6eb79d608ad49a9919366577aedc88b5e9cc1.png)  

#### Words and Documents

Given a collection of documents, assign to every word a vector whose $ i ^{th} $ entry is th number of times the word appears in the $  i ^{th} $ document

$$
dog = \begin{bmatrix}
0\\7\\0\\0\\ \dots
\end{bmatrix}
$$

#### Yes/No or Ratings

Given users and items, vectors can indicate if a user has integrated with the item ($ 1 = yes, 2 = no$)

### Some drawbacks to consider

- These vectors can be very sparse
  - A "sparse" vector is one with lots of zeros
- Possible lack of **meaningful relationship between** vectors
  - one-hot encodings are never "similar"
  - similarity is measured by the **dot product**

### dot product

multiply vectors

$$
\begin{bmatrix}
2 \\ 1
\end{bmatrix}
\cdot
\begin{bmatrix}
1 \\ 5
\end{bmatrix}
= 7
$$

$$
\begin{bmatrix}
1 \\ 0 \\ 3
\end{bmatrix}
\cdot
\begin{bmatrix}
7 \\ 2 \\ -1
\end{bmatrix}
= (1)(7) + (0)(2) + (3)(-1) = 4
$$

The dot product represents the length of the "shadow" of one vector along another.

### better vector representation?

## vector embedding

an embedding of a vector is another vector in a smaller dimensional space

$$
\text{Replace}
\begin{bmatrix}
*\\*\\*
\end{bmatrix}
\text{with}
\begin{bmatrix}
*\\*
\end{bmatrix}
$$

### Talking about matrices

A **matrix** is a $ 2 $-dimensional array of numbers.
It represents a particular process of turning one vector into another: stretching, rotating, scaling, ...

A **matrix** represents a transformation of an entire vector space to another

![picture 3](../../../images/fc511a22fe188c111b9d46a1cc1731f68b4a585e6b11b1f3e637130de303a756.png)  

#### what is a "matrix factorization"

We can multiply **matrices** and get a **matrix**

![picture 4](../../../images/b0ae8452de732cb06690749074ae1be1e1aa66c97a39494a0be2d05ead7a9ba9.png)  

##### factorization

![picture 5](../../../images/1836b138af868e2b05d194fea204b33ca851f33bfcb2501a7e0e2a4dae815d8b.png)  
![picture 7](../../../images/ab85e1045e1187f58809fe92ea96a6b4dc2534cbcc1fbb71f9e8b2645ba83734.png)  

==Every matrix can be factored!==

A fundamental theorem in linear algebra
**Singular Value Decomposition**

![picture 8](../../../images/79cf181e27cff9fe3a49812d8a47a1f1caa93498adaf37f024e3fd379b1f80f2.png)  

## Dimensionality Reduction

via eigenvectors

Recall that a matrix represents a transformation between vector spaces.
There are some transformations for which some vectors never change direction, but are only scaled.
These special vectors are called ==eigenvectors==.
The scaling factor is called and ==eigenvalue==.
