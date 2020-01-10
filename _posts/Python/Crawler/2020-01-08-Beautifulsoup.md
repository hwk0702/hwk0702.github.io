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

0. beautifulsoup 모듈 설치하기

```
$ pip install beautifulsoup4
```

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
- 예시 HTML

```html
html='''
<html>
  <head>
    <title>Hello BeautifulSoup</title>
  </head>
  <body>
    <div id='upper' class='test'>
      <h3 title='Content Title'>Content Title</h3>
      <p>Test Content</p>
    </div>
    <div id='lower' class='test'>
      <p>Test 1</p>
      <p>Test 2</p>
      <p>Test 3</p>
    </div>
  </body>
<html>'''
```

3. find 함수
- 특정 html tag를 검색
- 검색 조건을 명시하여 찾고자 하는 tag 검색
- 해당 조건에 맞는 하나의 태그(첫 번째 태그)를 가져온다.

```python
soup = BeautifulSoup(html)
print(soup.find('h3'))
print(soup.find('p'))
print(soup.find('div'))
print(soup.find('div', custom='2nd'))
print(soup.find('div', class_='test')) # class는 키워드이기 때문에 뒤에 _
# 여러 태그를 줄 때
attrs = {'id': 'upper', 'class': 'test'}
print(soup.find('div', attrs=attrs))
```
```python
# 출력 결과
<h3 title="Content Title">Content Title</h3>
<p>Test Content</p> # 가장 첫 번째 태그만 찾는다.
<div class="test" custom="1st" id="upper">
<h3 title="Content Title">Content Title</h3>
<p>Test Content</p>
</div>
<div class="test" custom="2nd" id="lower">
<p>Test 1</p>
<p>Test 2</p>
<p>Test 3</p>
</div>
<div class="test" custom="1st" id="upper">
<h3 title="Content Title">Content Title</h3>
<p>Test Content</p>
</div>
<div class="test" custom="1st" id="upper">
<h3 title="Content Title">Content Title</h3>
<p>Test Content</p>
</div>
```

4. find_all 함수
- 조건에 맞는 모든 tag를 리스트로 반환

```python
soup.find_all('div')
```
```python
# 출력 결과
[<div class="test" custom="1st" id="upper">
 <h3 title="Content Title">Content Title</h3>
 <p>Test Content</p>
 </div>, <div class="test" custom="2nd" id="lower">
 <p>Test 1</p>
 <p>Test 2</p>
 <p>Test 3</p>
 </div>]
```

5. get_text 함수
- tag안의 value를 추출
- 부모 tag의 경우, 모든 자식 tag의 value를 추출
```python
tag = soup.find('h3')
print(tag)
print(tag.get_text())
tag = soup.find('div')
print(tag)
print(tag.get_text())
```
```python
# 출력 결과
<h3 title="Content Title">Content Title</h3>
Content Title

<div class="test" custom="1st" id="upper">
<h3 title="Content Title">Content Title</h3>
<p>Test Content</p>
</div>

Content Title
Test Content
```

6. attribute 값 추출하기
- 경우에 따라 추출하고자 하는 값이 attribute에도 존재함
- 이 경우에는 검색한 tag에 attribute 이름을 []연산을 통해 추출가능

```python
tag = soup.find('h3')
print(tag)
print(tag['title'])
```
```python
# 출력 결과
<h3 title="Content Title">Content Title</h3>
'Content Title'
```
