---

layout: post

title: "데이터 유사도"

date: 2020-01-14 10:57:07

categories: [Data Science/Data Mining]

description:

image: /img/simil.png

published: true

canonical_url:

---

## Data similarity(데이터 유사도)

데이터 유사도란 두 데이터가 얼마나 같은지 나타내주는 척도이다.

### Basic data structure
1. data matrix (n object X p attributes)

$$\begin{bmatrix}
x_{11} & \cdots & x_{1f} & \cdots & x_{1p}\\
\cdots & \cdots & \cdots & \cdots & \cdots\\
x_{i1} & \cdots & x_{if} & \cdots & x_{ip}\\
\cdots & \cdots & \cdots & \cdots & \cdots\\
x_{n1} & \cdots & x_{nf} & \cdots & x_{np}
\end{bmatrix}$$

2. similarity matrix (n objects X n objects)

$$\begin{bmatrix}
0 &  &  &  & \\
sim(2,1) & 0 &  &  & \\
sim(3,1) & sim(3,2) & 0 &  & \\
\vdots & \vdots & \vdots &  & \\
sim(n,1) & sim(n,2) & \cdots & \cdots & 0
\end{bmatrix}$$

3. disimilarity matrix (n objects X n objects)

- sim(i,j) = 1 - d(i,j)

$$\begin{bmatrix}
0 &  &  &  & \\
d(2,1) & 0 &  &  & \\
d(3,1) & d(3,2) & 0 &  & \\
\vdots & \vdots & \vdots &  & \\
d(n,1) & d(n,2) & \cdots & \cdots & 0
\end{bmatrix}$$

----------------------------------------------

## Similarity and Distance Measures

### 1. For nominal attributes
- $$d(i,j) = { {p-m} \over p }$$
- m = number of matches
- p = total number of attributes descibing the objects

ex)

<br> <img src="/img/nom_simil.PNG" width="400">

### 2. For binary attributes

- For symmetric binary attributes (0과 1 모두 중요)

$$d(i,j) = { {r+s} \over {q+r+s+t}}$$

- For asymmetric binary attributes (1이 더 중요)

$$d(i,j) = { {r+s} \over {q+r+s}}$$ (Jaccard Coefficent라고도 불림)

<br> <img src="/img/bi_simil.PNG" width="300">

(ex)
<br> <img src="/img/bi_simil2.PNG" width="500">

### 3. For ordinal attributes

-
