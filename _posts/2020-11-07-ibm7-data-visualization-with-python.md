---
layout: post
title: Data Visualization with Python
subtitle: Course summary - IBM Data Science Professinal 7
categories: StudyNote
tags: [Data Sceience, Coursera, IBM, Python, 정리노트]
---

*본 포스트는 [IBM Data Science 특화 과정][coursera-ibm-ds] 중 [7. Data Visualization with Python][coursera-ibm-ds-7]에 대한 정리노트입니다.*

> IBM Data Science 전문가 과정 : 정리노트
  1. [What is Data Science?][ibm1]
  1. [Tools for Data Science][ibm2]
  1. [Data Science Methodology][ibm3]
  1. [Python for Data Science and AI][ibm4]
  1. [Databases and SQL for Data Science][ibm5]
  1. [Data Analysis with Python][ibm6]
  1. [Data Visualization with Python][ibm7]
  1. [Machine Learning with Python][ibm8]
  1. [Applied Data Science Capstone][ibm9]

> Jupyter notebook
  * [Introduction to Data Visualization][ipynb-7-1]
  * [Basic Visualization tools][ipynb-7-2]
  * [Specialized Visualization Tools][ipynb-7-3]
  * [Advanced Visualization Tools][ipynb-7-4]
  * [Visualizing Geospatial Data][ipynb-7-5]
  * [Final Assignment][ipynb-7-6]

***

## 0 Exploring datasets with Pandas

* Column & Row 반환
  * `df.columns`, `df.index` : Pandas index 객체로 반환
  * `df.columns.tolist()`, `df.index.tolist()` : List 형태로 변경. `.toframe()`도 가능

* Select Column
  1. `df.COL_NAME` : 'series' 반환. 열 이름에 공백이나 특수문자가 있으면 안 됨
  1. `df['COL_NAME']` : 'series' 반환. 열 이름 제한 없음
  1. `df[['COL1', 'COL2', ...]]` : 'dataframe' 반환

* Select Row
  1. `df.loc[LABLE]` : Filters by lables of index/column (라벨로 접근)
  1. `df.iloc[INDEX]` : Filters by positions of index/column (위치로 접근)


***

## 1 Introduction to Data Visualization

[Jupyter Notebook - Import][ipynb-7-1]

* Whay build visuals?
  1. For exploratory data analysis
  1. Communicate data clearly
  1. Share unbiased representation of data
  1. Use them to support recommendations to different stakeholders

> Good example - [Data Looks Better Naked](https://www.darkhorseanalytics.com/blog/salvaging-the-pie)

* Visualization - Main library
  1. matplotlib
  1. seaborn
  1. folium


* Matplotlib architecture

| No | Layer     | Library   |
| -- | --------- | --------- |
| 1  | Scripting | Pyplot    |
| 2  | Artist    | Artist    |
| 3  | Backend   | Figure canvas, Renderer, Event |

* Magic function
  * `%matplotlib inline`
  * `%matplotlib notebook` : 한 번 그려진 plot도 변경 가능

~~~Python
### Matplotlib import
%matplotlib inline   # Using inline backend

import matplotlib as mpl
import matplotlib.pyplot as plt

### 사용 스타일
print(plt.style.available)  # 가능 스타일 인쇄
mpl.style.use(['ggplot'])  # 'ggplot' 사용 선정
~~~

~~~Python
### Example
haiti.index = haiti.index.map(int)  # haiti df의 index를 int로 변경
haiti.plot(kind='line')  # line 그래프 생성

plt.title('Immigration from Haiti')
plt.ylabel('Number of immigrants')
plt.xlabel('Years')
plt.text(2000, 6000, '2010 Earthquake')  # (2000, 6000) 위치에 해당 텍스트 삽입

plt.show()  # 그래프 생성
~~~

***

### 2 Basic Visualization tools


***

### 3 Specialized Visualization Tools


***

### 4 Advanced Visualization Tools


***

### 5 Visualizing Geospatial Data


***

### 6 Final Assignment

[coursera-ibm-ds]: https://www.coursera.org/professional-certificates/ibm-data-science
[coursera-ibm-ds-7]: https://www.coursera.org/learn/python-for-data-visualization/home/welcome

[ibm1]: https://jamescbjeon.github.io/studynote/2020/09/29/ibm1-what-is-data-science.html
[ibm2]: https://jamescbjeon.github.io/studynote/2020/10/05/ibm2-tools-for-data-science.html
[ibm3]: https://jamescbjeon.github.io/studynote/2020/10/12/ibm3-data-science-methodology.html
[ibm4]: https://jamescbjeon.github.io/studynote/2020/10/19/ibm4-python-for-ds-n-ai.html
[ibm5]: https://jamescbjeon.github.io/studynote/2020/10/26/ibm5-databases-n-sql-for-data-science.html
[ibm6]: https://jamescbjeon.github.io/studynote/2020/11/03/ibm6-data-analysis-with-python.html
[ibm7]: https://jamescbjeon.github.io/studynote/2020/11/07/ibm7-data-visualization-with-python.html
[ibm8]: https://jamescbjeon.github.io/studynote/2020/11/10/ibm8-machine-learning-with-python.html
[ibm9]: https://jamescbjeon.github.io/studynote/2020/11/17/ibm9-applied-data-science-capstone.html

[ipynb-7-1]: https://github.com/jamescbjeon/ibmDS/blob/master/7/DV0101EN-1-1-1-Introduction-to-Matplotlib-and-Line-Plots.ipynb
[ipynb-7-2]: https://github.com/jamescbjeon/ibmDS/blob/master/7/DV0101EN-2-2-1-Area-Plots-Histograms-and-Bar-Charts-py-v2.0.ipynb
[ipynb-7-3]: https://github.com/jamescbjeon/ibmDS/blob/master/7/DV0101EN-2-3-1-Pie-Charts-Box-Plots-Scatter-Plots-and-Bubble-Plots-py-v2.0.ipynb
[ipynb-7-4]: https://github.com/jamescbjeon/ibmDS/blob/master/7/DV0101EN-3-4-1-Waffle-Charts-Word-Clouds-and-Regression-Plots-py-v2.0.ipynb
[ipynb-7-5]: https://github.com/jamescbjeon/ibmDS/blob/master/7/DV0101EN-3-5-1-Generating-Maps-in-Python-py-v2.0.ipynb
[ipynb-7-6]: https://github.com/jamescbjeon/ibmDS/blob/master/7/.ipynb
