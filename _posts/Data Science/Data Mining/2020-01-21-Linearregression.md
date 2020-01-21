---

layout: post

title: "Linear Regression"

date: 2020-01-21 10:57:07

categories: [Data Science/Data Mining]

description:

image: /img/linearregression.png

published: true

canonical_url:

---

## Statistical Learning

<img src="/img/statistical.PNG" >

------------------------------

## Linear Regression

<img src="/img/linearregression1.png" width='500'>

$$ Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + \cdots + \beta_pX_p$$

- Y variable (response, dependent, or output)
- X variables (predictor, independent, input, explanatory, cavariates, feature, or regressors)

### Two objectives of regression analysis

1. Explanatory modeling(설명적 모델링): 반응변수(Y)와 예측변수 집합(X)의 관계를 이해하기 위해
2. Predictive modeling(예측 모델링): 새로운 사례의 반응변수 결과를 예측하기 위해

### Types of Regression models

<img src="/img/linearregression2.png" width='500'>

### Linear Regression model

$$ \varepsilon = \text{Random error}$$

$$ \varepsilon: \varepsilon \sim N(0,\sigma^2) \rightarrow E(\varepsilon)=0, Var(\varepsilon)=\sigma^2$$

$$ E(Y|X)=\beta_0+\beta_1X $$

### Purpose of Linear Regression model

$$Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + \cdots + \beta_pX_p+\varepsilon, \varepsilon \sim N(0,\sigma^2)$$

$$ E(Y)= \beta_0 + \beta_1X_1 + \beta_2X_2 + \cdots + \beta_pX_p $$

- 목적: X와 E(X) 사이의 선형 관계를 찾기 위해

### Difference between Expectation and Fitted Value of Regression models

$$ E(Y|X)=\beta_0+\beta_1X \;\;\;\;\;\;\;\;\;\;\; \varepsilon = Y-E(Y|X)$$

$$\text{VS} \;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\; \text{VS}$$

$$ \hat{Y}=\hat{\beta_0}+\hat{\beta_1}X \;\;\;\;\;\;\;\;\;\;\;\;\; e=Y-\hat{Y}$$
