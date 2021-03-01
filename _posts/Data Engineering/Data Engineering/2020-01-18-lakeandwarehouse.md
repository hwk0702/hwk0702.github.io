---

layout: post

title: "데이터 레이크 vs 데이터 웨어하우스"

date: 2020-01-18 11:50:07

categories: [Data Engineering/Data Engineering]

description:

image: /img/lakeware.png

published: true

canonical_url:

tags: [데이터 레이크, 데이터 웨어하우스, Data Lake, Data Warehouse, ETL, ELT, 데이터 엔지니어링, Data Engineering]
---

## Data Lake vs Data Warehouse

|구분|데이터 레이크|데이터 웨어하우스|
|----|:----------:|:-------------:|
|Data Structure|Raw|Processed|
|Purpose of Data|Not Yet Determined|In Use|
|Users|Data Scientists|Business Professoinals|
|Accessibility|High / Quick to update|Complicated / Costly|

### ETL -> ELT

- ETL : 추출(Extract), 변환(Transform), 적재(Load)
- ETL에서 ELT로 변하는 추세. 즉, 데이터를 추출하고 적재를 한 다음에 나중에 변환하여 사용

<img src='/img/datalake.PNG'>
