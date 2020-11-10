---
layout: post
title: Python for Data Science and AI
subtitle: Course summary - IBM Data Science Professinal 8
categories: markdown
tags: [Data Sceience, Coursera, IBM, Python, 정리노트]
---

*본 포스트는 [IBM Data Science 특화 과정][coursera-ibm-ds] 중 [Python for Data Science and AI][coursera-ibm-ds-4]에 대한 정리노트입니다.*

> IBM Data Science 전문가 과정 : 정리노트   
  1. What is Data Science?
  1. Tools for Data Science
  1. Data Science Methodology
  1. Python for Data Science and AI
  1. Databases and SQL for Data Science
  1. Data Analysis with Python
  1. Data Visualization with Python
  1. Machine Learning with Python
  1. Applied Data Science Capstone

***

* Cheat-sheet
  * [Python2.7][cheat-sheet-python27]


## 1 Python Basics

~~~Notebook
# Check python version
import sys
print(sys.version)
~~~

### 1.1 Types
[Jupyter Notebook 정리노트][ipynb-4-1-1]

|     | int | float | str | bool |
| --- | --- | ----- | --- | ---- |
| Ex  | 1, -1| 3.141|'ABC'|True, False|
| Numeric? | Yes | Yes | No | Possible |
| Indexing? | No | No | Yes | No |


* Cast (타입 변경): `int`, `float`, `str`, `bool`

> `sys.float_info` : float max/min 정보 등 확인

### 1.2 Expressions and Variables

* Division operators
    1. division : 25/6 => 4.111.., float으로 결과 반환
    2. dividor : 25//6 => 4, int로 몫만 반환

### 1.3 String Operations

[Jupyter Notebook 정리노트][ipynb-4-1-2]

* String 자료 구조는 기본적으로 tuple로 이해 가능
  * Indexing
    * Negative Indexing
  * Slicing
  * Stride (큰 보폭으로 걷다) : ex. string[::2] => 매 2개씩 출력
  * Concatenate

* Escape
  * Backslash \ : `\n` new line, `\t` tab
  * \ 출력하기
    1. `\\`  <= 두 번 연속 붙여쓰기
    2. string 앞에 r 입력 (raw): ex. `print(r" Michael Jackson \ is the best" )`

* Method
  * Upper, Lower: `str.upper()`, `str.lower()`
  * Find : `str.find('parameter')`
    * 발견된 첫 번째 index 숫자를 반환
  * Replace : `str.replace('FIND_SEN', 'REPLACE_SEN')`
    * 치환 후 해당 string을 반환

***

## 2 Python Data Structures

|      |	Tuple	| List	| Dictionary	| Set |
| ---- | ----- | ------| ----------- | ----- |
| Ex	 |('Book 1', 12.99)|['apple', 'banana', 'orange']|{'name': 'Joe', 'age': 10}|{10, 20, 12}|
|Mutable? |Immutable|Mutable|Mutable	|Mutable|
|Ordered?	|Ordered	|Ordered	|Preserves order since Python 3.7	|Unordered|
|Iterable?	|Yes (takes linear time)	|Yes (takes linear time)	|Yes (constant time)	|Yes (constant time)|
|Use case	|Immutable data	|Data that needs to change	|Key/Value pairs	|Unique items|


### 2.1 Lists and Tuples
[Jupyter Notebook 정리노트 - Tuple][ipynb-4-2-1]   
[Jupyter Notebook 정리노트 - List][ipynb-4-2-2]

> Tuple과 List는 거의 동일. 단, Tuple은 Immutable, List는 Mutable하여 특성 차이가 발생. 보통 변하면 안 되는 중요한 정보를 tuple로 처리하고 나머지는 list가 용이.

* Tuples
  * sort: `sorted(TUPLE)`
  * length: `len(TUPLE)`

* List
  * `LIST.expand(LIST)` : 한꺼번에 추가 (Concatenate 가능)
  * `LIST.append(ITEM)` : 한 개씩만 추가
    * List를 `append`할 경우, 한 항목으로 추가되므로 주의!
  * `del(LIST[INDEX])` : 항목 삭제

* String --> List : split
  * `STR.split()` : 구분자 생략 시, 공백 기준으로 구분 후 list 생략
  * `STR.split('SEPORATOR')` : 구분자를 별도 지정도 가능

* Copy & Clone
  * B = A일 경우, B는 A를 참조. 즉, A가 변화하면 B값도 같이 변화
  * B = A[:]일 경우, B는 A를 복제 후 신규 생성. 이 경우, B는 더이상 A와 관련 없음

### 2.2 Sets

[Jupyter Notebook 정리노트 - Sets][ipynb-4-2-3]

> No order, Unique values only

* Operation
  * Define
    1. A = `{ITEM1, ITEM2, ...}`
    1. A = `set(LIST)`
  * Add/Remove
    * `SET.add(ITEM)` : 항목 추가
    * `SET.remove(ITEM)` : 항목 삭제

* `in`
  * ITEM `in` SET/LIST/TUPLE/DICT : 포함 여부 판단 후 bool 반환

* Logic - set A, B
  * A U B : `A.union(B)`
  * A & B : `A & B`, `A.intersection(B)`
  * A - B : `A.difference(B)`
  * B - A : `B.difference(A)`
  * `A.issuperset(B)` : A는 B를 포함하는가? Bool 반환
  * `A.issubset(B)` : A는 B에 포함되는가? Bool 반환

### 2.3 Dictionaries

[Jupyter Notebook 정리노트 - Dictionaries][ipynb-4-2-4]

> Key & Value로 정의
  * Key : Unique value only, LIST의 INDEX 역할
  * Dicionary : Duplicate 가능

* Operation
  * Define : `{'KEY1':'VALUE1', ...}`
  * Add : `DICT_NAME['NEW_KEY'] = 'VALUE'`
  * Delete : `del(DICT_NAME['KEY'])`

* Key/Values
  * `DICT.keys()` : key 목록을 List로 반환
  * `DICT.values()` : value 목록을 List로 반환

***

## 3 Python Programming Fundamentals

### 3.1 Conditions and Branching

[Jupyter Notebook 정리노트 - Conditions][ipynb-4-3-1]

* Comparison operators
  * Operatior
    * `==`, `!=`
    * `>`, `<`, `>=`, `<=`
  * 비교 결과는 boolean 형태로 반환 (True, False)

> 문자의 경우도 비교 가능
> 첫 대문자부터 ASCII 코드 번호로 비교 (대소문자 주의!)

* Logical operators  : `and`, `or`, `not`

|  A  |  B  |     |`and |`or` |`not`|
| --- | --- | --- | --- | --- | --- |
|False|False|     |False|False|True |
|False|True |     |False|True |True |
|True |False|     |False|True |False|
|True |True |     |True |True |False|

*`not` 연산자의 경우, A만 대상으로 계산한 결과임*

* **IF** statment

~~~Python
if CONDITION:  # 조건은 bool 형태로 반환되어야 함
  statement
elif CONDITION:
  statement
else:         # else는 상기 조건을 모두 미충족되었을 때만 실행
  statement
~~~

### 3.2 Loops

[Jupyter Notebook 정리노트 - Loops][ipynb-4-3-2]

* `range` : 필요 크기의 숫자 컨테이너를 생성
  1. `range(n)` : 0부터 n-1까지
  2. `range(i, n)` : i부터 n-1까지
  3. `range(i, n, k)` : i부터 n-1까지 k만큼 간격으로

> Python3부터는 별도로 List를 생성하지 않고, range 객체로 취급됨

* `enumerate` : 반복문에서 횟수 확인에 사용
  * tuple - (index, element) 형태로 결과 반환

~~~Python/Example
>> t = [1,3,5,7,9]
>> for i in enumerate(t):
      print(i)
...
(0, 1)
(1, 3)
...
> for i, v in enumerate(t):
      print(i, v)
...
0  1
1  3
...
~~~

* **for** loop

~~~Python
for COUNTER in COLLECTION:
  statement
~~~

* **while** loop

~~~Python
while CONDTION:
  statement
~~~

> `for`와 `while` loop의 차이는 반복 횟수를 사전에 지정하느냐, 혹은 조건에 따라 중지하느냐에 따라 구분

### 3.3 Functions

[Jupyter Notebook 정리노트 - Functions][ipynb-4-3-3]

~~~Python
def FUNC_NAME(ARGUMENTS):
  """
  documentation  # for HELP command
  """
  BODY  
  return RESULT
~~~

* Tips
  * `help(FUNC_NAME)` : 함수의 documentation 확인
  * `if` 분기로 여러 개의 `return`을 지정 가능

* Default argument value 설정
  * `ARG_NAME = VALUE` : def 시, arg 값에 사전 할당 가능 (값이 들어오면 변경됨)

* `global VAR_NAME` : 전역 변수 지정. 함수 밖에서도 접근 가능

* [Multiple arguments - collection (변수 숫자가 정해지지 않은 경우)][multiple-arg]
  1. `*args` : tuple 형태로 변수 대기
  2. `**kwargs` : dictionary 형태로 변수 대기 (key/value pair)

> 변수 순서 : normal arg > *args > ** kwargs - 틀릴 경우, 에러 발생

### 3.4 Objects and Classes

[Jupyter Notebook 정리노트 - Objects][ipynb-4-3-4]



***

## 4. Working with Data in Python

### 4.1 Reading files with open

### 4.2 Writing files with open

### 4.3 Loading data with Pandas

### 4.4 Working with and Saving data with Pandas

### 4.5 Numpy

***

## 5. Final Project - Analyzing US Economic Data and Building a Dashboard


[coursera-ibm-ds]: https://www.coursera.org/professional-certificates/ibm-data-science
[coursera-ibm-ds-4]: https://www.coursera.org/learn/python-for-applied-data-science-ai?specialization=ibm-data-science

[cheat-sheet-python27]: http://www.astro.up.pt/~sousasag/Python_For_Astronomers/Python_qr.pdf
[multiple-arg]: https://brunch.co.kr/@princox/180

[ipynb-4-1-1]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-1-1-Types.ipynb
[ipynb-4-1-2]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-1-2-Strings.ipynb
[ipynb-4-2-1]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-2-1-Tuples.ipynb
[ipynb-4-2-2]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-2-2-Lists.ipynb
[ipynb-4-2-3]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-2-3-Sets.ipynb
[ipynb-4-2-4]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-2-4-Dictionaries.ipynb
[ipynb-4-3-1]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-3-1-Conditions.ipynb
[ipynb-4-3-2]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-3-2-Loops.ipynb
[ipynb-4-3-3]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-3-3-Functions%20.ipynb
[ipynb-4-3-4]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-3-4-Classes.ipynb
