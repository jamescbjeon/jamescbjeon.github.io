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


***

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
  * `df.dtypes` : 각 열 변수의 type을 반환
  * `df.shape` : 행 x 열의 크기를 반환
  * `df.describes()` : 각 열의 통계값을 반환 (max, min, ...)
    * `df.describes(include="all")` : numeric 하지 않은 열도 포함
  * `df.info()` : 요약본 제공

* Missing value handling
  1. `df.replace('?', np.NaN)` : ?로 지정된 값을 NaN으로 변경
  2. `df.dropna(subset=['COL_NAME'], axis=0)`
    * `dropna`는 결측값 제외 명령
    * 선정된 열에서 결측값 확인
    * axis = 0 해당 행 삭제, axis = 1 해당 열 삭제

* Accessing database with Python
  * Pyton DB API
    1. Connection object
      * Database connections
      * Manage Transaction
    2. Cursor object
      * Database queries

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

***

## 2 Preprocessing Data in Python

[Jupyter Notebook - Wrangling][ipynb-6-5-2]

* Preprocessing data
  1. Identify and handle missing Values
  1. Data formatting
  1. Data normalization : centering & scaling
  1. Data binning
  1. Turn categorical values to numeric values

1. Identify and handle missing Values
  1. Check with the data collection **source**
  2. **Drop** missing values
    * `df.dropna(subset=['COL_NAME'], axis=)`
      * axis : '0' drop entire row, '1' drop entire column
      * subset : 해당 열에서 검색
  3. **Replace**
    * `df.replace(MISSING_VALUE, NEW_VALUE)`
  4. **Leave it** as a missing values
    * 결측치를 검사할 Filter DF 생성
      1. `df.isnull()` : df 전체에 대해 결측 유무를 bool df로 반환
      1. `df.notnull()` : `.isnull()`과 반대 결과를 bool df로 반환

~~~Python
# 예제 - 해당 열의 평균값으로 결측치를 대체
mean = df['normalized-losses'].mean()
df['normalized-losses'].replace(na.NaN, mean)

# 예제 - 각 열의 결측값을 count하여 확인
missing_data = df.isnull()
for col in missing_data.columns.values.tolist():
  print(col)
  print(missing_data[col]).value_counts())
  print(" ")
~~~

2. Data formatting
  1. 서로 다른 이름을 통일 : ex. 'N.Y', 'New Your', 'NY' --> 'New York'
  2. Apply calculation to an entire columns : 열별로 전체 계산 후 대체
  3. Data type cleaing
    1. Type 확인 : `df.dtype()`
    2. Type 변경 : `df.astype()`

~~~Python
# 예제 - Mile/gal을 L/100km로 계산 후 열 이름 변경
df['city-mpg'] = 235/df['city-mpg']
df.rename(columns = {'city-mpg':'city-L/100km'}, inplace=True)

# 예제 - 'price' 열을 int type으로 변경
df['price'] = df['price'].astype('int')
~~~

3. Data normalization : centering & scaling
  1. Simple feature scaling : New = Old / Max
  2. Min - max : New = (Old-Min) / (Max-Min)
  3. Z-score : New = (Old - Mean) / Std --> 보통 +/-3 이내로 수렴

4. Data binning
  * 값들을 Grouping하여 몇 개의 **Bin**에 나누는 것

~~~Python
# 예제 - 'price' 열의 값을 세 개의 라벨로 나눈 새로운 열을 생성
bins = np.linspace(min(df['price']), max(df['price']), 4)
group_names = ['low, 'medium', 'high']
df['price-binned'] = pd.cut(df['price'], bins, label=group_names, include-lowest=True)
~~~

5. Categorical variables into quantitative variables : **One-hot encoding**
  * `pd.get_dummies(df['COL_NAME'])`
    * 개별 카테고리 별로 Dummy variable 생성 --> 0 또는 1을 할당


***

## 3 Exploratory Data Analysis

[Jupyter Notebook - EDA][ipynb-6-5-3]


0. Simple Visualization
  1. Scatter plot
    * x-axis : predictor, independent variables   
      y-axis : target, dependent variables
    * Continuous variables에 대해 확인
    * `sns.regplot(x='COL_NAME', y='COL_NAME', data=df)`
  2. Box plot
    * Categorical variables에 대해 확인
    * `sns.boxplot(x='COL_NAME', y='COL_NAME', data=df)`

1. Descriptive statistics (기술 통계량)
  * EDA 실시 전 데이터 요약정보로 통찰을 얻을 수 있음
  * `df.decribe()` : 개별 열에 대한 기초 통계 정보 확인
  * `df.value_counts()` : `.to_frame()`, `to_list()`
    * Series에만 적용 가능. df에는 적용되지 않음

2. GroupBy
  * `df.groupby(['Target_COL1, Tar...'], as_index=False).mean()`   
    : 대상 열로 할당된 기술통계량의 정보를 정리하여 반환
  * `df.pivot(index='COL_NAME1', columns='COL_NAME2')`   
    : groupby 결과에 대해 pivot 분리하여 반환

3. Correlation
  * What extent different variables are independent each ohter
  * **Correlation doen not imply causation.**

4. Correlation - statistics
  * Pearson Correlation
    1. Correlation efficient
      * Close to +1 : Strong positive relationship
      * 0 : No relationship
      * Close to -1 : Strong negative relationship
    2. P-value
      * < 0.001 Strong certainty in the result
      * < 0.05 Moderate certainty in the result
      * < 0.1 Weak certainty in the result
      * > 0.1 No certainty
  * `df.corr()`
    * xy축에 각 varibles를 할당 후 상관관계 도표를 반환

~~~Python
# 예제 - Pearson correlation
p_coef, p_value = stats.pearsonr(df['horsepower'], df['price'])
~~~

5. ANOVA - ANalysis Of VariAnce
  * Finding correlation between different groups of a categorical variable.
  1. F-score : 표본그룹 평균을 표본그룹 내 분산에 따라 나눈 값 사이의 분산
  2. p-value : Confidence degree

> F-score가 크고, p-value가 작을 수록 해당 분류가 변수에 연관됨을 의미

***

## 4 Model Development

[Jupyter Notebook - Model dev][ipynb-6-5-4]

1. Simple and Multiple Linear Regression
2. Model Evaluation using Visualization
3. Polynomial Regression & Pipelines
4. R-squared and MSE for In-sample Evaluation
5. Prediction and Decision Making

> Model Development   
> : Independent variables & features --- **Model** (mathematical equation) ---> Dependent variables (desired prediction)   
> : More relavant data ==> More accurated result



***

## 5 Model Evaluation

[Jupyter Notebook - Model eval][ipynb-6-5-5]


***

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
