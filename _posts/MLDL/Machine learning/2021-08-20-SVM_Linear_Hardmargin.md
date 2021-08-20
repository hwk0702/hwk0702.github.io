---

layout: post

title: "SVM(Linear&HardMargin)"

date: 2021-08-20 19:30:07

categories: [ML/DL/Machine Learning]

description:

image: /img/SVM_LH1.png

published: True

canonical_url:

tags: [Machine Learning, Kernel-based Learning, SVM, Support Vector Machine, Linear, Hard Margin, 서포트벡터머신]

---

> 이 내용은 고려대학교 강필성 교수님의 Business Analytics 수업을 보고 정리한 것입니다.
>
> 아래 이미지 클릭 시 강의 영상 Youtube URL로 넘어갑니다.
>
>[![02-2: Kernel-based Learning - SVM (Linear Case with Hard Margin)](https://img.youtube.com/vi/eZtrD6pYaaE/mqdefault.jpg)](https://www.youtube.com/watch?v=eZtrD6pYaaE&list=PLetSlH8YjIfWMdw9AuLR5ybkVvGcoG2EW&index=9)

# Support Vector Machine - Linear & Hard Margin

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled.png' width='600'>

- Original SVM은 기본적으로 Linear Model

## 1. Linear Classification (Binary)

### ✓ Training data : i.i.d(independent and identically distribution)로 부터 $X\in R^d$

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 1.png' width='500'>

- 보통은 label을 1과 0으로 표현하지만 SVM에서는 formulation을 단순화하기 위해 +1, -1로 표현

### ✓ Problem : $h:X \rightarrow {-1,+1}$를 잘 분류하면서 generalization error $R_D(h)$를 가장 최소화하는 Classifier H를 찾는 것

### ✓ Purpose : d-dimension에서 두 범주를 잘 구분하는 (d-1)차원의 hyperplane을 찾자!

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 2.png' width='600'>

### ✓ 어떤 분류 결과물이 더 좋은 결과물인가?

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 3.png' width='600'>

- **margin** : 분류 경계면으로 부터 가장 가까운 양쪽 범주 객체와의 거리
- A 모델을 더 선호하게 설계되어 있다. (margin이 클수록 capacity가 작다)
- Neural network는 empirical error만 보기 때문에 많은 local optimum이 나온다. (but, 고차원에서 모든 방향으로 gradient가 0인 경우는 거의 없다. 문제 없다.)

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 4.png' width='600'>

## 2.  Formulation

### ✓ margin 계산 방법

- plane 자체를 margin이라 하는 경우도 있고, plane간의 공간을 margin이라 하는 경우도 있음

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 5.png' width='600'>

- $x_0$가 분류 경계면에 있고 $x_1$이 plus plane 위에 있다고 하였을 때 $w^Tx_0+b=0$이고 $x_1=x_0+pw$라고 할 수 있다.

$$\begin{matrix}
w^T(x_o+pw)+b=1 \;\;\;\;\rightarrow\;\;\;\; w^Tx_0+pw^Tw+b=1\\
pw^Tw=1\;\;\;\;(\because w^Tx_0+b=0)\\
p=\frac{1}{-w^Tw}=-\frac{1}{\left \| w \right \|^2}\\
|p|=\frac{1}{\left \| w \right \|^2}
\end{matrix}$$

### ✓ margin이 capacity term과 연관있는 이유

- VC dimension은 margin에 의해서 bound된다.

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 6.png' width='300'>

- margin을 최대화하면 VC dimension이 줄어들고, 이는 Expected Risk를 줄여준다.

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 7.png' width='400'>

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 4.png' width='600'>

- 높은 margin을 갖는 hyperplane을 선택하는 경우, 데이터를 분류하는데 적은 수의 경우가 존재 → lower VC dimension

## 3. Cases

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 8.png' width='450'>

## 4. Linear Case & Hard Margin

### ✓ Objective function

$$\begin{matrix}\text{min}\;\;\frac{1}{2}\left \| w \right \|^2\\
s.t.\;\;y_i(\textbf{w}^T\textbf{x}_i+b)\geq 1, \;\forall_i\end{matrix}$$

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 9.png' width='600'>

### ✓ Dual 문제 예시 (참고)

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 10.png' width='600'>

### ✓ Optimization Problem

- Lagrangian Problem

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 11.png' width='600'>

- KKT(Karush-Kuhn-Tucker) conditions

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 12.png' width='500'>

- From Primal to Dual

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 13.png' width='600'>

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 14.png' width='600'>

- Solution

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 15.png' width='400'>

- From KKT condition

  - 제약식과 그 제약식에 대응하는 lagrangian multiplier을 곱하면 항상 0
  - 또한, 둘 다 0이면 최적해가 아니다!

  $$\alpha_i(y_i(\text{w}^T\text{x}_i+b)-1)=0$$

  - 여기서 $\alpha_i \neq 0$이면 $y_i(\text{w}^T\text{x}_i+b)-1=0$이 성립하고 그 경우 margin 위에 있는 data이다.
  - $\alpha_i \neq 0$인 경우를 support vector라고 한다.

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 16.png' width='300'>

<img src='/img/Supprot Vector Machine(SVM) - Linear & Hard Margin 9044f1ec45664cbe8c63b8592e4b9aaa/Untitled 17.png' width='300'>

- b도 미지수이지만 support vector들을 통해 구할 수 있으며, 모든 support vector에 대해 b값이 동일하여야하지만 계산시 다를 수 있다. 따라서 support vector에 대해 b 값을 계산한 후 평균을 낸다.

### ✓ Compute the margin

- 모든 support vector를 이용하여 b를 계산

$$b=y_i-\sum_{i=1}^N\alpha_iy_i(\text{x}_j,\text{x}_i)\;\;\;\;(\because\;\text{w}=\sum^N_{i=1}\alpha_iy_i\text{x}_i)$$

- 양변에 $\alpha_iy_i$를 곱해준다

$$\begin{matrix} \sum^N_{i=1}\alpha_iy_ib=\sum^N_{i=1}\alpha_iy_i^2-\sum^N_{i,j=1}\alpha_i\alpha_jy_iy_j(\text{x}_i,\text{x}_j) \\ b\sum^N_{i=1}\alpha_iy_i=\sum^N_{i=1}\alpha_i-\text{w}^T\text{w}\;\;(\because\;b\text{ is constant, }y_i^2=1,\;\sum^N_{i,j=1}\alpha_i\alpha_jy_iy_j(\text{x}_i,\text{x}_j)=\text{w}^T\text{w})\\0=\sum^N_{i=1}\alpha_i-\text{w}^T\text{w}\;\;(\because\;\sum^N_{i=1}\alpha_iy_i=0)\end{matrix}$$

- 따라서 margin은

$$\rho^2=\frac{1}{\left \| \text{w} \right \|^2_2}=\frac{1}{\sum^N_{i=1}\alpha_i}=\frac{1}{\left \| \alpha \right \|_1}$$
