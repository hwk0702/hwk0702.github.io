---

layout: post

title: "로지스틱 회귀"

date: 2020-06-15 17:02:07

categories: [ML/DL/Machine Learning]

description:

image: /img/LoR.png

published: true

canonical_url:

---

로지스틱 회귀(Logistic Regression)
----------------------------------------------

- 어떤 사건이 발생할지에 대한 직접 예측이 아니라그 사건이 발생할 확률을 예측

---

#### 1. Model with a Binary Response Variable


$$y_i=\beta_0+\beta_1x_i, \: y_i=0 \: or \:1$$

$$P(y_i=1|x_i)=\pi_i\\P(y_i=0|x_i)=1-\pi_i$$

$$E(y_i|X_i)=\sum_{y_i=0\:or\:1}y_iP(y_i|X_i)=1\times+0\times(1-pi_i)=\pi_i$$


##### 1.1 응답 변수가 이진일때의 문제점

(1) Normal error term

$$when \: y_i=1,\: \varepsilon_i=1-\beta_0=\beta_1x_i \\ when \: y_i=0,\: \varepsilon_i=-\beta_0=\beta_1x_i $$

- 결과적으로, $$\varepsilon_i$$가 정상적으로 분포한다고 가정하는 정상 오차 회귀 모델은 적합하지 않다.

(2) Nonconstant variace of error

$$\text{Given} y_i=E(y_i)+\varepsilon_i \:\:\:\:\:\: \begin{matrix}
\varepsilon_i=y_i-E(y_i)\\ 
V(\varepsilon_i)=V(y_i)
\end{matrix}$$

$$V(y_i)=E\{(y_i-E(y_i))^2\}=\sum_{y_i=0\:or\:1}(y_i-E(y_i))^2\cdot P(y_i) \\ =(1-\pi_i)^2\pi_i+(0-\pi_i)^2(1-\pi_i)\\ =\pi_i(1-\pi_i)\\ =E(y_i)(1-E(y_i))\\ =V(\varepsilon_i)$$

- 결과적으로 오차항의 분산은 각 관측치 (상수 분산이 아님)에 따라 달라진다.

(3) Constant on response function

$$E(y_i)=\pi_i \\ 0 \leq E(y_i) \leq 1$$

위의 세가지 문제는 일반 선형 회귀 모형에 사용되는 선형 반응 함수를 선택할 때 심각한 문제이다.

일반적으로 반응 변수가 이항인 경우 반응 함수가 비선형이어야 한다는 경험적 증거가 있다.

---

#### 2. 로지스틱 회귀

- 선형 회귀 개념을 반응 변수가 이진인 상황으로 확장
- 예측 변수 값을 기반으로 클래스를 알 수 없는 새 관측치를 클래스 중 하나로 분류하는데 사용

<img src='/img/LoR1.png' width='400'> 

<img src='/img/LoR2.png' width='400'> 

##### 2.1 S-Curve fitting for Classification

- 많은 실제 상황에서 예측 변수의 확률을 S-Curve 모양으로 변경할 수 있다.

<img src='/img/LoR3.png' width='400'> 

$$p(x)=\frac{exp(\beta x)}{1+exp(\beta x)}=\frac{e^{\beta x}}{1+e^{\beta x}}$$

##### 2.2 로지스틱 회귀 모델

- simple logistic regression

$$\pi(X=x)=P(Y=1|X=x)\\1-P(Y=0|X=x)$$

$$E(y)=\pi(X=x)\\=\frac{exp(\beta_0+\beta_1 x)}{1+exp(\beta_0+\beta_1 x)} \:\:\:\: or \:\:\:\: \frac{1}{1+exp(-(\beta_0+\beta_1 x))}$$

<img src='/img/LoR4.png' width='400'> 

##### 2.3 Odds and Logit Transform 

- 로지스틱 반응 함수를 정의하려면 먼저 Odds를 정의해야한다.

$$\pi(X=x)=\frac{e^{(\beta_0+\beta_1x)}}{1+e^{(\beta_0+\beta_1x)}}=\frac{1}{1+e^{-(\beta_0+\beta_1x)}} \:\:\:\: 0 \leq\pi(X=x)\leq 1$$

- Odds: $$\frac{\pi(X-x)}{1-\pi(X=x)}\:\:\begin{matrix}
\rightarrow \text{Probability of belonging to class 1}\\ 
\rightarrow \text{Probability of belonging to class 0}
\end{matrix} \:\:\:\: 0 < Odds < 1$$

- Odds에 따라 "Logit"을 도출 할 수 있다

$$logit[\pi(X=x)]=log(Odds)=log\frac{\pi(x)}{1-\pi(x)}=\beta_0+\beta_1x\:\:\:\: -\infty<logit[\pi(X=x)]<\infty$$

##### 2.4 Simple logistic regression & Multiple logistic regression

$$logit[\pi(X=x)]=log(Odds)=log\frac{\pi(x)}{1-\pi(x)}=\beta_0+\beta_1x$$

$$logit[\pi(X=x)]=log(Odds)=log\frac{\pi(x)}{1-\pi(x)}=\beta_0+\beta_1x+\beta_2x_2+\cdots+\beta_px_p=\beta^Tx$$


 