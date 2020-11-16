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

* Column & Row 목록 접근
  * `df.columns`, `df.index` : Pandas index 객체로 반환
  * `df.columns.tolist()`, `df.index.tolist()` : List 형태로 변경. `.toframe()`도 가능

* Column selection
  1. `df.COL_NAME` : 'series' 반환. 열 이름에 공백이나 특수문자가 있으면 안 됨
  1. `df['COL_NAME']` : 'series' 반환. 열 이름 제한 없음
  1. `df[['COL1', 'COL2', ...]]` : 'dataframe' 반환

* Row and cell selection
  1. `df.loc[LABLE]` : Filters by lables of index/column (라벨로 접근)
  1. `df.iloc[INDEX]` : Filters by positions of index/column (위치로 접근)

* Data manipulation examples
  * 열 목록이 모두 string인지 확인: `all(isinstance(column, str) for column in df.columns)`
  * 현재 열 목록을 모두 string으로 치환 : `df.columns = list(map(str, df.columns))`
  * 특정 열을 index로 지정 : `df_can.set_index('Country', inplace=True)`
  * 행 index를 리셋 : `df_tot.reset_index(inplace = True)`
  * 필터로 사용할 목록을 생성 : `years = list(map(str, range(1980, 2014)))`
  * 그래프 생성을 위해 행-열 변환 : `df_top5 = df_top5[years].transpose()`

***

## 1 Introduction to Data Visualization

[Jupyter Notebook - Import][ipynb-7-1]

### 1.1 Data visualization

* Why build visuals?
  1. For exploratory data analysis
  1. Communicate data clearly
  1. Share unbiased representation of data
  1. Use them to support recommendations to different stakeholders

> [Data Looks Better Naked](https://www.darkhorseanalytics.com/blog/salvaging-the-pie) - Less is better!

* Main libraries
  1. matplotlib
  1. seaborn
  1. folium

### 1.2 Matplotlib Architecture

| No | Layer     | Library   |
| -- | --------- | --------- |
| 1  | Scripting | Pyplot    |
| 2  | Artist    | Artist    |
| 3  | Backend   | Figure canvas, Renderer, Event |

### 1.3 Matplotlib Example

* Magic function
  * `%matplotlib inline`
  * `%matplotlib notebook` : 한 번 그려진 plot도 변경 가능

~~~Python
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
haiti.plot(kind='line')  # df.plot()으로 간단하게 그래프 생성. kind parameter로 그래프 종류 선정

plt.title('Immigration from Haiti')
plt.ylabel('Number of immigrants')
plt.xlabel('Years')
plt.text(2000, 6000, '2010 Earthquake')  # (2000, 6000) 위치에 해당 텍스트 삽입

plt.show()  # 그래프 생성
~~~

***

## 2 Basic Visualization tools

### 2.1 Area plot

* [Area plot](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.area.html)
  * kind = 'area'
  * stacked = True or False
  * alpha = 0 to 1, Transparency

~~~Python
df_top5.plot(kind='area',
             alpha=0.25, # 0-1, default value a= 0.5
             stacked=False,
             figsize=(20, 10),
            )

plt.title('Immigration Trend of Top 5 Countries')
plt.ylabel('Number of Immigrants')
plt.xlabel('Years')

plt.show()
~~~

### 2.2 Using artist layer

* `plt` (= `matplotlib.pyplot`) : Script layer에서 작업
* `ax` 객체를 생성하여 현재 그래프를 할당하고, method를 호출하여 속성을 변경 가능 : Artist layer에서 작업 (preferred)

~~~Python
ax = df_top5.plot(kind='area', alpha=0.35, figsize=(20, 10))

ax.set_title('Immigration Trend of Top 5 Countries')
ax.set_ylabel('Number of Immigrants')
ax.set_xlabel('Years')
~~~

### 2.3 Histograms

~~~Python
count, bin_edges = np.histogram(df_t, 15)  # xtick에 사용할 array 생성
xmin = bin_edges[0] - 10   #  graph min에 사용할 값 생성
xmax = bin_edges[-1] + 10  #  graph max에 사용할 값 생성

# stacked Histogram
df_t.plot(kind='hist',
          figsize=(10, 6),
          bins=15,
          xticks=bin_edges,
          color=['coral', 'darkslateblue', 'mediumseagreen'],
          stacked=True,
          xlim=(xmin, xmax)
         )
~~~

### 2.4 Bar chart

~~~Python
df_iceland.plot(kind='bar', figsize=(10, 6))
~~~

~~~Python
df_top15.plot(kind='barh', figsize=(12, 12), color='steelblue')
~~~

### 2.5 [Annotate](https://matplotlib.org/3.3.2/api/_as_gen/matplotlib.pyplot.annotate.html) (주석 처리)

~~~Python
# Annotate arrow
df_iceland.plot(kind='bar', figsize=(10, 6))

plt.annotate('',                      # s: str. will leave it blank for no text
             xy=(32, 70),             # place head of the arrow at point (year 2012 , pop 70)
             xytext=(28, 20),         # place base of the arrow at point (year 2008 , pop 20)
             xycoords='data',         # will use the coordinate system of the object being annotated
             arrowprops=dict(arrowstyle='->', connectionstyle='arc3', color='blue', lw=2)
            )

# Annotate Text
plt.annotate('2008 - 2011 Financial Crisis', # text to display
             xy=(28, 30),                    # start the text at at point (year 2008 , pop 30)
             rotation=72.5,                  # based on trial and error to match the arrow
             va='bottom',                    # want the text to be vertically 'bottom' aligned
             ha='left',                      # want the text to be horizontally 'left' algned.
            )

plt.show()
~~~

~~~Python
df_top15.plot(kind='barh', figsize=(12, 12), color='steelblue')

# Barh plot 끝에 label 표시
for index, value in enumerate(df_top15):
    label = format(int(value), ',') # format int with commas    
    plt.annotate(label, xy=(value - 47000, index - 0.10), color='white')

plt.show()
~~~

***

## 3 Specialized Visualization Tools


***

## 4 Advanced Visualization Tools


***

## 5 Visualizing Geospatial Data


***

## 6 Final Assignment

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
