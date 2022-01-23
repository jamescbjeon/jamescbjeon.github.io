---
layout: post
title: Python pandas Q&A video series by Data School
subtitle: YouTube Tutorial by Kevin Markham
categories: Pandas
tags: [Data Science, Pandas, 정리노트]
---

> [IBM Data Science Specilization](https://www.coursera.org/professional-certificates/ibm-data-science)를 수료하고 나니, 이 분야가 이런 일련의 작업들이 필요하고 내가 어떤 부분을 보완 해야겠다는 대강의 감이 잡히는 듯 하다. 다음 수업을 수강하기에 앞서 필요한 Skill은 확실히 익혀야 겠다는 생각에 Tutorial이나 Tip을 찾아 보고 있는데 아래 YouTube 강좌가 상당히 유익했다.

* DataSchool - [Python pandas Q&A video series](https://youtube.com/playlist?list=PL5-da3qGB5ICCsgW1MxlZ0Hq8LL5U3u9y)
    * Instructor : [Kevin Markham](https://github.com/justmarkham)
    * [Jupyter Notebook](https://github.com/justmarkham/pandas-videos/blob/master/pandas.ipynb)

## 1 Data load

### 1.1 Read a tabular data file into pandas

소스의 형식에 맞춰 `pd.read_` 사용

* Source data는 2-dimension으로 정렬되어 있어야만 함
* `pd.read_table`
    * `sep=` Separator 명시 가능
    * `header= ` None으로 지정 시, 열 순서에 따라 정수 할당
    * `skiprows=`, `skipfooter=` 데이터에 불필요한 코멘트를 제외 가능

### 1.2 Select from a DataFrame

* DataFrame에서 Series를 반환하는 방법
   1. `df['COL_NAME']`
   2. `df.COL_NAME`   
      * pandas는 열 이름을 attribute로 보관   
      * 빈 칸이 있는 경우, 사용 불가   
      * 기존 할당된 명령어가 있는 경우, 명령어가 우선 작용

* Series + Series = String이 합쳐진 것과 동일하게 Series 반환
* 신규 열을 생성 시, Bracket notation만 가능

### 1.3 Create DataFrame

1. Dictionary : key --> colname, value --> value
2. List of lists : list 순서대로 stacked (즉, 모든 list의 길이가 동일해야 누락이 없음)
3. Numpy array : list와 동일

```Python
# Create and Export DataFrame   
: `pd.DataFrame({'PassengerId': test.PassengerId, 'Survived':new_pred_class}).set_index('PassengerId').to_csv('sub.csv')`

# dict로 {'열이름1':'데이터1', ...}로 명시. Series, Array, List에 관계 없이 Pandas가 알아서 처리 (!)
# 열 순서 보장을 위해 `.set_index()`로  지정 가능
``` 

* Columns, index는 별도 지정여부 확인할 것
* Series도 동일하게 생성 가능 : `pd.Series()`
* `pd.concat()` 수행 시, colname 및 index에 따라 정렬되므로 사전 확인할 것
* Pickle 
    * Pandas에서 제공하는 파일 타입. DataFrame 내 Python object를 현재 그대로 Export/Import 가능   
    : `train.to_pickle('train.pkl')`, `pd.read_pickle('train.pkl')`

### 1.4 Fast way to read - Read only few columns or rows

```Python
ufo = pd.read_csv('http://bit.ly/uforeports', usecols=[0, 4])
ufo = pd.read_csv('http://bit.ly/uforeports', nrows=3)
```

### 1.5 Methods and attritubes

1. Methods --> parentheses : **행동**. 괄호 안에 세부 행동 방법 지정 (arguments)
2. Attributes --> NO parentheses : **특성**. 이미 결정된 값. 반환값 변경 불가

* DataFrame/Series 뒤에 dot을 붙이고 `TAB` 누르면 호출 가능 methods/attributes 확인 가능
* Parentheses 안에서 `Shift + TAB` 누르면 Doc string 확인 가능 (클릭 횟수에 따라 변화)
    1. Short doc string
    2. Long doc string
    3. Window 유지 시간 증가 (Click +10초)
    4. 별도 창 분리

## 2 Preparation

### 2.1 Rename columns

1. `df.rename(columns= {'OLD_NAME1':'NEW_NAME1', ...}, inplace= True)`
2. `df.columns = LIST` : 사전 준비한 list로 열 이름 치환
3. `pd.read_csv('FILE_NAME', names=LIST, header=0)` : 2번과 동일. 호출할 때 사전 지정

* `df.columns` : DataFrame의 열이름을 Index object로 반환
* 이름을 규칙에 따라 변경하고 싶을 때,
    * `df.columns = df.columns.str.replace(' ', '_')`
        * Index obj를 String 형태로 변환 한 후 .repalce 사용

### 2.2 Remove columns or rows

`df.drop(LABEL, axis= , inplace= True)`   

1. LABEL: 열 혹은 행 이름. 여러 개인 경우, LIST로 작성
2. axis: row-direction 0, column-direction 1

### 2.3 Missing values

1. `.isnull()`
    * `.isnull()`, `.isna()`: NaN 여부를 확인해서 True/False 형태로 DataFrame 반환
        * `.notnull()`, `.notna()`
    * `.isna().sum()`: axis=0, 즉 매 열마다 na갯수를 합하여 반환
    * `df[df.Series.isna()]`: 해당 열의 값이 na인 행만을 DataFrame 형태로 반환

1. `.dropna()`
    * 'how=any': NaN이 한 개라도 있는 행은 모두 drop 
    * 'how=all': 모든 값이 NaN인 열만 drop
    * 'subset=[]': 해당 열에서만 NaN drop
1. `.fillna()`
    * 'value=': NaN을 해당 값으로 치환

### 2.4 Drop non-numeric column

df.select_dtypes(include=[np.number]).dtypes

### 2.5 Duplicates

`.duplicated()` : 중복 값 확인 후, True/False 반환   

`.drop_duplicates()` : 중복 값 확인 후, True 행을 drop

* `keep=`   
    1. `first` : 첫 번째 값은 제외 (False). 이후부터 중복 (True)   
    1. `last` : 마지막 값은 제외 (False). 이전 값은 중복 (True)   
    1. `False` : 제외 없이 모두 중복 (True)   
* `subset=`   
    * 지정된 열에 대해 duplicate 확인 --> 결과는 index에 대한 True/Fase Series로 반환

~~~Python
# 사용 예시
users.loc[users.duplicated(keep='last'), :]
users.drop_duplicates(subset=['age', 'zip_code']).shape
~~~


## 3 Select and filter

### 3.1 Sort

`sort_values(by=, ascending=True/False)`

* `by=`는 별도로 명시 불필요. 
* `ascending=` : `True` 오름차순, `False` 내림차순
* Series, DataFrame 모두 적용 가능
* DataFrame 적용 시,
    1. 지정된 Column 기준으로 DataFrame 정렬
    2. 여러 개의 Column도 정렬 가능. 이 경우, list로 전달. ascending 값도 list로 개별 지정 가능   
    첫 번째 열로 정렬하고, 동일한 값 내에서 두 번째 열로 정렬...

### 3.2 Filter rows

`df[CONDITION - Series comparison statement]`

* Series-comparison을 통해 Boolean mask series를 반환. 이 조건에 맞게 DataFrame을 반환
* Multiple filters (2개 이상 조건문)
    1. Parentheses()로 조건 구분 
    1. `and` ==> `&`, `or` ==> `|` 연산자로 사용
    1. 여러 개의 `or` 조건을 사용해야한다면 `.isin()` 사용
* `.loc()` method를 사용할 것
    * `df.loc(ROW_CONDITION, COLUMN_CONDITION)`

### 3.3 Select 

1. `.loc[]`: label로 해당 값을 반환. Stop 범위가 inclusive
2. `.iloc[]` : 위치값으로 해당 값을 반환. Stop 범위가 exclusive

* 필요한 열만을 선별할 때, 아래 2가지 모두 가능하나 가급적 2번째 방법을 추천   
    1. `ufo[['City', 'State']]`
    2. `ufo.loc[:, ['City', 'State']]`

### 3.5 Sample DataFrame

`.sample()`

* DataFrame에서 임의의 샘플 행을 반환. 실행할 때마다 변화
* `n=` : 샘플 갯수 지정, 별도 지정하지 않고 숫자만 사용 가능
* `random_state=` : 샘플 상태를 지정 가능. 동일한 DF에 대해 동일함 샘플 결과 반환 가능
* `frac=` : DF 전체 크기에 대해 비율로 샘플 반환

~~~Python
# `.sample()`을 활용하여 train/test set 분리
train = ufo.sample(frac=0.75, random_state=99)
test = ufo.loc[~ufo.index.isin(train.index), :]
~~~


## 4 Parameters

### 4.1 'axis' parameter

1. `axis=0`, `axis='index'` : Row 방향. 계산을 수행할 경우, Row 방향으로 계산하므로 개별 Column값 반환
1. `axis=1`, `axis='columns'` : Column 방향. 계산을 수행할 경우, Column 방향으로 계산하므로 개별 Row값 반환

### 4.2 'inplace' parameter

1. `inplace` parameter가 필요할 경우, 보통 `False`가 Default로 지정되어 있음   
: 원래 DataFrame에는 영향을 미치지 않으며 연산을 수행
2. 여러 parameter 값을 바꾸면서 데이터 결과를 사전 확인 가능.   
: 이후 확인된 경우에 대해서만 `inplace=True`로 데이터 치환하며 작업 할 것


## 5. Series

### 5.1 Index

* Index 사용 목적   
    1. Identification : 확인
    2. Selection : 선택
    3. Alignment : 정렬
* 계산 혹은 `pd.concat()` 등을 수행할 때, index가 되어 있는 경우 해당 값 자동 선별 계산됨
    
`.set_index()`: 해당 열로 index 변경   
`.reset_index()`: 현재 index를 DataFrame으로 이동. RangeIndex로 자동 변경.   
`.sort_index()`: index값으로 데이터 정렬 

### 5.2 Dates and times

`pd.to_datetime()` : 'datetime' 객체 생성/변환

* 'datetime' 객체의 장점
    * Mathematical calculation이 가능
    * 다양한 method와 attribute가 제공
* Attribute 사용 : `Series.dt.`
* Timestamp : datetime으로 설정되면 해당 시점 (timestamp)를 활용하여 slice 용이
* Timedelta : datetime 객체를 수리적으로 계산 가능. 결과는 다시 attribute로 변환 가능

### 5.3 Change data type

`series.astype(type)` : 해당 Series를 type을 바꿔줌

> boolean을 `.astype(int)`로 바꿀 경우, 0 또는 1로 반환

### 5.4 String methods

Series/Index에 대해 `.str` methods가 구비되어 있음
* Pandas ducumentation: [Working with text data](https://pandas.pydata.org/pandas-docs/stable/user_guide/text.html)

Tip for `.str.repalce()`
~~~
orders.choice_description.str.replace('[', '').str.replace(']', '')  # .str은 2번 이상 사용 가능
orders.choice_description.str.replace('[\[\]]', '')                  # Regular expression도 사용 가능
~~~

### 5.5 Explore pandas Series

`Series.value_counts()` : 해당 열의 값을 카운트하여 크기 순으로 반환 (series --> series)   
`Series.value_counts(normalize=True)` : 해당 열의 값을 카운트한 결과를 정규화 한 후 크기 순으로 반환 (series --> series)

`Series.unique()` : 해당 열의 값을 중복되지 않게 array 형태로 반환 (series --> array)   
`Series.nunique()` : 해당 열의 중복되지 않는 값의 갯수를 반환 (series --> integer)

`pd.crosstab(Series#1, Series#2)` : 두 개의 열의 관계를 DataFrame을 반환 (series --> df)   

`Series.plot(kind='hist')` : 열의 값으로 그래프 생성   
`Series.value_counts().plot(kind='bar')` : .value_counts()로 반환된 Series로 그래프 생성

Tip. 반환 값이 Series일 경우, 다시 Series method를 사용 가능


## 6 Useful functions

### 6.1 Groupby

`gropuby('COLUMN_NAME')` : 해당 열의 카테고리 별 계산

1. `groupby()`는 groupby object를 생성함. 이를 활용하여 항목별 계산 수행 가능
2. `groupby()`뒤에 열 이름을 명시하여 해당 열만 반환 가능
3. `agg(['..', ...])`을 통해 여러 개의 계산을 동시에 수행 가능
4. `.plot(kind=' ')`를 통해 그래프 생성 가능
  
### 6.2 Dummy variables

> Dummy variables?   
> : 해당 값 여부를 0과 1의 두 가지 값으로만 표현. 기계학습 적용 시 종종 필요.

* Dummy variable 생성 방법
    1. `.map(dict)`: (e.g.) train['sex_male'] = train.Sex.map({'female':0, 'male':1})
        * 해당 열 값을 각각 0과 1로 치환
    2. `pd.get_dummies()`: 
        * `pd.get_dummies(train.Sex)`: 해당 열 값을 바탕으로 Dummy variable로 구성된 별도 DF 생성
        * `pd.get_dummies(train.Sex, prefix='Sex')`: 개별 열 앞에 접두어_을 붙임
        * `pd.get_dummies(train.Sex, prefix='Sex').iloc[:, 1:]`: 첫 번째 열은 미반환

* Dummy variable 생성 후 원래 DataFrame에 붙이는 법
    1. 별도 DF 생성 --> 기존 DF와 `pd.concat`
~~~Python
    embarked_dummies = pd.get_dummies(train.Embarked, prefix='Embarked')
    train = pd.concat([train, embarked_dummies], axis=1)
~~~

    2. 바로 Dummy varialble 생성 후 기존 열 삭제.  
~~~Python
    pd.get_dummies(train, columns=['Sex', 'Embarked'], drop_first=True)  # 첫번째 Dummy 열 삭제
~~~


### 6.3 Apply and map

1. `.map`
2. `.apply`
3. `.applymap`


## 7 Tips

### 7.1 Make DataFrame samller and faster

1. Memory usage 확인
    * `.info()` : Object열에 대해 심층 확인을 수행하지 않고, +로 표기
    * `.info(memory_usage='deep')` : Object열에 대해 심층 확인 후 메모리 사용량을 계산
    * `.memory_usage(deep=True)`
    * `.memory_usage(deep=True).sum()` : 메모리 사용 전체 총합
1. 'Category' Dtype : `.astype('category')`
    * Object열의 경우, 메모리 사용이 큼 --> 반복되는 값의 경우, 별도 Category index를 만들어 보관 후 해당 값은 정수로 치환 가능
    * 값이 일정 이하가 아닐 경우, 오히려 Category type의 메모리 사용이 더 악화될 수 있음
    * `.cat.codes.head()` : Category 할당을 확인
1. 'Category' 내 순서를 할당하고 싶을 경우,
    * 필요 라이브러리 Import --> 요청 순서를 별도 변수에 할당 --> 'astype'으로 해당 변수 지정
    
~~~
from pandas.api.types import CategoricalDtype`
quality_cat = CategoricalDtype(['good', 'very good', 'excellent'], ordered=True)
df['quality'] = df.quality.astype(quality_cat)
df.quality
~~~

### 7.2 SettingWithCopy warning

~~~Python
# SettingWithCopy Warning
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead
~~~

1. `.loc` 사용할 것
    * 2가지 이상의 Operation이 혼합될 경우, Pandas는 Original 또는 Copy를 변경하는 지에 대한 보증을 할 수 없음. 따라서 결과 값이 정확하지 않을 위험이 존재.
    * `.loc`로 하나의 연산을 변경하면 해당 문제 해결
2. 새로운 DataFrame은 `.copy()`로 명시할 것

### 7.3 Display options

* pandas.get_option documentation : https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.get_option.html

* Display option 변경
    * `pd.get_option()` : 현재 옵션 확인
    * `pd.set_option()` : 옵션 변경
    * `pd.reset_option()` : 기본값으로 옵션 초기화
        * 'all' : 모든 옵션을 초기화 (경고는 무시할 것)
    * `pd.describe_option()` : 옵션 관련 매뉴얼 반환
        * '단어' : 해당 단어가 포함되는 arguments 검색 후 반환

* 자주 사용되는 parameter
    * 'display.max_rows'
    * 'display.max_columns'
    * 'display.precision'
    * 'display.float_format'
    
```Python
pd.set_option('display.float_format', '{:,}'.format)  # float type에 대해 3자리마다 , 표시
pd.set_option('display.float_format','{:,.0f}'.format)  # float type에 대해 decimal 제거
```

### 7.4 Iteration

```Python
for index, row in ufo.iterrows():
    print(index, row.City, row.State)
```