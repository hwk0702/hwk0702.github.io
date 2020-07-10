---

layout: post

title: "계층적 군집화"

date: 2020-06-16 17:02:07

categories: [ML/DL/Machine Learning]

description:

image: /img/HC.png

published: true

canonical_url:

tags: [계층적 군집화, Hierarchical Clustering, 머신러닝, Machine Learning]

---

계층적 군집화(Hierarchical Clustering)
----------------------------------------------

- 계층적 트리로 구성된 중첩 클러스터 셋 생성
- Dendrogram으로 시각화

<img src='/img/HC1.PNG' width='400'> 

---

#### 1. 장점

- 특정 수의 클러스터를 가정할 필요가 없다(Dendrogram에서 적절한 수준에서 절단)
- meaningful taxonomies이다.

#### 2. 방법

1) 모든 관측치를 개별 군집으로 간주한다.

<img src='/img/HC2.PNG' width='400'> 

2) 가장 작은 거리를 가진 두 개의 클러스터를 선택한다.

<img src='/img/HC3.PNG' width='400'> 

3) 군집 사이의 거리를 정의한다(다른 군집의 관측치 간의 최소거리로 정의)

<img src='/img/HC4.PNG' width='400'> 

4) 모든 관측치가 단일 군집에 속할 때까지 병합한다.

<img src='/img/HC5.PNG' width='400'> 

<img src='/img/HC6.PNG' width='400'>

<img src='/img/HC7.PNG' width='400'>

<img src='/img/HC8.PNG' width='400'>   

5) 절삭점을 이용하여 클러스터를 정의 할 수 있다.(다른 절삭점을 적용하여 다른 클러스터링 결과 얻을 수 있다.)

<img src='/img/HC9.PNG' width='400'>   

#### 3. 종류

1) Minimum Distance(simple linkage) -> 장: 비타원 모양 처리 가능 / 단: 노이즈와 이상치에 민감

<img src='/img/HC10.PNG' width='400'>   


2) Maximum Distance(complete linkage) -> 장: 노이즈와 이상치에 덜 민감 / 단: 큰 클러스터를 깰 경향, 구상 성단 쪽으로 치우침

<img src='/img/HC11.PNG' width='400'>   

3) Group Distance(Average linkage)

<img src='/img/HC12.PNG' width='400'>   

4) Distance between centroid

<img src='/img/HC13.PNG' width='400'>   

