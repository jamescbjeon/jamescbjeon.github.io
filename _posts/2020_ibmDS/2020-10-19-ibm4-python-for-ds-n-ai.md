---
layout: post
title: IBM4 - Python for Data Science and AI
subtitle: Course summary - IBM Data Science Professinal 4
categories: IbmDataScience
tags: [Data Science, Coursera, IBM, Python, 정리노트]
---

*본 포스트는 [IBM Data Science 특화 과정][coursera-ibm-ds] 중 [4. Python for Data Science and AI][coursera-ibm-ds-4]에 대한 정리노트입니다.*

> IBM Data Science 전문가 과정 : 정리노트
  1. What is Data Science?
  1. Tools for Data Science
  1. Data Science Methodology
  1. [Python for Data Science and AI][ibm4]
  1. Databases and SQL for Data Science
  1. [Data Analysis with Python][ibm6]
  1. [Data Visualization with Python][ibm7]
  1. [Machine Learning with Python
  1. Applied Data Science Capstone

> Jupyter notebook
  * [Type][ipynb-4-1-1]
  * [String][ipynb-4-1-2]
  * [Tuple][ipynb-4-2-1]
  * [List][ipynb-4-2-2]
  * [Set][ipynb-4-2-3]
  * [Dictionary][ipynb-4-2-4]
  * [Condition][ipynb-4-3-1]
  * [Loop][ipynb-4-3-2]
  * [Function][ipynb-4-3-3]
  * [Object/Class][ipynb-4-3-4]
  * [Exception][ipynb-4-3-5]
  * [Read file][ipynb-4-4-1]
  * [Write file][ipynb-4-4-2]
  * [Numpy 1D][ipynb-4-5-1]
  * [Numpy 2D][ipynb-4-5-2]
  * [Simple API][ipynb-4-5-3]
  * [Requestes HTTP][ipynb-4-5-4]
  * [Final assignment][ipynb-4-final]

> [Cheat-sheet][cheat-sheet-python27]

***

## 1 Python Basics

~~~Notebook
# Check python version
import sys
print(sys.version)
~~~

### 1.1 Types
[Jupyter Notebook - Types][ipynb-4-1-1]

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

[Jupyter Notebook - String][ipynb-4-1-2]

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
[Jupyter Notebook - Tuple][ipynb-4-2-1]   
[Jupyter Notebook - List][ipynb-4-2-2]

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

[Jupyter Notebook - Sets][ipynb-4-2-3]

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

[Jupyter Notebook - Dictionaries][ipynb-4-2-4]

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

[Jupyter Notebook - Conditions][ipynb-4-3-1]

* Comparison operators
  * Operator
    * `==`, `!=`, `>`, `<`, `>=`, `<=`
  * 비교 결과는 boolean 형태로 반환 (True, False)
  * 문자도 비교 가능. 첫 글자부터 ASCII 코드 번호로 비교

* Logical operators  : `and`, `or`, `not`
  * *`not` 연산자의 경우, A만 대상으로 계산한 결과임*

|  A  |  B  |     |`and`|`or` |`not`|
| --- | --- | --- | --- | --- | --- |
|False|False|     |False|False|True |
|False|True |     |False|True |True |
|True |False|     |False|True |False|
|True |True |     |True |True |False|


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

[Jupyter Notebook - Loops][ipynb-4-3-2]

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

[Jupyter Notebook - Functions][ipynb-4-3-3]

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

[Jupyter Notebook - Objects][ipynb-4-3-4]

* Class --> Instance : Object --> Attribute
  1. attributes : 자료가 가져야 할 특성
  2. methods : class 자체 내장 함수

~~~Python
# Creating a Class
class CLASS_NAME(object): # 괄호 안은 class parent. 이 경우, object를 사용

  def __init__(self, attr1, ...):  # Constructor
    self.attr1 = ...
    self.attr2 = ...

  def METHOD1(self, ARGS):  # Method
    ...
    return(RETURN_VALUE)
~~~

> `dir(CLASS)` class 내부 호출 가능한 methods/attributes list 반환  

### 3.5 Exception handling

[Jupyter Notebook - Exception][ipynb-4-3-5]   
[Python Document - Exception][doc-python-exception]

* Execution 중 Error 발생 시,
  1. Not prepared : Halt the Execution
  2. Prepared : Raise exception --> 준비된 예외코드 실행
    * ex. 'ZeroDivisionErro', 'NameError', 'IndexError', ...

~~~Python
## try-except-finally structure
try:
    # 실행하려는 코드
except ERROR_CODE:  # 생략가능
    # 별도 에러코드를 분리해서 지정 가능
except:
    # 지정된 에러 이외 예외처리 발생 시 실행 코
else:  # 생략가능
    # 에러가 없을 때 실행되는 코드. try --> else
finally:  # 생략가능
    # 에러 여부와 관계없이 마지막에 실행될 코드
~~~

***

## 4. Working with Data in Python

### 4.1 Reading files with open

[Jupyter Notebook - Read File][ipynb-4-4-1]   

~~~Python
# No-with : 작업 종료 후 .close 필요
fhand = open('PATH/NAME', 'r')
content = fhand.read()   # File obj에서 내용만 불러와 string으로 저장
fhand.close()

# With : .close() 필요 없음
with open('PATH/NAME', 'r') as fhand:
  content = fhand.read()
~~~

* File open
  * Hanlder를 통해 File object로 해당 내용을 불러옴
  * Mode
    1. `r` : Read
    2. `w` : Write
    3. `a` : Append
  * Resource 유실을 막기 위해 사용 완료 후에는 `fhand.close()` 필요
    * 보통 `with` 구문으로 open 후 자동 close

* Textfile Attributes & Methods
  * 줄의 마지막에는 '\n'이 별도 문자로 포함
  * `.read()`
    * Handler 내부 내용을 읽어옴
    * `.read(n)` : n을 별도 지정 시, 해당 문자열 갯수만큼만 불러옴. 다시 사용 시, 종료된 이후부터 재개
  * `.readline(n)` : 지정된 n만큼의 문자열을 읽어오며, \n이 있을 경우 종료
  * `.readlines()` : 개별 줄을 구분하여 list 형태로 저장. 각 항목 마지막에는 \n이 포함


### 4.2 Writing files with open

[Jupyter Notebook - Write File][ipynb-4-4-2]   

~~~Python
# Write : 기존 내용은 무시하고 신규로 작성
with open('PATH/NAME', 'w') as fhand:
  fhand.write(....)

# Append : 기존 내용 이후에 추가
with open('PATH/NAME', 'a') as fhand:
  fhand.write(....)

# 파일 복사
with open('PATH/NAME', 'r') as readfile:
  with open('PATH/NAME', 'w') as writefile:
    for line in readfile:
      writefile.write(line)
~~~

* Write/Append
  * `.write(CONTENT)` 신규 내용 작성. 재호출 시, 종료된 이후부터 작성.

### 4.3 Pandas

* import : `import pandas as pd`
* load : `pd.read_csv('PATH')`, `pd.read_excel('PATH')`, ...
* save : `to_csv('NAME')`

* Dataframe object
  * Pandas 자료형태 : DF - 2차원 구조
    1. row index
    2. column header
  * dict 자료형은 dataframe로 변환 가능

* Address
  1. loc : label based, 숫자 또는 헤더라벨로 접근 (ex.`df.loc[0, 'Artist']`)
  2. iloc : integer based, 숫자로만 접근 (ex. `df.iloc[0:2, 0:3]`)

~~~Pandas
# Useful example

# Artist 열의 값을 중복 없는 형태로 반환
df['Artist'].unique  

# 해당 열만 모은 new_df 신규 생성
new_df = df[['Artist', 'Albumyear', ...]]


# Albumyer 열을 조건에 맞춰 boolean 형태로 반환
df['Albumyear'] >= 1980  
# 해당 조건 만족하는 row만 추출하여 new_df 신규 생성
new_df = df[df['Albumyear'] > 1980]

~~~

### 4.4 Numpy

[Jupyter Notebook - Numpy1D][ipynb-4-5-1]   
[Jupyter Notebook - Numpy2D][ipynb-4-5-2]   

* import: `import numpy as np`
* creation: `np.array(LIST)`  # list를 numpy.ndarray 객체로 변환

* Useful fuction
  * `np.pi` : PI값 반환
  * `np.sin(ARRAY)` : array 개별값을 sin 변환
  * `np.linespace(a, b, num = k)`  # a부터 b까지 k개의 간격으로 array 생성

* Array attributes
  * `.dtype` : array 내부 데이터 타입 (ex. int32, float64...)
  * `.size` : array 내부 데이터 갯수
  * `.ndim` : array dimension. 정수값 (1, 2, ...)
  * `.shape` : row/column 갯수 (n, m)

* Array methods
  * `.mean()`, `.std()`, `.max()`, `.min()`
  * `.T` : transpose

* Slicing & Accessing : 아래 2가지 모두 동일한 결과
  1. A[n, m]
  2. A[n][m]

* Array calculation
  1. Addition : `A + B`
    * Add constant : `A + n`
  2. Multiplication : `n * A`
  3. Product : `A * B` --> 같은 행열 값끼리 곱
  4. **Dot product** : `np.dot(A, B)`

> 1d-array는 vector로, 2d-array는 matrix로 이해 가능

### 4.5 Simple API - Application Programming Interface

[Jupyter Notebook - Simple API][ipynb-4-5-3]  

> Your program  --- **API** (input) ---> Software component   
> Your program  <-- Data (output) -- Software component   

* API : **A**pplication **P**rogramming **I**nterface
  * An API lets two pieces of software talk to each other.
  * Pandas library도 API로 볼 수 있음
* REST APIs : **RE**presentational **S**tate **T**ransfer
  * http 기반으로 필요한 자원에 접근하는 방식의 아키텍쳐

### 4.6 Overview of HTTP

[Jupyter Notebook - Requests HTTP][ipynb-4-5-4]  

> Client -- **Request** --> Web server   
> Client <-- **Response** -- Web server

* URL : **U**niform **R**esource **L**ocator
  1. Scheme : `https://`
  2. Base URL (internet address) : `jamescbjeon.github.io/`
  3. Route : `markdown/2020/10/19/ibm4-python-for-ds-n-ai.html`

* Requests
  * Server에 필요한 정보를 요청
    * HTTP method에 의해서 필요한 Response를 얻을 수 있음
  * Request message : Startline, Header

| HTTP method | Description                    |
| ----------- | ------------------------------ |
| GET         | Retrieves data from server     |
| POST        | Submits data to server         |
| PUT         | Updates data already on server |
| DELETE      | Deletes data from server       |

* Response
  * Request에 의해 수행 후 server에서 전송된 결과 데이터
  * Response message : Startline, Header, Body
    * Status code
      * 200 OK
      * 401 Unauthorized, 403 Forbidden, 404 Not found

~~~Python
# Python에서 requests library 사용 예

>> import requests

>> url = 'https://www.ibm.com/'
>> r = requests.get(url)  # resonponse 객체를 생성

>> r.status_code  
  200                # response 확인. 양호.
>>> r.headers
  {'Date': ..., ...}  # response header 정보 확인
>>> r.headers['Content-Type']
  'application/json'
>>> r.json()    # json을 다루는 method
  {'args':..., }
~~~

***

## 5. Final Project - Analyzing US Economic Data and Building a Dashboard

[Jupyter Notebook - Final Assignment][ipynb-4-final]


[coursera-ibm-ds]: https://www.coursera.org/professional-certificates/ibm-data-science
[coursera-ibm-ds-4]: https://www.coursera.org/learn/python-for-applied-data-science-ai?specialization=ibm-data-science

[ibm1]: https://jamescbjeon.github.io/ibmdatascience/2020/09/29/ibm1-what-is-data-science.html
[ibm2]: https://jamescbjeon.github.io/ibmdatascience/2020/10/05/ibm2-tools-for-data-science.html
[ibm3]: https://jamescbjeon.github.io/ibmdatascience/2020/10/12/ibm3-data-science-methodology.html
[ibm4]: https://jamescbjeon.github.io/ibmdatascience/2020/10/19/ibm4-python-for-ds-n-ai.html
[ibm5]: https://jamescbjeon.github.io/ibmdatascience/2020/10/26/ibm5-databases-n-sql-for-data-science.html
[ibm6]: https://jamescbjeon.github.io/ibmdatascience/2020/11/03/ibm6-data-analysis-with-python.html
[ibm7]: https://jamescbjeon.github.io/ibmdatascience/2020/11/07/ibm7-data-visualization-with-python.html
[ibm8]: https://jamescbjeon.github.io/ibmdatascience/2020/11/10/ibm8-machine-learning-with-python.html
[ibm9]: https://jamescbjeon.github.io/ibmdatascience/2020/11/17/ibm9-applied-data-science-capstone.html

[cheat-sheet-python27]: http://www.astro.up.pt/~sousasag/Python_For_Astronomers/Python_qr.pdf
[multiple-arg]: https://brunch.co.kr/@princox/180
[doc-python-exception]: https://docs.python.org/3/library/exceptions.html

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
[ipynb-4-3-5]: https://github.com/jamescbjeon/ibmDS/blob/master/4/3-1.2ExcecptionHandling.ipynb
[ipynb-4-4-1]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-4-1-ReadFile.ipynb
[ipynb-4-4-2]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-4-2-WriteFile.ipynb
[ipynb-4-5-1]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-5-1-Numpy1D.ipynb
[ipynb-4-5-2]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-5-2-Numpy2D.ipynb
[ipynb-4-5-3]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-5.1_Intro_API.ipynb
[ipynb-4-5-4]: https://github.com/jamescbjeon/ibmDS/blob/master/4/PY0101EN-5.3_Requests_HTTP.ipynb
[ipynb-4-final]: https://github.com/jamescbjeon/ibmDS/blob/master/4/test_notebook_final.ipynb
