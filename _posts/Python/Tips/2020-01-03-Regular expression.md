---

layout: post

title: "정규표현식과 re 모듈"

date: 2020-01-03 10:50:07

categories: [Python/Tips]

description:

image: /img/regular.png

published: true

canonical_url:

---

정규표현식
----------

-	regular expression
-	특저한 패턴과 일치하는 문자열을 '검색', '치환', '제거' 하는 기능을 지원
-	정규표현식의 도움없이 패턴을 찾는 작업(Rule 기반)은 불완전 하거나, 작업의 cost가 높음
-	e.g) 이메일 형식 판별, 전화번호 형식 판별, 숫자로만 이루어진 문자열 등

### raw string

-	문자열 앞에 r이 붙으면 해당 문자열이 구성된 그래도 문자열 변환

```python
a = 'abcdef\n' # escape 문자열
print(a)
```

```
abcdef

```

이 경우 한 줄이 띄어진 채로 출력

```python
b = r'abcdef\n'
print(b)
```

```
abcdef\n
```

이 경우 문자열 그대로 출력

###기본 패턴

-	a, X, 9 등등 문자 하나하나의 character들은 정확히 해당 문자와 일치 <br> - e.g) 패턴 test는 test 문자열과 일차 <br> - 대소문자의 경우 기본적으로 구별하나, 구별하지 않도록 설정 가능 - 몇몇 문자들에 대해서는 예외가 존재하는데, 이들은 특별한 의미로 사용 됨 <br> .^$*+{}[]/() - .(마침표) - 어떤 한개의 character와 일치 (newline(엔터) 제외) - \w - 문자 character와 일치 [a-zA-Z0-9_] - \s - 공백문자와 일치 - \t, \n, \r - tab, newline, return - \d - 숫자 character와 일치 [0-9] - ^ = 시작, $ = 끝 각각 문자열의 시작과 끝을 의미 - \가 붙으면 스페셜한 의미가 없어짐. 예를 들어 .는 .자체를 의미 \\는 \를 의미 - 자세한 내용은 링크 참조 [https://docs.python.org/3/library/re.html](https://docs.python.org/3/library/re.html)

### search method

-	첫번째로 패턴을 찾으면 match 객체를 반환
-	패턴을 찾지 못하면 None 반환

```python
import re
m = re.search(r'abc', 'abcdef')
print(m.start())
print(m.end())
print(m.group())
```

```
0
3
abc
```

```python
m = re.search(r'abc', '123abdef')
print(m)
```

```
None
```

```python
m = re.search(r'\d\d', '112abcdef119')
m
```

```
<_sre.SRE_Match object; span=(0, 2), match='11'>
```

### metacharacter (메타 캐릭터)

#### [] 문자들의 범위를 나타내기 위해 사용

-	[]내부의 메타 캐릭터는 캐릭터 자체를 나타냄
-	e.g) <br> * [abck] : a or b or c or k <br> * [abc.^] : a or b or c or . or ^ <br> * [a-d] : -와 함께 사용되면 해당 문자 사이의 범위에 속하는 문자 중 하나 <br> * [0-9] : 모든 숫자 <br> * [a-z] : 모든 소문자 <br> * [A-Z] : 모든 대문자 <br> * [a-zA-Z0-9] : 모든 알파벳 문자 및 숫자 <br> * [^0-9] : ^가 맨 앞에 사용되는 경우 해당 문자 패턴이 아닌 것과 매칭

```python
m = re.search(r'[cbm]at', 'cat')
print(m)
m = re.search(r'[cbm]at', 'aat')
print(m)
m = re.search(r'[^cbm]at', 'aat')
print(m)
```

```
<_sre.SRE_Match object; span=(0, 3), match='cat'>
None
<_sre.SRE_Match object; span=(0, 3), match='aat'>
```

```python
m = re.search(r'[0-4]at', '1at')
print(m)
m = re.search(r'[0-4]at', '7at')
print(m)
```

```
<_sre.SRE_Match object; span=(0, 3), match='1at'>
None
```

###

1.	다른 문자와 함께 사용ㅇ되어 특수한 의미를 지님 <br> - \d : 숫자를 [0-9]와 동일 <br> - \D : 숫자가 아닌 문자 [^0-9]와 동일 <br> - \s : 공백 문자(띄어쓰기, 탭, 엔터 등) <br> - \S : 공백이 아닌 문자 <br> - \w : 알파벳 대소문자, 숫자 [0-9a-zA-Z]와 동일
2.	메타 캐릭터가 캐릭터 자체를 표현하도록 할 경우 사용 <br> - `\.`, `\\`

```python
m = re.search(r'\sand', 'apple and banana')
print(m)
m = re.search(r'\Sand', 'apple and banana')
print(m)
```

```
 <_sre.SRE_Match object; span=(5, 9), match=' and'>
None
```

```python
m = re.search(r'.and', 'pand')
print(m)
m = re.search(r'.and', '.and')
print(m)
m = re.search(r'\.and', 'pand')
print(m)
m = re.search(r'\.and', '.and')
print(m)
```

```
_sre.SRE_Match object; span=(0, 4), match='pand'>
<_sre.SRE_Match object; span=(0, 4), match='.and'>
None
<_sre.SRE_Match object; span=(0, 4), match='.and'>
```

### 반복패턴

-	패턴 뒤에 위치하는 *, +, ?는 해당 패턴이 반복적으로 존재하는지 검사 <br> - '+' -> 1번 이상의 패턴이 발생 <br> - '*' -> 0번 이상의 패턴이 발생 <br> - '?' -> 0 혹은 1번의 패턴이 발생
-	반복 패턴의 경우 greedy하게 검색함, 즉 가능한 많은 부분이 매칭되도록 함 <br> - e.g) a[bcd]*b 패턴을 abcdbdccb에서 검색하는경우, ab/abcb/abcbdccd 전부 가능하지만 최대한 많은 부분이 매칭된 abcbdccb가 검색된 패턴

```python
re.search(r'a[bcd]*b', 'abcbdccb')
```

```
<_sre.SRE_Match object; span=(0, 8), match='abcbdccb'>
```

```python
re.search(r'b\w+a', 'banana')
```

```
<_sre.SRE_Match object; span=(0, 6), match='banana'>
```

```python
re.search(r'i+', 'piigiii')
```

```
<_sre.SRE_Match object; span=(1, 3), match='ii'>
```

```python
m = re.search(r'pi+g', 'pg')
print(m)
m = re.search(r'pi*g', 'pg')
print(m)
```

```
None
<_sre.SRE_Match object; span=(0, 2), match='pg'>
```

```python
re.search(r'https?', 'http://naver.com')
```

```
None
<_sre.SRE_Match object; span=(0, 4), match='http'>
```

### ^*, *$

-	^ 문자열의 맨 앞부터 일치하는 경우 검색
-	$ 문자열의 맨 뒤부터 일치하는 경우 검색

```python
m = re.search(r'b\w+a', ' cabana')
print(m)
m = re.search(r'^b\w+a', ' cabana')
print(m)
m = re.search(r'b\w+a$', ' cabana')
print(m)
m = re.search(r'b\w+a$', ' cabanap')
print(m)
```

```
<_sre.SRE_Match object; span=(3, 7), match='bana'>
None
<_sre.SRE_Match object; span=(3, 7), match='bana'>
None
```

### grouping

-	()을 사용하여 그루핑
-	매칭 결과를 각 그룹별로 분리 가능
-	패턴 명시 할 때, 각 그룹을 괄호() 안에 넣어 분리하여 사용

```python
m = re.search(r'\w+@.+', 'test@gmail.com')
print(m.group())
m = re.search(r'(\w+)@(.+)', 'test@gmail.com')
print(m.group()) # group(0)과 동일
print(m.group(1))
print(m.group(2))
```

```
test@gmail.com
test@gmail.com
test
gmail.com
```

### {}

-	*, +, ?을 사용하여 반복적인 패턴을 찾는 것이 가능하나, 반복의 횟수 제한은 불가
-	패턴 뒤에 위치하는 중괄호 {}에 숫자를 명시하면 해당 숫자 만큼의 반복인 경우에만 매칭
-	{4} - 4번 반복
-	{3,4} - 3 ~ 4번 반복

```python
m = re.search(r'pi+g', 'piiig')
print(m)
m = re.search(r'pi{3}g', 'piiig')
print(m)
m = re.search(r'pi{3}g', 'piiiig')
print(m)
m = re.search(r'pi{3,5}g', 'piiiig')
print(m)
m = re.search(r'pi{3,5}g', 'piiiiiig')
print(m)
```

```
<_sre.SRE_Match object; span=(0, 5), match='piiig'>
<_sre.SRE_Match object; span=(0, 5), match='piiig'>
None
<_sre.SRE_Match object; span=(0, 6), match='piiiig'>
None
```

### 미니멈 매칭(non-greedy way)

-	기본적으로 *, +, ?를 사용하면 greedy하게 동작함
-	*?, +?을 이요하여 해당 기능을 구현

```python
re.search(r'<.+>', '<html>haha</html>')
```

```
<_sre.SRE_Match object; span=(0, 17), match='<html>haha</html>'>
```

```python
re.search(r'<.+?>', '<html>haha</html>')
```

```
<_sre.SRE_Match object; span=(0, 6), match='<html>'>
```

### {}?

-	{m,n}의 경우 m번에서 n번 반복하나 greedy하게 동작
-	{m,n}?로 사용하면 non-greedy하게 동작. 즉, 최소 m번만 매칭하면 만족

```python
re.search(r'a{3,5}', 'aaaaa')
```

```
<_sre.SRE_Match object; span=(0, 5), match='aaaaa'>
```

```python
re.search(r'a{3,5}?', 'aaaaa')
```

```
<_sre.SRE_Match object; span=(0, 3), match='aaa'>
```

### match

-	search와 유사하나, 주어진 문자열의 시작부터 비교하여 패턴이 있는지 확인
-	시작부터 해당 패턴이 존재하지 않는다면 None 반환

```python
re.search(r'\d\d\d', 'my number is 123')
```

```
<_sre.SRE_Match object; span=(13, 16), match='123'>
```

```python
re.match(r'\d\d\d', 'my number is 123')
```

```
None
```

### findall

-	search가 최초로 매칭되는 패턴만 반환한다면, findall은 매칭되는 전체의 패턴을 반환
-	매칭되는 모든 결과를 리스트 형태로 반환

```python
re.findall(r'[\w-]+@[\w.]+\w+', 'test@gmail.com haha test2@gmail.com nice test')
```

```
['test@gmail.com', 'test2@gmail.com']
```

### sub

-	주어진 문자열에서 일치하는 모든 패턴을 replace
-	그 결과를 문자열로 다시 반환함
-	두번째 인자는 특정 문자열이 될 수 도 있고 함수가 될 수 도 있음
-	count가 0 이니 경우는 전체를, 1이상이면 해당 숫자만큼 치환 됨

```python
re.sub(r'[\w-]+@[\w.]+\w+', 'great', 'test@gmail.com haha test2@gmail.com nice test')
```

```
'great haha great nice test'
```

```python
re.sub(r'[\w-]+@[\w.]+\w+', 'great', 'test@gmail.com haha test2@gmail.com nice test', count=1)
```

```
'great haha test2@gmail.com nice test'
```

### compile

-	동일한 정규표현식을 매번 다시 쓰기 번거로움을 해결
-	compile로 해당 표현식을 re.RegexObject 객체로 저장하여 사용가능

```python
email_reg = re.compile(r'[\w-]+@[\w.]+\w+')
email_reg.search('test@gmail.com haha test2@gmail.com nice test')
```

```
<_sre.SRE_Match object; span=(0, 14), match='test@gmail.com'>
```
