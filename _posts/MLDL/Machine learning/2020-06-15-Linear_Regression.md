---

layout: post

title: "선형회귀"

date: 2020-06-15 16:02:07

categories: [ML/DL/Machine Learning]

description:

image: /img/LR.png

published: true

canonical_url:

---

회귀분석(Regression)
----------------------------------------------

- 종속 변수에 영향을 미치는 다수의 독립 변수들과의 관계를 알아보고자 할 때 사용
- 모델의 유의성은 p-value로 판단하는데 p-value 값이 유의수준보다 작을 경우 유의하다고 판단
- 각 독립 변수의 유의성도 마찬가지로 p-value가 유의수준보다 작을 경우 종속 변수 예측에 유의한 영향을 미친다고 판단
- 모델을 얼마나 잘 설명하는지, 즉 모델이 전체 변동을 얼마나 섦명할 수 있는지에 대해서는 결정계수 R-squred를 기준으로 판단(1에 가까울수록 설명력이 높다)
- 다중공산성: 독립 변수들 사이에 강한 상관성이 존재하여 회귀계수 값이 불안정하게 되는 현상
- 분산팽창계수(VIF): 다중공산성을 판단하는 척도, 5이상이면 높고 5이하이면 낮다고 판단

---

#### 1. 선형 회귀

- 일반적으로 선형 모델은 입력 특성의 가중치 합과 편향(bias 또는 절편)이라sms 상수를 더해 예측을 만든다.

$$Y=\beta_0+\beta_1\mathbf{X}_1+\beta_2\mathbf{X}_2+\cdots+\beta_p\mathbf{X}_p$$

<img src='/img/LR2.png' width='400'>

##### 1.1 Two objectives of regression analysis

1) 설명적 모델링: 반응변수(Y)와 예측변수 집합(X)의 관계를 이해하기 위해

2) 예측 모델링: 새로운 사례의 반응 변수 결과를 예측하기 위해

##### 1.2 선형 회귀 모델

<img src='/img/LR1.png' width='400'>

$$\varepsilon$$=Random error

랜덤 오차에 대한 가정: $$\varepsilon~N(0,\sigma^2) \rightarrow E(\varepsilon)=0, Var(\varepsilon)=\sigma^2$$ 

##### 1.3 선형 회귀의 목적

- $$X$$와 $$E(X)$$ 사이의 선형 관계를 찾기 위해서

$$Y=\beta_0+\beta_1\mathbf{X}_1+\beta_2\mathbf{X}_2+\cdots+\beta_p\mathbf{X}_p+\varepsilon$$

$$E(Y)=\beta_0+\beta_1\mathbf{X}_1+\beta_2\mathbf{X}_2+\cdots+\beta_p\mathbf{X}_p$$

##### 1.4 회귀 모형의 기대치와 적합치의 차이

<img src='/img/LR3.png' width='400'>

- 랜덤 오차($$\varepsilon$$)는 관심 수량의 실제 값과 관측 값의 편차
- 잔차($$e$$)는 관심 수량의 관측값과 추정 값의 차이

#### 2. 단순 회귀 모형의 최소 추정량

$$\varepsilon_i=y_i-E(y_i)=y_i-(\beta_0+\beta_1x_i)=y_i-\beta_0-\beta_1x_i$$

$$Q(\beta_0\beta_1)=\sum^n_{i=1}\varepsilon_i^2=\sum^n_{i=1}(y_i-\beta_0-\beta_1x_i)^2$$

$$MinimizeQ(\beta_0\beta_1)=\sum^n_{i=1}\varepsilon_i^2=\sum^n_{i=1}(y_i-\beta_0-\beta_1x_i)^2$$

> $$\frac{\delta Q(\beta_0,\beta_1)}{\delta \beta_0}=-2\sum^n_{i=1}(y_i-\beta_0-\beta_1x_i)=0$$
> $$\sum y_i-n\beta_0=\beta_1\sum x_i=0$$
> $$\hat{\beta_0}=\frac{\sum y_i-\hat{\beta_1}\sum x_i}{n}=\bar{y}-\hat{\beta_1}\bar{x}$$


> $$\frac{\delta Q(\beta_0,\beta_1)}{\delta \beta_1}=-2\sum^n_{i=1}(y_i-\beta_0-\beta_1x_i)x_i=0$$
> $$\sum x_iy_i-\beta_0\sum x_i-\beta_1\sum(x_i)^2=0$$
> $$\sum x_iy_i-(\bar{y}-\hat{\beta_1}\bar{x})\sum x_i-\beta_1\sum(x_i)^2=0$$
> $$\sum x_iy_i-\bar{y}\sum x_i-\hat{\beta_1}\bar{x}\sum x_i-\beta_1\sum(x_i)^2=0$$
> $$\sum x_iy_i-\bar{y}\sum x_i-\hat{\beta_1}(n\bar{x}^2-\sum(x_i)^2)=0$$
> $$\hat{\beta_1}=\frac{n\bar{x}\bar{y}-\sum x_iy_i}{n\bar{x}^2-\sum{(x_i)^2}}=\frac{\sum{(x_i-\bar{x})(y_i-\bar{y})}}{\sum{(x_i-\bar{x})^2}}$$

$$\hat{\beta_0}=\bar{y}-\hat{\beta_1}\bar{x}$$

$$\hat{\beta_1}=\frac{\sum{(x_i-\bar{x})(y_i-\bar{y})}}{\sum{(x_i-\bar{x})^2}}$$

##### 다중선형회귀에서의 최소 추정량

<img src='/img/LR4.png' width='400'>

