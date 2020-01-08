---

layout: post

title: "beautifulsoup 모듈"

date: 2020-01-08 17:50:07

categories: [Python/Crawler]

description:

image: /img/bs.png

published: true

canonical_url:

---

## beautifulsoup


1.	beautifulsoup 모듈 사용하기

```python
from bs4 import Beautifulsoup
```

2.	HTML 문자열 파싱

  (1) html 파일 열기

  ```python
  with open("example.html") as f:
    soup = BeautifulSoup(f, 'html.parser')
  ```
  (2) urllib를 통해서 웹에 있는 소스 가져오기

  ```python
  import urllib.request
  import urllib.parse


  with urllib.request.urlopen(web_url) as response:
    html = response.read()
    soup = BeautifulSoup(html, 'html.parser')
  ```
  (3) requests를 통해서 웹에 있는 소스 가져오기

  ```python
  import requests

  req = request.get(web_url)
  ```
3. find 함수
- 특정 html tag를 검색
- 검색 조건을 명시하여 찾고자 하는 tag 검색
- 해당 조건에 맞는 하나의 태그(첫 번째 태그)를 가져온다.

```python
soup = BeautifulSoup(html)
print(soup.find('h3'))
```
