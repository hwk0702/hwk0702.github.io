---

layout: post

title: "학습률 스케줄링"

date: 2020-08-28 15:37:07

categories: [ML/DL/Deep Learning]

description:

image: /img/learning_rate_scheduling.png

published: true

canonical_url:

tags: [학습률 스케줄링, learning rate scheduling, 학습률, learning rate, 딥러닝, Deep Learning, 텐서플로우, Tensorflow, 케라스, Keras]

---

> 이 내용은 핸즈온 머신러닝 2판 책을 보고 정리한 것 입니다.
>
> <img src='http://image.yes24.com/goods/89959711/800x0' width='150'>

## 학습률 스케줄링

- 학습률을 너무 크게 잡으면 발산할 수 있으며, 너무 작게 잡으면 최적점에 수렴하는데 오랜 시간이 걸린다.

<img src='/img/learning_rate_scheduling_1.png' width='600'>

- 큰 학습률로 시작하고 학습 속도가 느려질 때 학습률을 낮추면 최적의 고정 학습률 보다 좋은 솔루션을 더 빨리 발견할 수 있다.
- 이를 학습 스케줄이라고 한다

---

#### 1. 널리 사용하는 학습 스케줄링 기법

- 거듭제곱 기반 스케줄링(power scheduling)

학습률을 반복 횟수 $$t$$에 대한 함수 $$\eta(t)=\eta_0 / (1+t/s)^c$$로 지정. ($$\eta_0$$: 초기 학습률, $$c$$: 거듭제곱 수, $$s$$: 스텝 횟수)

처음에는 빠르게 감소하다가 점점 더 느리게 감소

- 지수 기반 스케줄링(exponential scheduling)

$$\eta(t)=\eta_00.1^{t/s}$$로 설정. 학습률이 $$s$$스텝마다 10배씩 점차 감소

- 구간별 고정 스케줄링(piecewise constant scheduling)

일정 횟수의 에포크 동안 일정한 학습률을 사용하고 그 다음 또 다른 횟수의 에포크 동안 작은 학습률을 사용하는 방법

- 성능 기반 스케줄링(performance scheduling)

매 $$N$$ 스텝마다 검증 오차를 측정하고 오차가 줄어들지 않으면 $$\lambda$$배 만큼 학습률을 감소

- 1 사이클 스케줄링(1 cycle scheduling)

1 사이클은 훈련 절반 동안 초기 학습률 $$\eta_0$$을 선형적으로 $$\eta_1$$까지 증가. 나머지 절반동안 선형적으로 학습률을 $$\eta_0$$까지 감소. 마지막 몇 번의 에포크는 학습률을 소수점 몇 째 자리까지 줄인다. 최대 학습률 $$\eta_1$$은 최적의 학습률을 찾을 때와 같은 방식을 사용해 선택하고 초기 학습률 $$\eta_0$$은 대략 10배 정도 낮은 값을 선택
