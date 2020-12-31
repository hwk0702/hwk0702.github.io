---

layout: post

title: "Supervised Variable Selection"

date: 2020-12-27 21:30:07

categories: [ML/DL/Machine Learning]

description:

image: /img/supervised_variable_selection.png

published: True

canonical_url:

tags: [Machine Learning, Dimensionality Reduction, Supervised Variable Selection, Exhaustive Search, Forward Selection, Backward Elimination, Stepwise Selection, 머신러닝, 차원축소]

---

> 이 내용은 고려대학교 강필성 교수님의 Business Analytics 수업을 보고 정리한 것입니다.
>
> 아래 이미지 클릭 시 강의 영상 Youtube URL로 넘어갑니다.
>
>[![01-2: Dimensionality Reduction - Supervised Selection](https://i.ytimg.com/vi/A69fxxdU0mk/hqdefault.jpg?sqp=-oaymwEYCKgBEF5IVfKriqkDCwgBFQAAiEIYAXAB&amp;rs=AOn4CLBjfOaA-n3YZRo5U644s5rLxvnlyw)](https://youtu.be/A69fxxdU0mk)

Supervised Variable Selection
----------------------------------------------

---

## Exhaustive Search

- 가능한 모든 조합을 확인하는 방법

<img src='/img/exhaustive_search01.PNG' width='600'>

- 변수 선택을위한 성능 기준:
    - Akaike Information Criteria(AIC)
    - Bayesian Information Criteria(BIC)
    - Adjusted $$R^2$$
    - Mallow's $$C_p$$
    - etc

- Global Optimum을 확보할 수 있으나 현실적으로 사용 불가하다.

<img src='/img/exhaustive_search02.PNG' width='600'>

## Forward Selection

- 변수가 없는 모델에서 중요한 변수를 순차적으로 추가하는 방법

- 변수를 선택하면 제거되지 않는다. (변수 수 점차 증가)

<img src='/img/forward_selection01.PNG' width='600'>

## Backward Elimination

- 모든 변수가 있는 모델에서 관련 없는 변수를 순차적으로 제거

- 변수가 제거되면 다시 선택되지 않는다. (변수 수 점차 감소)

<img src='/img/backward_elimination01.PNG' width='600'>

## Stepwise Selection

- 변수가 없는 모델에서 순방향 선택과 역방향 제거를 번갈아 수행

- Forward Selection/Backward Elimination보다 시간이 오래 걸리지만 최적의 변수 집합을 찾을 수 있는 기회가 더 많다.

- Forward Selection/Backward Elimination과는 다르게 선택/제거 된 변수는 선택/제거를 위해 다시 고려할 수 있다.

<img src='/img/stepwise_selection01.png' width='600'>
