---
layout: post
title: IBM6 - Data Analysis with Python
subtitle: Course summary - IBM Data Science Professinal 6
categories: IbmDataScience
tags: [Data Science, Coursera, IBM, Python, EDA, 정리노트]
---

*본 포스트는 [IBM Data Science 특화 과정][coursera-ibm-ds] 중 [6. Data Analysis with Python][coursera-ibm-ds-6]에 대한 정리노트입니다.*

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

[ibm1]: https://jamescbjeon.github.io/studynote/2020/09/29/ibm1-what-is-data-science.html
[ibm2]: https://jamescbjeon.github.io/studynote/2020/10/05/ibm2-tools-for-data-science.html
[ibm3]: https://jamescbjeon.github.io/studynote/2020/10/12/ibm3-data-science-methodology.html
[ibm4]: https://jamescbjeon.github.io/studynote/2020/10/19/ibm4-python-for-ds-n-ai.html
[ibm5]: https://jamescbjeon.github.io/studynote/2020/10/26/ibm5-databases-n-sql-for-data-science.html
[ibm6]: https://jamescbjeon.github.io/studynote/2020/11/03/ibm6-data-analysis-with-python.html
[ibm7]: https://jamescbjeon.github.io/studynote/2020/11/07/ibm7-data-visualization-with-python.html
[ibm8]: https://jamescbjeon.github.io/studynote/2020/11/10/ibm8-machine-learning-with-python.html
[ibm9]: https://jamescbjeon.github.io/studynote/2020/11/17/ibm9-applied-data-science-capstone.html

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

### 1.1 Python Library Packages

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

### 1.2 Data Import/Export

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

### 1.3 Get started

* Overview
  1. `df.head(n)` : 첫 n행 표시 (생략 시, 5행)
  1. `df.tail(n)` : 마지막 n행 표시 (생략 시, 5행)
  1. `df.columns` : Column header 목록을 list 형태로 반환

* Attributes & Descriptive statistics
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

### 1.4 Accessing database with Python

* Python DB API
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

### 2.1 Identify and handle missing Values

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

### 2.2 Data formatting

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

### 2.3 Data normalization : centering & scaling

1. Simple feature scaling : New = Old / Max
2. Min - max : New = (Old-Min) / (Max-Min)
3. Z-score : New = (Old - Mean) / Std --> 보통 +/-3 이내로 수렴

### 2.4 Data binning

값들을 Grouping하여 몇 개의 **Bin**에 나누는 담는 것

~~~Python
# 예제 - 'price' 열의 값을 세 개의 라벨로 나눈 새로운 열을 생성
bins = np.linspace(min(df['price']), max(df['price']), 4)
group_names = ['low, 'medium', 'high']
df['price-binned'] = pd.cut(df['price'], bins, label=group_names, include-lowest=True)
~~~

### 2.5 Categorical variables into quantitative variables : **One-hot encoding**

`pd.get_dummies(df['COL_NAME'])` : 개별 카테고리 별로 Dummy variable 생성 --> 0 또는 1을 할당


***

## 3 Exploratory Data Analysis

[Jupyter Notebook - EDA][ipynb-6-5-3]

### 3.0 Simple Visualization

1. Scatter plot
  * x-axis : predictor, independent variables   
    y-axis : target, dependent variables
  * Continuous variables에 대해 확인
  * `sns.regplot(x='COL_NAME', y='COL_NAME', data=df)`
2. Box plot
  * Categorical variables에 대해 확인
  * `sns.boxplot(x='COL_NAME', y='COL_NAME', data=df)`

### 3.1 Descriptive statistics (기술 통계량)

* EDA 실시 전 데이터 요약정보로 통찰을 얻을 수 있음
* `df.decribe()` : 개별 열에 대한 기초 통계 정보 확인
* `df.value_counts()` : `.to_frame()`, `to_list()`
  * Series에만 적용 가능. df에는 적용되지 않음

### 3.2 GroupBy

* `df.groupby(['Target_COL1, Tar...'], as_index=False).mean()`   
  : 대상 열로 할당된 기술통계량의 정보를 정리하여 반환
* `df.pivot(index='COL_NAME1', columns='COL_NAME2')`   
  : groupby 결과에 대해 pivot 분리하여 반환

### 3.3 Correlation

It measures that what extent different variables are independent each ohter.

> **Correlation doen not imply causation.**

* Pearson Correlation
  1. Correlation efficient
    * Close to +1 : Strong positive relationship
    * 0 : No relationship
    * Close to -1 : Strong negative relationship
  2. P-value
    * < 0.001 Strong certainty in the result
    * < 0.05 Moderate certainty in the result
    * < 0.1 Weak certainty in the result
    * \> 0.1 No certainty
* `df.corr()`
  * xy축에 각 varibles를 할당 후 상관관계 도표를 반환

~~~Python
# 예제 - Pearson correlation
p_coef, p_value = stats.pearsonr(df['horsepower'], df['price'])
~~~

### 3.4 ANOVA - ANalysis Of VariAnce

Finding correlation between different groups of a categorical variable.

1. F-score : 표본그룹 평균을 표본그룹 내 분산에 따라 나눈 값 사이의 분산
2. p-value : Confidence degree

> F-score가 크고, p-value가 작을 수록 해당 분류가 변수에 연관됨을 의미

***

## 4 Model Development

[Jupyter Notebook - Model dev][ipynb-6-5-4]

> Model Development   
> : Independent variables & features --- **Model** (mathematical equation) ---> Dependent variables (desired prediction)   
> : More relavant data ==> More accurated result

### 4.1 Linear Regression - Simple and Multiple

* Linear regression
  1. Simple : X --> Y
    * Y = b0 + aX
    * b0 : intercept (y-shift), a = coef (slope)
  2. Multiple : X1, ..., Xn --> Y
    * Y = b0 + aX = b0 + a1 * X1 + ... + an * Xn

* Fit : 주어진 모델에 데이터를 맞추는 것
  * 결과물로 **coef**, **intercept**를 얻게 됨
  * SLR, MLR에 관계없이 `LinearRegression()` 객체를 사용하며, lm.fit(X, y)도 동일하다. 단, MLR의 경우, X는 n의 열로 구성되어 있으므로 얻어지는 `lm.coef_`도 n개로 주어진다.

~~~Python
### Example - Model fit

from sklearn.linear_model import LinearRegression  # Import library
lm = LinearRegression()  # Create LR object using the consturctor

X = df[['highway=mpg']]  # Define predictor
y = df['price']  # Define target variables

lm = fit(X, y)  # Fit the model
print('y-shift: {}, slope: {}'.format(lm.intercept_, lm.coef_))

Yhat = lm.predict(X, y)  # Obtain prediction. 이 때 Yhat에는 모델에 의해 예측된 신규 Y값 목록이 반환. 즉, Yhat - y간 비교를 통해 모델 정확성을 검증 가능
~~~

* Noise : 예측치가 모델에서 벗어난 정도
  * [Noise] = [Prediction] -[Acual data] = Yhat - Y

### 4.2 Model Evaluation using Visualization

* Regression plot gives us...
  1. Relationship between the variables
  1. Strength of correlation
  1. Direction of relationship (+/-)

~~~Python
### Example - Regression plot

import seaborn as sns

sns.regplot(X = 'highway-mpg', y = 'price', data = df)
plt.ylim(0, )
~~~

* Residual plot : 잔차의 분포를 확인
  * 다음의 경우에는 Model이 실패함을 암시
    * Not randomly spread out
    * Variance appears to change with x-axis

~~~Python
### Example - Residual plot

sns.residplot(X = 'highway-mpg', y = 'price', data = df)
~~~

* Distribution plot : 분포 곡선 - X 변화에 따른 실제와 예측치 사이의 분포를 확인

~~~Python
### Example - Distritubion plot
# 실제 값과 모델 값을 같은 축에 배치하여 비교

ax1 = sns.distplot(df['price], hist=False, color='r', label='Actual value')  # 실제값으로 빨간 분포 곡선 생성
sns.distplot(Yhat, hist=False, color='b', label='Fitted values', ax=ax1)  # 모델을 통한 예측값을 동일한 그래프에 파란 분포 곡선으로 병기
~~~

### 4.3 Polynomial Regression

* 1-D Polynomial regression
  * Y = b0 + a1 * x + ... + an * x^n
  * Quadratic (2차), Cubic (3차), High-order (그 이상)


> Polynoimal regression은 기본적으로 MLR과 처리방식 동일. x, x^2... x^n을 X1, ..., Xn으로 간주하고 MLR 방식으로 모델 생성

~~~Python
# 별도 library 없이 numpy로 처리 가능
f = np.polyfit(x, y, n)  # n차 x에 대해 y를 대상으로 model fitting. 이 때 f는 b0, a1, ..., an을 포함하는 array로 반환
p = np.poly1d(f)  # p는 model fitting과 관련 없음. np.poly1d는 주어진 계수를 가지고 이해하기 쉽게 y = b + aX 형태로 값을 출력.
~~~

* Multivariate polynomial regression
  * Y = b0 + a1X1 + a2X2 + a3X1X2 + a4X^2 + ...

~~~Python
### Example - Multivariate polynomial regression

from sklear.preprocessing import PolynomialFeatures

pr = PolynomialFeatures(degree=2, include_bias=False)  # pr 객체를 생성
Z_pr = pr.fit_transform(Z)  # 여러 열(Xn)을 가진 Z를 Model fitting. 이 때, Z_pr은 해당 모델에서 예측된 값으로 반환.
~~~

### 4.4 Pipelines

> Pipeline은 Preprocssing 절차에 필요한 Model을 하나로 모아서 한번에 처리할 수 있게 함으로 작업 효율을 올려 준다.

~~~Python
### Ex - Pipeline

# Import libraries
from sklearn.preprocessing import StandardScaler
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression
from sklearn.pipeline import Pipeline

# Pipeline constructor에 넣을 parameter를 tuple 형태로 준비
Input = [('scale, StandardScaler()), \
          ('Polynomial', PolynomialFeatures(include_bias=False), \
          ('model', LinearRegression())]

pipe = Pipeline(Input)
pipe.fit(Z, y)
# Z와 y에 대해 Model fit.
# 이 때, 준비된 대로 Pipeline은 Z값을 normalize하고 Polynomial 형태로 변환한 후 Linear regression 모델에 적용한다.

ypipe = pipe.predict(Z, y)  # 모델에 의한 예측값 확보 (yhat)
~~~

### 4.5 R-squared and MSE for In-sample Evaluation

* **MSE** : Mean squared error
* **R-squared** (R^2) : Coefficient of determination
  * % of variation of response variable (y) that is explained by a linear model   
  It indicates how close the data is to the fitted regression line.
  * [R-squared] = 1 - [MSE of regressionline] / [MSE of the average of data]
  * 0에서 1 사이의 값으로 정의

~~~Python
# R-squared : 별도 library 없이 LinearRegression에서 .score() 메서드 제공
lm.fit(X, Y)  # Model fit
lm.score(X, Y)  # R-squred

# MSE : mean_squared_error library 호출
from sklearn.metrics import mean_squared_error
yhat = lm.predict(X, Y)  # 예측값 생성
mean_squared_error(Y, Yhat)  # MSE
~~~

> MSE가 작을 수록, R-squared가 1에 가까울 수록 Model이 실제값을 정확히 예측

### 4.6 Prediction and Decision Making

1. Does the predicted values make sense?
1. Visualization
1. Numerical measures for evaluation
1. Comparing models


***

## 5 Model Evaluation

[Jupyter Notebook - Model eval][ipynb-6-5-5]

### 5.1 Model evaluation and refinement

Train model과 Predict new data는 다른 영역이며, 이를 사전 검증하기 위해 Model evaluation이 필요하다. 기존에 가진 Sample data를 보통 분리하여 R-squared 등을 평가한다.

> In-sample data : Training, ~70%   
> Out-of-sample : Test, ~30%

~~~Python
from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test = train_test_split(x_data, y_data, test_size=0.3, random_state=0)
~~~

#### 5.1.1 Cross validation

Most common out-of-sample evaluation metrics.   
More effective use of data : Each observation is used for train/test.   
- Dataset을 n개의 fold로 나눈 후, 1개는 test/나머지는 train set을 활용하는 validation을 n번 반복

~~~Python
from sklearn.model_selection import cross_val_score
scores = cross_val_score(lr, x_data, y_data, cv=3)  # 결과는 각 fold에 대해 n개 arry로 반환 (이 경우, 3개)

print(scores.mean())  # n개의 R-squared에 대한 평균
print(scores.std())   # n개의 R-squared에 대한 표준편차

yhat = cross_val_predict(lr, x_data, y_data, cv=3)  # Cross valiation을 활용한 예측도 가능
~~~

### 5.2 Overfit, underfit and model selection

1. Fit : Best!
1. **Underfit** : Too simple
1. **Overfit** : Too flex --> Noise에 대해 과하게 Fitting

~~~Python
# Polinomial fit의 각 n-degree에 대해 R^2 계산
Rsqu_test = []
order = [1, 2, 3, 4]

for n in order:
  pr = PolynomialFeatures(degree =n)
  x_train_pr = pr.fit_transform(x_train[['horsepower']])
  x_test_pr = pr.fit_transform(x_test[['horsepower']])
  lr.fit(x_train, y_train)
  Rsqu_test.append(lr.score(x_test_pr, y_test))
~~~


### 5.3 Ridge regression

alpha값에 따라 Regression 결과의 차이가 발생

> Ridge regression 관련 자료   
> * [Ridge regression와 Lasso regression 쉽게 이해하기](https://rk1993.tistory.com/entry/Ridge-regression%EC%99%80-Lasso-regression-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
> * [ISL 6장 - Lasso, Ridge, PCR이해하기](https://godongyoung.github.io/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D/2018/02/07/ISL-Linear-Model-Selection-and-Regularization_ch6.html)

~~~Python
from sklearn.linear_model import Ridge

RidgeModel = Ridge(alpha = 0.1)
RidgeModel.fit(X, y)
Yhat = RidgeModel.predict(X)
~~~

### 5.4 Grid search

Hyper parameter인 alpha 값을 쉽게 찾게 해주는 Grid search

~~~python
from sklearn.model_selection import GridSearchCV

parameters1= [{'alpha': [0.001, 0.1, 1, 10, 100, 1000, 10000, 100000, 100000]}]  # 필요한 alpha를 사전에 할당
RR=Ridge()  # Ridge 객체 생성
Grid1 = GridSearchCV(RR, parameters1, cv=4)  # Ridge 객체와 alpha 후보를 파라미터에 할당
Grid1.fit(x_data[['horsepower', 'curb-weight', 'engine-size', 'highway-mpg']], y_data)

BestRR = Grid1.best_estimator_  # 최적 alpha 도출. 예제에서는 alpha = 10000
BessRR.score  # R-squared 확인
~~~

***

## 6 Final Project - House Sales in King County, USA

[Jupyter Notebook - Final Assignment][ipynb-6-final]


[coursera-ibm-ds]: https://www.coursera.org/professional-certificates/ibm-data-science
[coursera-ibm-ds-6]: https://www.coursera.org/learn/data-analysis-with-ipynb/home/welcome


[ipynb-6-5-1]: https://github.com/jamescbjeon/ibmDS/blob/master/6/DA0101EN-Review-Introduction.ipynb
[ipynb-6-5-2]: https://github.com/jamescbjeon/ibmDS/blob/master/6/DA0101EN-2-Review-Data-Wrangling.ipynb
[ipynb-6-5-3]: https://github.com/jamescbjeon/ibmDS/blob/master/6/DA0101EN-3-Review-Exploratory-Data-Analysis.ipynb
[ipynb-6-5-4]: https://github.com/jamescbjeon/ibmDS/blob/master/6/DA0101EN-4-Review-Model-Development.ipynb
[ipynb-6-5-5]: https://github.com/jamescbjeon/ibmDS/blob/master/6/DA0101EN-5-Review-Model-Evaluation-and-Refinement.ipynb
[ipynb-6-final]: https://github.com/jamescbjeon/ibmDS/blob/master/6/House_Sales_in_King_Count_USA.ipynb
