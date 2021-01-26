---

title: Traffic Accident Detection

subtitle: Connected Vehicles (CV) Traffic Accident Detection

date: 2021-01-18 14:50:07

categories: [Projects]

description: This is a project description

product_code:

published: true

layout: product

image: /img/cv_novelty.png

price:

show_sidebar: false

features:
  - label: KETI
    icon: fa-location-arrow
  - label: 2020.08 ~ 2020.12
    icon: fa-calendar-alt
  - label: 교통사고 탐지
    icon: fa-file-alt
  - label: Python, keras, pytorch, Yolov4, DeepSort, FlowNet2.0, ORBSLAM2
    icon: fa-code

rating: 5

---

# Traffic Accident Detection

본 프로젝트는 전자기술연구원(KETI)에서 진행되는 프로젝트로 데이터 및 코드는 대외비 입니다.

데이터, 코드를 제외한 프로젝트 과제 내용만 공유합니다.

---

### 1. 소개

#### 1.1	정의

-	블랙박스 영상을 활용한 교통사고 탐지
-	1인칭 시점의 블랙박스 영상을 활용한, 비지도 학습 기반의 교통 상황 이상 탐지 모델
-	영상 프레임 내의 객체들에 대한 미래 위치를 예측해서 이상 탐지 진행. 이 때 모델이 학습하기 위한 정답, Label은 바로 다음 순간의 위치이기 때문에 별도로 Labeling 할 필요가 없다.
-	미래 위치 예측은 1) 모델이 예측한 미래 위치가 실제 위치와 비교했을 때 얼마나 정확한지(Accuracy), 그리고 2) 객체가 보이는 비정상적인 움직임이 일관적으로 관측되는지(Consistency) 등을 평가하며 학습이 진행되고, 잘 학습된 모델은 예측한 위치와 실제 위치의 차이가 큰 경우를 이상 상황으로 탐지
-	인코더-디코더를 포함하는 LSTM 모델로 예측
-	모델에 Input으로 들어가는 Feature를 생성하기 위해서는 4가지 기법이 사용됨
    - 객체 탐지 :  Yolov4 (논문에서는 Mask-RCNN을 사용)
    -	트래킹 :  DeepSort
    -	광학 흐름 : FlowNet2.0
    -	자아 궤적 탐지 : ORBSLAM2

<img src='/img/tad01.png' width='500'> <img src='/img/tad02.png' width='300'>

---

### 2. 단계별 영상

#### 2.1 원본 영상

<iframe width="600" height="308" src="https://www.youtube.com/embed/8iTKbFVVtZc" frameborder="0" allow="accelerometer; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#### 2.2 객체 탐지 + 트래킹

- Yolov4를 이용하여 객체를 탐지하고 DeepSort를 이용하여 객체 트래킹

<iframe width="600" height="308" src="https://www.youtube.com/embed/uiXte5HMu6E" frameborder="0" allow="accelerometer; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#### 2.3 광학 흐름

- FlowNet2를 이용하여 프레임상의 광학 흐름을 탐지하여 프레임 이미지의 변화를 탐지

<iframe width="600" height="308" src="https://www.youtube.com/embed/iNlqb-fFtVA" frameborder="0" allow="accelerometer; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#### 2.4 자아 궤적 탐지

- ORBSLAM2를 이용하여 자아의 궤적을 탐지, 어떻게 움직이고 있는지를 판단한다.

<iframe width="600" height="308" src="https://www.youtube.com/embed/Tm84vvClZOI" frameborder="0" allow="accelerometer; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### 3. 결과

<iframe width="600" height="308" src="https://www.youtube.com/embed/RxrHdY9yyZU" frameborder="0" allow="accelerometer; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#### 3.1 추가 영상

<iframe width="600" height="308" src="https://www.youtube.com/embed/n8cDpEmVHLg" frameborder="0" allow="accelerometer; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
