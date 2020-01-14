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

### 3. For numeric attributes

1) Euclidean Distance

$$ d(i,j) = \sqrt{\sum^p_{k=1}(x_{ik}-x_{jk})^2} $$

2) Manhattan Distance

$$ d_{manhattan}(i,j) = \sum^p_{k=1}\left | x_{ik}-x_{jk} \right | $$

- Euclidean, Manhattan Distance가 만족해야하는 조건
  * 음이 아닌 수
  * Identify of indiscernibles
  * 대칭
  * Triangle inequality

3) Minkowski Distance

$$ d(i,j) = (\sum^p_{k=1} \left | x_{ik}-x_{jk} \right |^r)^{1/r} $$

- r=1 : Manhattan (L1 norm)
- r=2 : Euclidean (L2 norm)
- r= $$\infty$$ : Supremum (Lmax norm, L$$\infty$$ norm)

<br> <img src="/img/num_dist.PNG" width="250">

4) Mahalanobis Distance

- 데이터 분포를 고려하기 위해 사용

$$ Mahalanobis(X,Y) = (X-Y)^T{\sum}^{-1}(X-Y) $$

<br> <img src="/img/maha_dist.PNG" width="500">

<br> <img src="/img/maha_dist2.PNG" width="500">


### 4. For ordinal attributes

- ordinal attributes는 순서 or 순위가 있지만 크기는 알 수 없다.
  * 1) 등급에 따라 점수를 준다.
  * 2) normalizes
  * 3) Euclidean Distance 이용
<br> <img src="/img/ord_dist.PNG" width="300"> <img src="/img/ord_dist2.PNG" width="150">

### 5. For mixed attributes

1) 각 속성 유형을 그룹화하고 각 유형에 대해 개별적으로 군집화와 같은 데이터 마이닝 수행하는 방법
2) 다른 방법으로 모든 속성 유형을 함께 처리하여 한개의 분석을 실행하는 방법
  -> 여러 속성을 단 한개의 차이 행렬로 연결하고 모든 의미 있는 속성을 공통된 범위 척도 [0.0, 1.0]으로 만드는 방법
