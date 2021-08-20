---

layout: post

title: "SVM(SoftMargin)"

date: 2021-08-20 20:30:07

categories: [ML/DL/Machine Learning]

description:

image: /img/SVM_SM1.png

published: True

canonical_url:

tags: [Machine Learning, Kernel-based Learning, SVM, Support Vector Machine, Soft Margin, 서포트벡터머신]

---

> 이 내용은 고려대학교 강필성 교수님의 Business Analytics 수업을 보고 정리한 것입니다.
>
> 아래 이미지 클릭 시 강의 영상 Youtube URL로 넘어갑니다.
>
>[![02-2: Kernel-based Learning - SVM (Linear Case with Hard Margin)](https://img.youtube.com/vi/RKMiTJAnLy8/mqdefault.jpg)](https://www.youtube.com/watch?v=RKMiTJAnLy8&list=PLetSlH8YjIfWMdw9AuLR5ybkVvGcoG2EW&index=10)

# 1. Support Vector Machine(SVM) - Soft Margin

- Hard margin은 넘어가는 예외X
- Hard margin으로 margin이 생기지 않는 경우도 있으며, 실제는 noise도 있어 항상 Hard margin으로 풀 수 있는 문제는 거의 없다.
- Soft margin은 margin을 넘어가는 예외를 두지만 penalty를 준다.

## 1.1 Optimization Problem (C-SVM)

### ✓ Objective function

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled.png' width='400'>

- $C$는 margin을 최대화하는 term과 margin을 넘어가는 penalty를 얼마만큼 허용해줄 것인지의 trade-off를 control하는 hyper-parameter

### ✓ Constraints

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 1.png' width='400'>

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 2.png' width='600'>

### ✓ Lagrangian Problem

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 3.png' width='600'>

### ✓ KKT conditions

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 4.png' width='500'>

## 1.2. From Primal to Dual

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 5.png' width='600'>

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 6.png' width='600'>

## 1.3. Solution

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 7.png' width='300'>

## 1.4. Case

KKT condition에 따르면,

$$\alpha_i(y_i(\textbf{w}^T\textbf{x}_i+b)-1+\xi_i)=0$$

support vector는 $\alpha_i\neq0$일 수 없다.

거기다가, $C-\alpha_i-\mu_i=0 \;\;\&\;\; \mu_i\xi_i=0$ 이기 때문에 다음과 같이 case를 나눌 수 있다.

- Case 1: $\alpha_i=0$ → non-support vectors

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 8.png' width='400'>

- Case 2: $0<\alpha_i<C$ → support vectors on the margin

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 9.png' width='400'>

- Case 3: $\alpha_i=C$ → support vectors outside the margin

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 10.png' width='400'>

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 11.png' width='400'>

## 1.5. Regularization cost C

- Large C: margin의 폭을 좁게 갖는다.  $C\uparrow \;\;\xi\downarrow\;\;\rightarrow \text{margin}\downarrow$
- Small C: margin의 폭을 넓게 갖는다.  $C\downarrow \;\;\xi\uparrow\;\;\rightarrow \text{margin}\uparrow$

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 12.png' width='600'>

---

# 2. SVM Case 3: Non-linear Case & Soft Margin

- Decision boundary가 선형이 아닌 경우
- mapping function $\Phi(\textbf{x})$를 사용하여 저차원에서의 input vector를 고차원에서의 feature vector로 변환

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 13.png' width='600'>

- Goal
  - Large margin : 일반화된 성능(구조적 위험 최소화)
  - Flexible : 임의의 모양을 갖는 boundary를 생성할 수 있는 SVM을 만들자(유연한 분류 경계면)

## 2.1 Optimization Problem (C-SVM)

- mapping function $\Phi(\textbf{x})$ : $\textbf{x}\in R^d \rightarrow \Phi(\textbf{x})\in R^D \; (d<D)$

### ✓ Objective function

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 14.png' width='200'>

### ✓ Constraints

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 15.png' width='400'>

### ✓ Lagrangian Problem (Primal)

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 16.png' width='500'>

### ✓ KKT conditions

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 17.png' width='500'>

### ✓ Lagrangian Problem (Dual)

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 18.png' width='400'>

$\Phi(\textbf{x}_i)^T\Phi(\textbf{x}_j)$으로 부터 kernel trick 등장

## 2.2. Kernel Trick

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 19.png' width='400'>

mapping function $\Phi$으로 부터 나온 feature space의 내적 말고 다른 함수를 씌워서 feature space의 내적과 같다는 보장을 할 수 있다면, 굳이 힘들게 $\Phi$를 찾지말고 $K$라는 함수를 이용하자.

### ✓ Generalized inner product

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 20.png' width='600'>

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 21.png' width='600'>

고차원 공간에서의 내적이 갖는 특징을 잘 보존할 수 있는 함수를 갖다 쓰자

### ✓ Polynomial Kernel

위에꺼 확장, $Q$를 늘리면 늘릴수록 더 고차원에 mapping 가능

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 22.png' width='600'>

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 23.png' width='300'>

### ✓ Gaussian (RBF) Kernel

polynomial을 무한히 확장

유한 차원의 vector를 이론적으로 무한 차원의 vector로 mapping시킨 상태에서의 내적을 계산할 수 있다.

선형 분류기가 무한대의 점들을 shatter할 수 있고, VC dimension이 커진다고 생각할 수 있으나 margin이 VC dimension을 줄여준다.

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 24.png' width='600'>

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 25.png' width='400'>

### ✓ Sigmoid Kernel

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 26.png' width='300'>

### 2.2.1 Idea

- Define $K:\textbf{X}\times\textbf{X}\rightarrow R$, called Kernel

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 27.png' width='300'>

- Benefits
  - Efficiency : 굳이 mapping function을 찾지 않아도 계산 연산의 효율성 확보
  - Flexibility : Mercer's condition을 만족하는 어떤 family의 함수들도 K로 사용 가능하므로 유연하다.

### 2.2.2 Kenel function이 가져야하는 조건

$\text{L}_2$-space(적분 가능한)에서 symmetric function이 밑에 두가지 조건을 만족하면 kernel function으로 사용가능하다.

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 28.png' width='600'>

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 29.png' width='600'>

### 2.2.3 C의 특징

Linear의 경우 $C$가 커지면 margin이 작아졌는데, Kernel의 경우 $C$가 커지면 margin을 벗어나는 것을 허용하지 않기 위해서 margin 폭이 굉장히 좁아지고 꼬불꼬불해진다.

### 2.2.4 Kernel width (sigma) for RBF Kernel

Kernel width가 작으면 작을수록 분류 경계면이 꼬불꼬불해지고, 클수록 선형에 가까워진다.

<img src='/img/Support Vector Machine(SVM) - Soft Margin 70bc4bc4afb64bc9987bdf844bb79113/Untitled 30.png' width='600'>
