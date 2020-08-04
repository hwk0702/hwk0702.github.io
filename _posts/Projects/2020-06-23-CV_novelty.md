---

title: CV Novelty Detection

subtitle: Connected Vehicles (CV) Novelty Detection

date: 2020-06-22 14:50:07

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
  - label: 2020.06 ~
    icon: fa-calendar-alt
  - label: 커넥티드 차량 이상치 탐지 및 제거
    icon: fa-file-alt
  - label: Python, sklearn
    icon: fa-code

rating: 3

---

# CV Novelty Detection

본 프로젝트는 전자기술연구원(KETI)에서 진행되는 프로젝트로 데이터 및 코드는 대외비 입니다. 

데이터, 코드를 제외한 프로젝트 과제 내용만 공유합니다.

### 0. CV 과제 소개

#### 0.1 CV 과제

<img src='/img/coolant5.png' width='600'>

<img src='/img/coolant2.png' width='600'>

#### 0.2 데이터 설명

-	데이터의 구조 이해

①	실시간으로 elex, triphos 등의 회사로 부터 레미콘 차량의 데이터를 받아 DB에 저장하고 있다.

②	레미콘 차량의 주행 속도, 냉각수 온도, GPS 위치, DTC, RPM 등 센서 데이터 수집

---

### 1. 소개

#### 1.1	문제 정의

<img src='/img/cv_novelty1.png' width='500'>

-	주행 속도: 1초간 속도가 비이상적으로 증감하는 이상치가 존재
- 냉각수 온도: 냉각수 온도가 비이상적으로 낮거나 높은 수치 데이터가 존재
- 배터리 전압: 배터리 전압이 비이상적으로 낮거나 높은 수치 데이터가 존재
- 데이터 전처리로 이상치를 제거하여 데이터 분석 정확도 향상
- 여러 비지도 학습 결과 비교 분석하여 이상치 제거에 효과적인 모델 선택

<img src='/img/cv_novelty2.png' width='500'>

---

### 2. 이상치 탐지

#### 2.1 가우시안 밀도 추정 방법

- 샘플이 파라미터가 알려지지 않은 가우시안 분포에서 생성되었다고 가정하는 확률 모델
- 밀도 임계값을 정하여 밀도가 낮은 지역에 있는 모든 샘플을 이상치로 가정
- 깨끗한 데이터셋에서 특이치 탐지로 사용 가능

<img src='/img/cv_novelty3.png' width='700'>

#### 2.2 Robust Covariance

- 데이터에서 Determinant of sample covariance matrix를 최소로 만드는 h개의 데이터를 뽑아 그들만 이용하여 variance나 mean을 구하는 방법
- 이상치의 영향을 받지 않고 이상치를 탐지 가능

<img src='/img/cv_novelty4.png' width='700'>

#### 2.3 One-class SVM

- SVM이지만 클래스가 하나. 원본 공간으로부터 고차원 공간에 있는 샘플을 분리
- 새로운 샘플이 이 영역 안에 놓이지 않는 다면 이는 이상치.
- 고차원 데이터셋에 잘 작동하나 대규모 데이터셋으로 확장은 어렵다.

<img src='/img/cv_novelty5.png' width='700'>

#### 2.4 Isolation Forest

- 고차원 데이터셋에서 이상치 감지를 위한 알고리즘
- 무작위로 성장한 결정 트리로 구성된 랜덤 포레스트 생성
- 모든 샘플이 다른 샘플과 격리될 때까지 진행하고 다른 샘플과 멀리 떨어져있는 샘플을 이상치로 판단

<img src='/img/cv_novelty6.png' width='700'>

#### 2.5 Local Outlier Factor

- 주어진 샘플 주위의 밀도와 이웃 주위의 밀도를 비교

<img src='/img/cv_novelty7.png' width='700'>

---

### 3. 결과

- 현재 사용하는 cv, 2차원 데이터에서 가우시안 밀도 추정 방법이 가장 적절하다고 판단
- 현재 가우시안 밀도 추정 방법을 이용하여 데이터 이상치를 제거하여 DB에 저장하는 코드 작성 중
