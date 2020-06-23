---

title: skin cancer prediction

subtitle: Skin cancer data analysis and prediction model

date: 2019-06-01 14:50:07

categories: [Projects]

description: This is a project description

product_code: 

published: true

layout: product

image: /img/skincancer.png

price:

show_sidebar: false

features:
  - label: Incheon University
    icon: fa-location-arrow
  - label: 2019.03 ~ 2019.06
    icon: fa-calendar-alt
  - label: 피부암 이미지 데이터를 이용하여 데이터 분석 및 CNN 기반 예측 모델 개발
    icon: fa-file-alt
  - label: Python, Tensorflow, Keras
    icon: fa-code
  - label: https://github.com/hwk0702/Skin-cancer-data-analysis-and-prediction-model
    icon: fab fa-github

rating: 3

---

# Skin cancer data analysis and prediction model

### 1. 소개

#### 1.1 피부암

<img src='/img/skincancer1.png' width='500'>

- 피부암(skin cancer)은 피부에 발생하는 악성 종양 때문에 생기는 암 질환이다.
- 대표적인 종류로는 기저세포암, 편평상피세포암, 흑색종이 있다.

<img src='/img/skincancer2.png' width='300'>

---

### 2. 데이터

#### 2.1 데이터 구조

<img src='/img/skincancer3.png' width='500'>

<img src='/img/skincancer4.png' width='300'>

<img src='/img/skincancer5.png' width='300'>

- 10015개의 피부암 사진으로 구성

#### 2.2 EDA

<img src='/img/skincancer6.png' width='400'><img src='/img/skincancer7.png' width='300'>

---

### 3. 데이터 전처리

1) Null값을 갖는 모든 행 제거

2) Csv파일의 image_id와 실제 이미지 파일의 위치를 path로 저장

<img src='/img/skincancer8.png' width='500'>

3) 이미지 파일들을 읽어와서 array로 저장

<img src='/img/skincancer9.png' width='500'>

4) train, test 데이터 나누기

<img src='/img/skincancer10.png' width='500'>

5) 이미지 데이터를 정규화 하기

<img src='/img/skincancer11.png' width='500'>

6) Label Encoding 하기

<img src='/img/skincancer12.png' width='500'>

---

### 4. 모델

#### 4.1 CNN 구성

<img src='/img/skincancer13.png' width='500'>

<img src='/img/skincancer14.png' width='500'>

<img src='/img/skincancer15.png' width='500'>

<img src='/img/skincancer16.png' width='500'>

---

### 5. 결과

<img src='/img/skincancer17.png' width='500'>

<img src='/img/skincancer18.png' width='200'>





