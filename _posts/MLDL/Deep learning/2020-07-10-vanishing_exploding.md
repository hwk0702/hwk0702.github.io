---

layout: post

title: "그래디언트 소실/폭주"

date: 2020-07-09 11:27:07

categories: [ML/DL/Deep Learning]

description:

image: /img/van_gradient.png

published: true

canonical_url:

tags: [그래디언트 소실, 그래디언트 폭주, Vanishing Gradient, Exploding Gradient, 글로럿, He, 르쿤, 딥러닝, Deep Learnig, 텐서플로우, Tensorflow, 케라스, Keras]

---

> 이 내용은 핸즈온 머신러닝 2판 책을 보고 정리한 것 입니다.
>
> <img src='http://image.yes24.com/goods/89959711/800x0' width='150'>

## 그래디언트 소실과 폭주 (Vanishing & Exploding Gradient)

- **그래디언트 소실(Vanishing Gradient)**: 알고리즘이 하위층으로 진행될수록 그래디언트가 점점 작아지는 경우
- **그래디언트 폭주(Exploding Gradient)**: 그래디언트가 점점 커져서 여러 층이 비정상적으로 큰 가중치를 갱신되어 알고리즘이 발산하는 경우
- 로지스틱 활성화 함수의 경우 입력이 커지면 0이나 1로 수렴해서 기울기가 0에 가까워짐
- 역전파가 될 때 사실상 신경망으로 전파할 그래디언트가 거의 없고 조금 있는 그래디언트는 최상위층에서부터 역전파가 진행되면서 점차 약해져서 실제로 아래쪽 층에는 아무것도 도달하지 않는다.

<img src='/img/van_gradient1.PNG' width='400'>

---

#### 1. 글로럿과 He 초기화

- 글로럿과 벤지오가 불안정한 그래디언트 문제를 완화하는 방법 제안
- 각 층의 출력에 대한 분산이 입력에 대한 분산과 같아야 한다고 주장
- 역방향에서 층을 통과하기 전과 후의 그래디언트 분산이 동일
- $$fan_{avg}=(fan_{in}+fan_{out})$$ 층의 입력 개수는 팬인 출력 개수는 팬아웃

글로럿 초기화

> 평균이 0이고 분산이 $$\sigma^2=\frac{1}{fan_{avg}}$$인 정규 분포
> 또는 $$r=\sqrt{\frac{3}{fan_{avg}}}$$일 때 -r과 +r사이의 균등 분포

르쿤 초기화

> 평균이 0이고 분산이 $$\sigma^2=\frac{1}{fan_{in}}$$인 정규 분포
> 또는 $$r=\sqrt{\frac{3}{fan_{in}}}$$일 때 -r과 +r사이의 균등 분포

- 글로럿 초기화를 하면 훈련 속도가 증가

|초기화 전략|활성화 함수|$$\sigma^2$$(정규분포)|
|---|---|---|
|글로럿|활성화 함수 없음, tanh, logstic, softmax| $$1/fan_{avg}$$|
|He|ReLU 함수와 그 변종들|$$2/fan_{in}$$|
|르쿤|SELU|$$1/fan_{in}$$|

- 케라스는 기본적으로 균등 분포의 글로럿 초기화를 사용