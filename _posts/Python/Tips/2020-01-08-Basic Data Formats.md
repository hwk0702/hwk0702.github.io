---

layout: post

title: "Basic Data Formats"

date: 2020-01-08 15:50:07

categories: [Python/Tips]

description:

image: /img/dataformat.png

published: true

canonical_url:

---

Data formats
------------

### 데이터 형식이 중요한 이유

-	데이터 생성 및 소비를위한 다양한 환경, OS, SW, HW…
-	목적에 따라 너무 많은 데이터 형식. (Human consumable data, Machine consumable data)

------------------------------------------

## CSV

-	Comma Separated Version file
-	장점: 숫자나 문자열로 구성되어 있는 표(혹은 스프레드시트) 형태의 데이터가 일반 텍스트로 저장되므로 이를 저장하거나 전송하고 처리할 수 있는 프로그램이 다양
-	단점: 수식 없이 오직 데이터만 저장 가능, 각 셀이 은 자료형이 없는 raw data이다.

### Read by Python
-	csv.reader (file)은 행 단위 액세스에 대한 Iterator type object를 리턴.
-	각 줄에 대해 목록 유형과 같은 특정 셀에 액세스 할 수 있다.


```python
import csv

# f = open('범죄발생장소_2016년_.csv', 'r', encoding='utf-8')
f = open('범죄발생장소_2016년_.csv', 'r')
rdr = csv.reader(f)
for line in rdr:
print(line[1])
f.close()
```

### Write by Python
- writerow () 함수를 사용하여 각 행을 작성할 수 있다.
- 한 행은 하나의 리스트 형식으로 나타낸다.

```python
import csv

f = open(‘myfile.csv', 'w', newline='')
wr = csv.writer(f)
wr.writerow([1, "김정수", False])
wr.writerow([2, "박상미", True])
f.close()
```
---------------------------------------------
## XML
- eXtensible Markup Language
- 구조적, 계층 적, 자기 설명 언어
- 가장 강력한 데이터 포맷 중 하나
- HTML은 특별한 유형의 XML
- <node attr=“value” …>
- Node = element = item
	* Root node <- the most top node
- 장점:
	1. 문법과 형식이 단순하다.
	2. 유니코드로 작성되는 텍스트 형식이기 때문에, 호환성이 좋다.
	3. 메타 언어이기 때문에 새로운 tag를 정의해서 사용할 수 있다. 즉, 확정성이 좋다.
	4. XML문서는 data와 meta-data가 tag형식으로 동시에 저장됩니다. 따라서 누구나 쉽게 data와 meta-data를 구분할 수 있고, 따라서 쉽게 이해할 수 있다.
	5. data의 내용과 표현이 완전히 분리되어 있기 때문에 우리는 data를 좀더 쉽게 다룰 수 있다.
	6. Tree구조인 XML 문서는 데이터 검색 시에 비교, 연산 과정이 간단하기 때문에 원하는 결과를 더욱 빨리 얻게 할 수 있다.
- 단점:
	1. 지나치게 많은 것을 정의해 주어야 한다.
	2. 속도가 느리다.
<br> <img src="/img/xml.jpg" width="150">

일반적으로 데이터 분석을 위해 XML을 작성할 필요가 없으므로 parsing만 다룬다.

### Parsing by Python
- 먼저, root를 얻는다.
- 구조에 따라 자식 노드를 찾는다.

```python
from xml.etree.ElementTree import parse

tree = parse("상표_공보_2015년_샘플_.xml")
root_node = tree.getroot()
print(root_node)
print(root_node.find("KR_Bibliographic").find("KR_PublishingORG").text)
print(root_node.find("KR_Bibliographic").find("KR_PublishingORG").get("TYPE"))
```

```python
from xml.etree.ElementTree import fromstring
import requests

response = requests.get("RSS_URL")
root_node = fromstring(response.content)
print(root_node)
print(root_node.find("channel").find("description").text)

items = root_node.find("channel").findall("item")
for item in items:
	print(item.find("title").text)
	print(item.find("link").text)
```

---------------------------------------------------------------
##JSON
- JavaScript Object Notation
- 본래는 자바스크립트 언어로부터 파생
- 속성-값 쌍 또는 "키-값 쌍"으로 이루어진 데이터 오브젝트를 전달하기 위해 인간이 읽을 수 있는 텍스트를 사용하는 개방형 표준 포맷
- 장점:
	1. 내용이 함축적으로 최소한의 정보만 표현
	2. 용량이 적고 빠른 속도
	3. 언어에 독립적
	4. 사용하기 쉽다.
	5. 확장이 용이
-단점:
	1. 내용이 함축적이다 보니 의미 파악이 힘들 수 있다.
	2. 대용량급 데이터 송수신에는 부적합한 모습도 있다.

### Read by Python

```python
import json

f = open("naver_search.json",'r', encoding="utf-8")
json_text = f.read()

dict = json.loads(json_text)

print(dict['lastBuildDate'])
for item in dict['items']:
	print(item['title'])
	print(item['link'])
```

------------------------------------------------------
## 참고 내용
### 파일 입출력
1. 파일 생성: open()
	* 파일 객체를 사용한 후에는 반드시 closer() 함수를 이용하여 객체를 반환하여야 한다.
	```python
	#파일 객체 = open(파일명, 파일 속성)
	f = open(“test.txt”, “w”)
	f.close()
	```
	<img src="/img/file1.jpg">

2. 파일 읽기: readline(), readlines(), read()
	* 파일 한줄씩 읽기: readline()
	```python
	f = open("c:/python_sample/test.txt", "r")
	print(f.readline())
	f.close()
	```
	```python
	f = open("c:/python_sample/test.txt", "r")
	while True:
		line = f.readline()
		if not line:
			break
		print(line)
	f.close()
	```
	* 파일 전체를 리스트로 읽어오기: readlines()
	```python
	f = open("c:/python_sample/test.txt", "r")
	lines = f.readlines()
	for line in lines:
		print(line)
	f.close()
	```
	* 파일 전체를 객체로 읽어오기: read()
	```python
	f = open("c:/python_sample/test.txt", "r")
	lines = f.read()
	print(lines)
	f.close()
	```
3. 파일 쓰기: write()
	* 행단위 입력: write()
	```python
	f = open("c:/python_sample/test.txt", 'w')
	f.write("첫번째 줄입니다")
	f.write("두번째 줄입니다")
	f.close()
	```
	* 개행문자의 추가: \n
	```python
	f = open("c:/python_sample/test.txt", 'w')
	f.write("첫번째 줄입니다")
	f.write("\n")
	f.write("두번째 줄입니다")
	f.write("\n")
	f.close()
	```
	* 파일 내용 추가: 'a' 속성
	```python
	f = open("c:/python_sample/test.txt", 'a')
	f.write("추가한 줄입니다")
	f.close()
	```
4. with 문
- with문과 함께 사용하면 close()를 호출하지 않아도 된다. with 블록을 벗어나면서 자동으로 close() 호출
	```python
	with open("c:/python_sample/test.txt", "r") as f:
		lines = f.read()
		print(lines)
	```
