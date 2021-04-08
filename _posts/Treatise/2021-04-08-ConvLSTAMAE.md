---

layout: post

title: "A Deep Learning Model for Smart Manufacturing Using Convolutional LSTM Neural Network Autoencoders"

date: 2021-04-08 19:30:07

categories: [Treatise Review]

description:

image: /img/2DConvLSTMAE_0.png

published: True

canonical_url:

tags: [smart manufacturing, ConvLSTM, Convolution, CNN, LSTM, Autoencoder, Encoder-Decoder, Time-series forecasting]

---

> A Deep Learning Model for Smart Manufacturing Using Convolutional LSTM Neural Network Autoencoders
> Aniekan Essien , Member, IEEE, and Cinzia Giannetti, 2020
>



## A Deep Learning Model for Smart Manufacturing Using Convolutional LSTM Neural Network Autoencoders

### ABSTRACT

- Machine Speed Prediction은 다양한 시스템 조건에 따라 생산 프로세스를 동적으로 조정하고 생산 처리량을 최적화하여 에너지 소비량을 최소화하는데 사용
- 정확한 데이터 기반 기계 속도 예측은 어렵다.
- 산업 제조 공정 데이터의 복잡한 특성을 감안할 때 noise에 강하고 입력 시계열 신호의 시간 및 공간 분포를 캡처 할 수 있는 에측 모델이 전제조건이 되어야 한다.
- End-to-End model for multistep machine speed prediction인 Deep convolutional LSTM encoder-decoder architechture를 제안

### INTRODUCTION

- CNN은 주로 벡터 공간에서 작동하므로 입력 시계열의 고차원 features를 학습하는데는 어려움이 있다. 따라서 CNN은 시계열 예측 문제에서의 적용은 차선책이다.
- Convolutional LSTM(ConvLSTM)은 spatial information을 보존하고 sequential learning에 잘 수행한다.
- 2-DConvLSTMAE를 제안(Deep ConvLSTM stacked autoencoder for univariate, multistep machine speed forecasting)

  1) ConvLSTM encoding layers

  2) Bidirectional stacked LSTM decoding layers

  3) Time-distributed supervised learning[Fully connected(FC)] layers

- Input: 금속 캔 bodymaker 기계의 내부 속도 (분당 스트로크 수로 측정)

### TECHNICAL PRELIMINARIES

#### A. Problem Formulation

- Multistep(sequence to sequence) 시계열 에측의 목표는 이전에 관찰된 입력 sequence를 이용하여 미래 시계열 값의 고정 길이 sequence를 예측하는 것
- Sequential 입력 데이터를 지도 학습 문제로 변환하는 sliding-window method를 사용
- 입력 시계열 sequence의 일부가 Input features로 사용되도록 재구성
- 이전 Time step을 window width/size로 나타낸다.
- 단변량 time series $$x(t)={x_1,x_2,\cdots,x_t}$$를 이용하여 미래의 k값들을 예측

$$\hat{y}=(\hat{y_1},\hat{y_2},\cdots,\hat{y_k})\cong(x_{t+1},x_{t+2},\cdots,x_{t+k})$$

- sliding window size로 나타내면 $$\hat{y}=(\hat{y_1},\hat{y_2},\cdots,\hat{y_k})=f(x_{t-w},x_{t-w+1},x_{t-w+2},\cdots,x_t)$$
- Input은 일정 기간(1분)동안 얻은 기계의 속도
- Input matrix : $$X\in\mathbb{R}^{n\times w}$$, Output matrix : $$Y\in\mathbb{R}^{n\times k}$$, Training samples의 갯수 : $$n=(N-w-k+1)$$

#### B. Structure of the CNN

- CNN은 주로 이미지, 비디오 인식에 사용되는 feed forward neural network

<img src='/img/2DConvLSTMAE_1.png' width='600'>

- Convolution 연산

$$\begin{aligned}
 y_{ij}=\sigma\begin{pmatrix}\sum^F_{r=1}\sum^F_{c=1}w_{rc}x_{(r+1\times S)(c+j\times S)}+b\end{pmatrix} \\
 0\leq 1\leq \frac{H-F}{S}, \;\;\;\; 0 \leq j \leq \frac{W-F}{S} \;\;\;\;
 \end{aligned}$$

- $$H$$ : 높이, $$W$$ : 너비, $$F$$ : 커널의 크기, $$S$$ : stride
- $$x_{(r+1\times S)(c+j\times S)}$$는 좌표 $$(r+1 \times S)(c+j \times S)$$에 있는 입력 데이터 요소
- $$w_{rc}$$ : 가중치, $$b$$ : 편향, $$\sigma$$ : 비선형 활성화 함수
