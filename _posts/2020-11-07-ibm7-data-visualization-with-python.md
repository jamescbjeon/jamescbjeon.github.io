---
layout: post
title: Data Visualization with Python
subtitle: Course summary - IBM Data Science Professinal 7
categories: StudyNote
tags: [Data Science, Coursera, IBM, Python, 정리노트]
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

### 0.1 Column and row selection

1. Column and index
  * `df.columns`, `df.index` : 열과 행을 Pandas index object로 반환
    * `df.columns.tolist()`, `df.index.tolist()` : Index object를 List로 변경. `.toframe()`으로 pandas frame으로도 변환 가능
2. Column selection
  1. `df.COL_NAME` : 'series' 반환. 열 이름에 공백이나 특수문자가 있으면 안 됨
  1. `df['COL_NAME']` : 'series' 반환. 열 이름 제한 없음
  1. `df[['COL1', 'COL2', ...]]` : 'dataframe' 반환
3. Row selection
  1. `df.loc[LABLE]` : Filters by lables of index/column (라벨로 접근)
  1. `df.iloc[INDEX]` : Filters by positions of index/column (위치로 접근)

### 0.2 Data manipulation

* String
  * 열 목록이 모두 string인지 확인: `all(isinstance(column, str) for column in df.columns)`
  * 현재 열 목록을 모두 string으로 치환 : `df.columns = list(map(str, df.columns))`
  * 필터로 사용할 목록을 생성 : `years = list(map(str, range(1980, 2014)))`

* Index set/reset
  * 특정 열을 index로 지정 : `df_can.set_index('Country', inplace=True)`
  * 행 index를 리셋 : `df_tot.reset_index(inplace = True)`

* Transpose
  * 그래프 생성을 위해 행-열 변환 : `df_top5 = df_top5[years].transpose()`

### 0.3 Groupby

  1. Split : Data --> Into group by criteria
  2. Apply : Applying a function to each group independently:
    * `.sum()`, `.count()`, `.mean() `, `.std()`, `.aggregate()`, `.apply()`, ...
  3. Combine : Combining the results into a data structure

~~~Python
# group countries by continents and apply sum() function
df_continents = df_can.groupby('Continent', axis=0).sum()

# note: the output of the groupby method is a `groupby' object.
print(type(df_can.groupby('Continent', axis=0)))

~~~

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

### 3.1 Pie charts

* Parameters
  * `autopct` : percentages 표기 방법
  * `startangle` : Pie chart 시작 위치를 counterclockwise로 회전
  * `shadow`
  * `labels` : label 표기 여부
  * `Explode` : 해당 항목은 살짝 밖으로 배치 (강조)
  * `legent` : 범례 표기

~~~Python
colors_list = ['gold', 'yellowgreen', 'lightcoral', 'lightskyblue', 'lightgreen', 'pink']
explode_list = [0.1, 0, 0, 0, 0.1, 0.1] # ratio for each continent with which to offset each wedge.

df_continents['Total'].plot(kind='pie',
                            figsize=(15, 6),
                            autopct='%1.1f%%',   # add in percentages
                            startangle=90,       # start angle 90° (Africa)
                            shadow=True,         # add shadow
                            labels=None,         # turn off labels on pie chart
                            pctdistance=1.12,    # the ratio between the center of each pie slice and the start of the text generated by autopct
                            colors=colors_list,  # add custom colors
                            explode=explode_list # 'explode' lowest 3 continents
                            )

plt.legend(labels=df_continents.index, loc='upper left')
~~~

### 3.2 Box plots

* Statistical meaning
  * Minimum: Smallest number in the dataset
  * 1st quartile: Middle number between the minimum and the median
  * **Median** (2nd quartile): Middle number of the (sorted) dataset
  * 3rd quartile: Middle number between median and maximum
  * Maximum: Highest number in the dataset
  * IQR (Interquartile range) : Q1-Q3, distance between the upper and lower quartiles

~~~Python
df_CI.plot(kind = 'box', figsize = (10, 7))

# horizontal box plots
df_CI.plot(kind='box', figsize=(10, 4), color='blue', vert=False)
~~~

### 3.3 Scatter plots

~~~Python
df_tot.plot(kind='scatter', x='year', y='total', figsize=(10, 6), color='darkblue')
~~~

~~~Python
### Scatter plot에 1d linear regression 추가할 경우,
x = df_tot['year']      # year on x-axis
y = df_tot['total']     # total on y-axis
fit = np.polyfit(x, y, deg=1)

df_tot.plot(kind='scatter', x='year', y='total', figsize=(10, 6), color='darkblue')

# plot line of best fit
plt.plot(x, fit[0] * x + fit[1], color='red') # recall that x is the Years
plt.annotate('y={0:.0f} x + {1:.0f}'.format(fit[0], fit[1]), xy=(2000, 150000))

plt.title('Total Immigration to Canada from 1980 - 2013')
plt.xlabel('Year')
plt.ylabel('Number of Immigrants')

plt.show()

# print out the line of best fit
'No. Immigrants = {0:.0f} * Year + {1:.0f}'.format(fit[0], fit[1])
~~~


### 3.4 Bubble plots

* A variation of the scatter plot that displays three dimensions of data (x, y, z)
  * Data points --> bubbles (x, y)
  * Weight --> size of the bubble (z)

~~~python
# Brazil
ax0 = df_can_t.plot(kind='scatter',
                    x='Year',
                    y='Brazil',
                    figsize=(14, 8),
                    alpha=0.5,                  # transparency
                    color='green',
                    s=norm_brazil * 2000 + 10,  # pass in weights
                    xlim=(1975, 2015)
                   )

# Argentina
ax1 = df_can_t.plot(kind='scatter',
                    x='Year',
                    y='Argentina',
                    alpha=0.5,
                    color="blue",
                    s=norm_argentina * 2000 + 10,
                    ax = ax0
                   )

ax0.set_ylabel('Number of Immigrants')
ax0.set_title('Immigration from Brazil and Argentina from 1980 - 2013')
ax0.legend(['Brazil', 'Argentina'], loc='upper left', fontsize='x-large')
~~~

### 3.5 Subplot

한 장표에 여러 개의 그래프를 Grid 형태로 배치

~~~Python
# Basic Syntax
fig = plt.figure()  # create figure
ax = fig.add_subplot(nrows, ncols, plot_number)  # create subplots

# nrows, ncols : split figure --> (nrows * ncols) sub-axes,
# plot_number : number of grid
~~~

|       | column 1  | column 2  |
| ----- | --------- | --------- |
| row 1 | Subplot 1 | Subplot 2 |
| row 2 | Subplot 3 | Subplot 4 |

***

## 4 Advanced Visualization Tools

### 4.1 Waffle chart

* Waffle chart : 목표까지 성취도 표시할 때 주로 사용. 엑셀 cell을 활용하여 칸칸이 채워가는 형태.


### 4.2 Word cloud

### 4.3 Regression plot - Seaborn

~~~Python
plt.figure(figsize=(15, 10))  # Size 지정

sns.set(font_scale=1.5)  # 그래프 글자 크기
sns.set_style('whitegrid')  # 그래프 배경 스타일

ax = sns.regplot(x='year', y='total', data=df_tot, # 기본 데이터 출처
                  color='green', # 색 지정
                  marker='+', scatter_kws={'s': 200}  # 마커 형태 및 크기
                  )
ax.set(xlabel='Year', ylabel='Total Immigration')  # Artist layer를 통해 축 이름 지정
ax.set_title('Total Immigration to Canada from 1980 - 2013')
~~~


***

## 5 Visualizing Geospatial Data

### 5.1 Introduction to Folium

~~~Python
import folium

world_map = folium.Map(location=[56.130, -106.35], zoom_start=4
                      tiles='Stamen Terrain')  # Tiles option으로 지도 테마 변경 가능
world_map
~~~


### 5.2 Map with Markers

~~~Python
# San Francisco latitude and longitude values
latitude = 37.77
longitude = -122.42

# create map and display it
sanfran_map = folium.Map(location=[latitude, longitude], zoom_start=12)

# loop through the 100 crimes and add each to the map
for lat, lng, label in zip(df_incidents.Y, df_incidents.X, df_incidents.Category):
    folium.features.CircleMarker(
        [lat, lng],
        radius=5, # define how big you want the circle markers to be
        color='yellow',
        fill=True,
        popup=label,
        fill_color='blue',
        fill_opacity=0.6
    ).add_to(sanfran_map)

# show map
sanfran_map
~~~

~~~Python
from folium import plugins

# let's start again with a clean copy of the map of San Francisco
sanfran_map = folium.Map(location = [latitude, longitude], zoom_start = 12)

# instantiate a mark cluster object for the incidents in the dataframe
incidents = plugins.MarkerCluster().add_to(sanfran_map)

# loop through the dataframe and add each data point to the mark cluster
for lat, lng, label, in zip(df_incidents.Y, df_incidents.X, df_incidents.Category):
    folium.Marker(
        location=[lat, lng],
        icon=None,
        popup=label,
    ).add_to(incidents)

# display map
sanfran_map
~~~

### 5.3 Choropleth Maps


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
