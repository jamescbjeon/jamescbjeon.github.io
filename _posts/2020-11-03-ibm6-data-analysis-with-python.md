---
layout: post
title: Data Analysis with Python
subtitle: Course summary - IBM Data Science Professinal 6
categories: StudyNote
tags: [Data Sceience, Coursera, IBM, Python, EDA, 정리노트]
---

*본 포스트는 [IBM Data Science 특화 과정][coursera-ibm-ds] 중 [6. Data Analysis with Python][coursera-ibm-ds-6]에 대한 정리노트입니다.*

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


> Jupyter notebook   
* [Importing Data Set][ipynb-6-5-1]
* [Data Wrangling][ipynb-6-5-2]
* [Exploratory Data Analysis][ipynb-6-5-3]
* [Model Development][ipynb-6-5-4]
* [Model Evaluation][ipynb-6-5-5]
* [Final Assignment][ipynb-6-final]


## 1 Importing Data Set

[Jupyter Notebook - Import][ipynb-6-5-1]

* Python Library Packages
  1. Scientifics Computing
    * Pandas : Data structure & tools
    * Numpy : Array & matrix
    * Scipy : Integral, soving differential equation, optimization
  2. Visualization
    * Matplotlib
    * Seaborn
  3. Algorithmic
    * Scikit-learn : Machine learning - Regression, classification, ...
    * Stasmodels : Explore data

* Data Import/Export

| Format | Read              | Save            |
| ------ | ----------------- | --------------- |
| csv    | pd.read_csv(..)   | df.to_csv(..)   |
| json   | pd.read_json(..)  | df.to_json(..)  |
| xlsx   | pd.read_excel(..) | df.to_excel(..) |
| sql    | pd.read_sql(..)   | df.to_sql(..)   |

~~~Python
import pandas as pd
url = 'PATH'
df = pd.read_csv(url, header = None)  # Column header가 없는 경우. Dataframe 객체 생성.
...
path = 'C:/windows/.../NAME.csv'
df.to_csv(path)  # 처리된 df를 csv로 저장
~~~

* Overview
  1. `df.head(n)` : 첫 n행 표시 (생략 시, 5행)
  1. `df.tail(n)` : 마지막 n행 표시 (생략 시, 5행)
  1. `df.columns` : Column header 목록을 list 형태로 반환

* Getting started...
  * `df.dtypes` : 
  * `df.shape` : 
  * `df.describes()` : 
    * `df.describes(include="all")` : 
  * `df.info()` : 


~~~Python
from dbmodule import connect

# Create connect object
connection = connect(‘databasename’, ‘username’, ‘pswd’)

# Create a cursor object
cursor = connection.cursor()

# Run queries
cursor.execute(‘select * from mytable’)
results = cursor.fetchall()

# Free resources
cursor.close()
connection.close()
~~~

## 2 Data Wrangling

[Jupyter Notebook - Wrangling][ipynb-6-5-2]


## 3 Exploratory Data Analysis

[Jupyter Notebook - EDA][ipynb-6-5-3]


## 4 Model Development

[Jupyter Notebook - Model dev][ipynb-6-5-4]


## 5 Model Evaluation

[Jupyter Notebook - Model eval][ipynb-6-5-5]


## 6 Final Project - House Sales in King County, USA

[Jupyter Notebook - Final Assignment][ipynb-6-final]


[coursera-ibm-ds]: https://www.coursera.org/professional-certificates/ibm-data-science
[coursera-ibm-ds-6]: https://www.coursera.org/learn/data-analysis-with-python/home/welcome


[ipynb-6-5-1]: https://github.com/jamescbjeon/ibmDS/blob/master/6/DA0101EN-Review-Introduction.ipynb
[ipynb-6-5-2]: https://github.com/jamescbjeon/ibmDS/blob/master/6/DA0101EN-2-Review-Data-Wrangling.ipynb
[ipynb-6-5-3]: https://github.com/jamescbjeon/ibmDS/blob/master/6/DA0101EN-3-Review-Exploratory-Data-Analysis.ipynb
[ipynb-6-5-4]: https://github.com/jamescbjeon/ibmDS/blob/master/6/DA0101EN-4-Review-Model-Development.ipynb
[ipynb-6-5-5]: https://github.com/jamescbjeon/ibmDS/blob/master/6/DA0101EN-5-Review-Model-Evaluation-and-Refinement.ipynb
[ipynb-6-final]: https://github.com/jamescbjeon/ibmDS/blob/master/6/House_Sales_in_King_Count_USA.ipynb