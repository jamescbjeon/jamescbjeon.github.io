---
layout: post
title: Pandas 및 성장도표를 활용한 자녀 성장 도식화
subtitle: Children growth analysis with Pandas
categories: Practice
tags: [Pandas, Practice, 자녀성장]
---

## 1 Introduction

현재 직장에서 Process engineer로 근무한지 벌써 10년이 훌쩍 넘었다. 매일 공정 데이터를 관리하고 분석하는 업의 특성 때문인지 어느 샌가부터 숫자와 이력에 대한 강한 강박이 생겨 버렸다.

가령 두 아이와 조카의 신체 성장 기록을 엑셀 시트로 수 년간 관리했었는데 갑자기 Pandas skill practice 삼아 Notebook version으로 migration 해보는 것도 좋겠다는 생각이 들어 정리를 해보았다 ([Jupyter Notebook Link](https://github.com/jamescbjeon/project/blob/main/children-growth/children-growth.ipynb))

일단 File import를 해보자. Dataset은 아래처럼 구성되어 있다.

* PERSON (대상) : 총 3명에 대해 측정함 - Ariel, Ted, Jua
* DATE (측정일자)
* WEIGHT, HEIGHT, HEAD (측정값) : 몸무게(kg), 키(cm), 머리둘레(cm)

![df.head](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/children-growth-1.PNG)

아이들의 성장 정도를 쉽게 파악하기 위해 생년월일을 이용하여 생후개월을 생성하고 이를 Index로 지정하였다. 또한 Body Mass Index 및 성별 열도 추가로 생성하도록 한다.

* MONTHS_FROM_BIRTH (생후개월) : `index`
* BMI (Body Mass Index)
* GENDER (성별) : Male 1, Female 2

가공된 Dataset head는 아래와 같다.

![modified df.head](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/children-growth-2.PNG)

## 2 개별 성장값 비교 

세 아이들의 키 성장을 생후개월에 대해 비교해 보자.

 Ariel의 경우, 셋 중 가장 나이가 많다보니 두 동생들 대비하여 키가 굉장히 크다는 평가를 집안 어른들로부터 많이 받는 편이다. 하지만 데이터 근거하여 비교할 경우, 실제 세 아이들의 키 성장은 생후 70개월까지 큰 차이 없이 비슷함을 알 수 있다. 오히려 70개월 차부터는 Ted의 키가 갑자기 컸음을 알 수 있다.

 ![three kids height](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/children-growth-3.PNG)

키 성장은 생후 100개월 내외까지는 선형 모델과 유사한 것을 추정된다. 가령 Ariel 키 성장 결과로 regression plot을 fit할 경우, linear model과 일치도가 높은 편이다.

![height regression plot](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/children-growth-4.PNG)

세 아이 모두 Scikit-learn Linear Model을 적용하여 Fit 시킨 결과, 모두 R-squared > 0.99의 높은 선형성을 확인하였다. 또한 이 시기에는 약 0.6cm/month의 속도로 유아 성장이 이루어짐을 알 수 있다 (만 2세 ~ 8세).

```Python
>>>
from sklearn.linear_model import LinearRegression
from sklearn.metrics import r2_score

lr = LinearRegression()

for person in birth:
    x = df.loc[df.PERSON == person, 'MONTHS_FROM_BIRTH']
    y = df.loc[df.PERSON == person, 'HEIGHT']
    
    lr.fit(x.values.reshape(-1,1), y)
    yhat = lr.predict(x.values.reshape(-1,1))
    
    print('********')
    print(person)
    print('coefficient: ', lr.coef_)
    print('intercept: ', lr.intercept_)
    print('r-squared: ', r2_score(y, yhat))

# Run result
>>>
********
Ariel
coefficient:  [0.56783271]
intercept:  73.58988753508174
r-squared:  0.9909396144229968
********
Ted
coefficient:  [0.60566605]
intercept:  71.91726515195201
r-squared:  0.993091645972718
********
Jua
coefficient:  [0.55939033]
intercept:  74.31254379817801
r-squared:  0.9936763959131122
```

몸무게 및 BMI의 경우, 키와는 다르게 세 아이들 간 다소 차이가 있었다. 

Ted는 몸무게가 다른 두 여자 아이 대비 높았지만 BMI는 18~19 내외에서 유지되고 있었다. 오히려, Ariel의 BMI가 최근 16에서 19.5까지 크게 증가하였다. 성장기에 키와 몸무게의 증가는 당연하나 비만의 우려가 있으므로 관리가 필요한 시점임을 알 수 있다.

![three kids weight](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/children-growth-5.PNG)
![three kids bmi](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/children-growth-6.PNG)

## 3 유아청소년 성장도표

### 3.1 여아 w/Ariel, Jua

이제 대한민국 평균과 비교하여 우리 아이들이 잘 성장하고 있는지 비교해 보도록 하자. 

WHO 및 대부분의 국가에서는 소아청소년 성장 통계를 제공한다. 우리 나라의 경우, [질병관리청](http://www.cdc.go.kr/contents.es?mid=a20303030400)에서 해당 내용을 확인할 수 있다. 이를 우리 아이들의 Dataset과 병기하여 확인해보자.

남아와 여아의 성장 수준이 다르기 때문에 성장도표 역시 남녀 성별에 따라 구분하여 제공된다. 일단 Ariel과 Jua의 성장 수준을 대한민국 평균과 비교해 보자. 

> 하기 그래프에서 실선은 각 아이들의 성장 데이터를, 점선은 대한민국 소아청소년 백분위(Percentile, 100%) 값을 나타낸다.

키 성장의 경우, Ariel과 Jua 모두 70개월 내외까지 약 50% 수준에서 성장함을 알 수 있다. Ariel의 경우, 100개월(만 8세) 전후하여 키 성장이 급격하게 발생하여 백분위 기준 75% 수준까지 도달하였다 (상위 25% 의미).

성장 도표를 확인할 때, 약 40개월에서 130개월 내외까지 키 성장이 모든 백분위에 대해 1차 선형식과 근사하게 증가함을 알 수 있다. 이 시기가 통계적으로 볼 때 대부분의 성장이 이루어 지는 구간이며, 150개월을 넘어가면 대부분의 성장이 멈추게 된다 (남녀 차이는 존재).

![girl height](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/children-growth-7.PNG)

몸무게의 경우, Jua는 75% 수준에서 유지 중이다 (상위 25%). Ariel의 경우 50% 내외에서 유지되던 몸무게가 100개월 전후하여 약 80% 수준까지 크게 증가하였다. 이로 인해 BMI 수치도 같이 크게 증가되었음을 알 수 있다.

![girl weight](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/children-growth-8.PNG)
![girl bmi](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/children-growth-9.PNG)

### 3.2 남아 w/Ted

Ted는 50개월 내외까지는 하위 25% 수준의 키였지만, 최근에는 부쩍 성장하여 대한민국 중위수, 즉 50% 내외까지 성장한 모습이다.

![boy height](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/children-growth-10.PNG)

적당히 살이 쪘다고 생각했는데 몸무게는 상위 25% 내외에서 유지되는 모습이다. BMI 측면에서는 상위 10% 수준까지 육박한다. 단, 앞에서 지적한 것처럼 BMI 값은 큰 변화없이 오히려 서서히 감소하는 모습이기 때문에 큰 문제는 되지 않을 듯 하다.

![boy weight](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/children-growth-11.PNG)
![boy bmi](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/children-growth-12.PNG)

### 3.3 백분위 추이

성장도표와 비교해 보니 아이들이 어떤 수준에서 성장하고 있는지 대략적인 감을 잡을 수 있어 상당히 유용한 듯 하다. 특히 백분위 기준으로 아이들의 성장 수준을 별도로 집계해 보았다.

Ariel은 생후 65개월까지 키와 몸무게 모두 중위수 내외에서 잘 유지된 편이다. 다만 65개월 전후하여 키와 몸무게가 크게 증가하였다. 소아청소년기에 높은 성장은 반가운 일이지만 단기간에 이런 성장은 문제가 있을 가능성이 있다. 실제로 병원 확인 결과, 성호르몬 과다로 성조숙증이 의심되어 70개월 차부터 관련 치료를 받고 있는 중이다.

![percentile ariel](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/percentile_ariel.PNG)

Ted는 생후 내내 키에 비해 몸무게가 높은 백분위 수준으로 유지되었다. 하지만 활동에 큰 문제가 없고 최근 키 성장으로 인해 BMI 등이 개선되는 경향이 있어 좀더 지켜볼 예정이다.
![percentile ted](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/percentile_ted.PNG)

Jua는 Ted와 비슷한 경향성으로 성장하는 모습이다. 최근 Jua 역시 키가 훌쩍 커서 (본 데이터에는 포함되지 않음) 나중에 기회가 되면 측정 및 확인을 해보려고 한다.
![percentile jua](https://raw.githubusercontent.com/jamescbjeon/project/main/children-growth/percentile_jua.PNG)

## 4 글을 마치며

엑셀 시트로 관리하던 내용을 pandas로 재정리해보니 다소 시간이 걸리긴 했지만 재미도 있고 생각치 못한 Insight도 얻은 기분이다. 특히 Scikit-learn을 통한 Linear model 적용이나 백분위값 추적은 엑셀로도 가능하겠지만 pandas로 훨씬 쉽게 적용이 가능하였다.