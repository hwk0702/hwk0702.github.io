---

layout: post

title: "데이터 탐색"

date: 2020-01-08 09:57:07

categories: [Data Science/Data Mining]

description:

image: /img/data.png

published: true

canonical_url:

---

# 데이터 탐색
--------------------------

## What is Data Exploration
- 데이터 특성을 더 잘 이해하기 위한 데이터의 예비 탐색
- 전처리 or 분석을 위한 올바른 도구 선택 지원
- 패턴 인식

-------------------------

### 1. Frequency and mode
- **Frequency(빈도수)**:
attribute value의 빈도는 데이터 세트에서 값이 발생하는 횟수(시간)의 백분율
- **Mode(최빈수)**: attribute의 mode는 가장 빈번하게 나오는 attribute values
- frequency와 mode는 주로 categorical data에 사용된다.

### 2. Percentiles
- 크기가 있는 값들로 이루어진 자료를 순서대로 나열했을 때 백분율로 나타낸 특정 위치의 값
- 일반적으로 크기가 작은 것부터 나열하여 가장 작은 것을 0, 가장 큰 것을 100으로 한다.
- 100개의 값을 가진 어떤 자료의 20 백분위수는 그 자료의 값들 중 20번째로 작은 값을 뜻한다. 50 백분위수는 중앙값과 같다.

### 3. Measures of Location
- **Mean(평균)**: <br> * 데이터의 중앙을 대표하는 통계 값 <br> * outliers에 민감하다. <br> $$\bar{x}={\sum_{i=1}^N x_i \over N}$$ or $$\bar{x}={\sum_{i=1}^N w_ix_i \over \sum_{i=1}^N w_i}$$
- **Median(중위수)**: * 숫자를 크기에 따라 정렬하였을 때 가장 중앙(50%)에 위치한 값 <br> $$median(x)=\left\{\begin{matrix}
 x_{(r+1)} && \textbf{if} \: m \: \textbf{is odd, i.e,} \: m=2r+1\\ {1 \over 2}(x_{(r)}+x_{(r+1)}) && \textbf{if} \: m \: \textbf{is even, i.e,} \: m=2r
\end{matrix}\right.$$

### 4. Measures of Spread
- **Range**: 최대값과 최소값의 차이
- **Midrange**: 최대값과 최소값의 평균
- **variance(분산)**: 데이터가 평균으로 부처 얼마나 떨어져서 분포하는지 산포를 알아보기 위한 기술량
$$variance(x) = s^2_{x}={1\over{m-1}}\sum_{i=1}^m(x_i-\bar{x})^2$$
- outliers에 민감하기 때문에 다음과 같은 방법을 사용하기도 한다.
<br> $$AAD(x)={1 \over m}\sum_{i=1}^m \left |x_i-\bar{x} \right |$$ <br> $$MAD(x)=median( \left \{ {\left | x_1-\bar{x} \right |} \right \},..., \left \{ {\left | x_m-\bar{x} \right |} \right \})$$ <br> $$IQR$$(interquartile range)는 밑에 설명

### 5. IQR(interquartile range)
- 4분위수는 분포의 중심, 확산 및 모양을 나타낸다.
- 중간에 50% 데이터들이 흩어진 정도
$$IQR=Q_3-Q_1$$
