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

* IN
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

### 3.2 Loops

### 3.3 Functions

### 3.4 Objects and Classes

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
[ipynb-4-1-1]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-1-1-Types.ipynb
[ipynb-4-1-2]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-1-2-Strings.ipynb
[ipynb-4-2-1]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-2-1-Tuples.ipynb
[ipynb-4-2-2]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-2-2-Lists.ipynb
[ipynb-4-2-3]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-2-3-Sets.ipynb
[ipynb-4-2-4]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-2-4-Dictionaries.ipynb
