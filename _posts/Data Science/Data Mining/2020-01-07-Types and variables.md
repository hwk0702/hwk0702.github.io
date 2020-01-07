---

layout: post

title: "데이터 타입"

date: 2020-01-07 10:50:07

categories: [Data Science/Data Mining]

description:

image: /img/data.png

published: true

canonical_url:

---

﻿데이터 타입
===========

---

데이터 객체 및 속성 유형
------------------------

-	데이터 집합은 데이터 객체 집합으로 구성된다.
-	DB의 경우, 각 **행**은 **데이터 객체**에 해당하고, **열**은 **속성**에 해당한다.
-	**속성**은 **데이터 객체의 특성 또는 특징을 나타내는 데이터 필드**이다.
-	속성은 통계에서 변수라고 하며, 기계학습의 특징이다.
-	주어진 객체를 기술하는데 사용되는 속성세트를 **속성 벡터**라고 부른다.
-	하나의 속성을 포함하는 데이터의 분포를 **단변량**이라고 한다.

속성의 타입
-----------

### 1. nominal attribute (규범적 속성)

-	**어떤 상징이나 사물의 이름**
-	ex) hair-color, marital-status, ID-numbers, etc.
-	**범주형 속성**이라고도 한다. (categorical attribute)
-	nominal attribute의 가능한 값에 숫자나 코드를 사용할 수 있다. 이 경우, 수학연산은 의미가 없다.

### 2. binary attribute (이진 속성)

-	**0과 1**의 두 가지 상태
-	두 상태가 true 및 false에 해당하면 Boolean 이라고도 불림

### 3. ordinal attribute (순서 속성)

-	ordinal attribute는 **의미 있는 순서 또는 순위**를 가질 수 있는 값을 갖는 속성이지만, 연속값 사이의 크기는 알려져 있지 않다.
-	ex) Customer satisfaction - 0: very dissatisfied, 1: dissatisfied, ... , 4: very satisfied
-	ordinal attribute의 중심 경향은 **mode**와 **median**으로 표현 될 수 있으나, 평균은 정의 될 수 없다.
-	실제 크기나 양을 주지 않고 물체의 특징을 설명

### 4. numeric attribute (숫자 속성)

-	**interval - scaled attribute** <br> * 크기가 같은 단위로 측정 <br> * 가치의 순위를 제공하고, 가치의 차이를 비교하고 정량화 할 수 있게 해준다. <br> * ex) temperature (celsius, fahrenheit)
-	**ratio-scaled attribute** <br> * 고유의 영점을 가진 numeric attribute <br> * 측정값이 ratio-scaled이면 값은 다른 값의 배수로 말 할 수 있으며, 값의 차이와 mean, median, mode를 계산 할 수 있다.
-	ex) Kelvin temperature scale, weight, height

### 5. discrete vs continuous attribute (이산/불연속, 연속 속성)

-	이산 속성은 정수로 표현되거나 표현되지 않을 수도 있는 유한 또는 무한대의 값 집합을 가진다.
-	연속 속성은 일반적으로 부동 소수점 변수로 표시된다.

데이터 셋의 유형
----------------

1.	record data
2.	record data, transaction data, data matrix, document-term matrix
3.	graph data
4.	world wide data, molecular structures
5.	ordered data
6.	spatial, temporal, sequential, genetic sequence

데이터 셋의 특징
----------------

-	**Dimensionality(차원)**: 데이터 셋을 포함하는 속성의 수
-	**Sparsity(희소성)**: 0이 아닌 의미 있는 값만 저장
-	**Resolution(선명도)**: 패턴은 스케일에 영향을 미친다. <br> * 해상도가 너무 좋은 경우 패턴이 보이지 않거나 노이즈가 있을 수 있다. <br> * 해상도가 너무 거칠면 패턴이 사라질 수 있다.

중심 경향 측정
--------------

1.	Mean (평균)
2.	데이터의 중앙을 대표하는 통계값 $\bar{x}={\sum*{i=1}^N x_i \over N}$ or $\bar{x}={\sum*{i=1}^N w*ix_i \over \sum*{i=1}^N w_i}$

3.	Median (중위수)

4.	숫자를 크기에 따라 정렬하였을 때 가장 중앙(50%)에 위치한 값

5.	Mode (최빈수)

6.	가장 많이 나타난 수

7.	Midrange

8.	가장 큰 값과 가장 작은 값의 평균

9.	Skewness (왜도/비대칭도)

10.	실수 값 확률 변수의 확률 분포의 비대칭성을 나타내는 지표
