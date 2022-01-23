---
layout: post
title: 데이터에 기반한 대한민국 역대 대통령 지지율 분석
subtitle: Data Science Practice - Korea President Approving Rate Analysis with Pandas
categories: Pandas
tags: [Data Science, Pandas, Practice, Korea President]
---

## 1. 개요

코로나19가 창궐하고 현 정부가 이를 잘 대응하면서 현 대통령의 지지율이 크게 증가했다고 합니다. 몇 주 뒤에는 잇다른 부동산 정책 실패로 지지율이 크게 떨어졌다는 정반대의 뉴스가 나옵니다. 대통령 지지율 둑이 뚫려 부정평가가 크게 증가한다는 기사가 나오지만, 같은 시기에 지지층 결집하면서 콘크리트 지지율이 견고하다는 다른 언론의 기사도 조회됩니다. 대부분의 뉴스에는 지난 몇 주간의 지지율 변화 추이와 역대 대통령 지지율 조사 결과에 대한 짧막한 코멘트만 기재될 뿐, 이를 심도있게 분석하고 비교하는 기사를 찾는 일은 생각보다 쉬운 일이 아닙니다.

만약 순수한 데이터 관점에서 대통령 지지율을 분석한다면 어떤 결과를 얻을 수 있을지 궁금했습니다. 정치적인 선입견을 완전히 배제한 상태에서 아래 짧은 데이터 분석을 통해 현 대통령이 전 대통령들과 대비하여 얼마나 국민의 지지를 받고 있는지, 그리고 향후 어떤 지지율 변화를 겪을 것인지에 대한 간단한 예측을 해보려고 합니다.

하기 분석은 Jupyter notebook으로 수행하였고 자세한 결과 및 원본 코드는 [여기][Notebook]에서 확인 가능합니다. 이를 통해 얻으려는 분석의 목적은 아래와 같습니다.

1. 역대 대통령 지지도 비교
2. 현 정부 지지도 예측 및 분석


## 2. 데이터 준비

대통령 지지율 조사는 13대 노태우 전 대통령부터 시작되었습니다. 13대(노태우)부터 17대(이명박)까지는 매 3개월마다 한국갤럽에서 조사하였고, 18대(박근혜)부터는 한국갤럽과 리얼미터에서 매주 조사하여 발표하고 있습니다.

분석을 위해 아래의 Library 및 설정을 사용했습니다.

~~~Python
import numpy as np
import pandas as pd
pd.set_option("display.max_rows", None, "display.max_columns", None)  # 행열의 값이 최대로 표시되도록 설정

import requests
from bs4 import BeautifulSoup

import matplotlib as mpl
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.linear_model import LinearRegression  # 선형회귀 분석
~~~

한글 위키피디아 페이지에 [역대 정부의 지지율 조사 결과](https://ko.wikipedia.org/wiki/%EB%8C%80%ED%95%9C%EB%AF%BC%EA%B5%AD%EC%9D%98_%EB%8C%80%ED%86%B5%EB%A0%B9_%EC%A7%80%EC%A7%80%EC%9C%A8)가 잘 정리되어 있습니다.

![19대 문재인 대통령 지지율 조사 결과 - Wikipedia](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/wikitable1.PNG)

해당 페이지를 Request를 이용하여 수집한 후 BeautifulSoup을 이용하여 Pandas DataFrame 형태로 가져오도록 합니다.

~~~Python
url = 'https://ko.wikipedia.org/wiki/%EB%8C%80%ED%95%9C%EB%AF%BC%EA%B5%AD%EC%9D%98_%EB%8C%80%ED%86%B5%EB%A0%B9_%EC%A7%80%EC%A7%80%EC%9C%A8'

res = requests.get(url)
soup = BeautifulSoup(res.text, 'lxml')  # 페이지 내에서 텍스트만 soup 객체로 반환
table = soup.find_all('table')
~~~

Soup에서 가져온 TABLE 객체는 HTML 형태로 되어 있으므로 head와 data 부분을 구분하여 별도로 Parse하고 이를 DataFrame 형태로 입력 가능한 List 혹은 Array 형태로 가공해야 합니다. 

대부분의 데이터 분석에서는 EDA 및 심층 분석 단계보다 데이터 준비 과정이 번거로운데, 이번에도 역시 Wikipedia 내 HTML Table 중 일부분이 위아래 혹은 좌우가 서로 merge되어 있어서 해당 부분을 반영하는 게 가장 어려웠습니다. HTML tag 중 `rowspan`, `colspan`을 찾아 해당 값을 반영하는 함수를 만들어 해결할 수 있었습니다 ([Jupyter notebook에서 원본 코드 확인][Notebook]).

정리된 데이터를 분석을 위해 Pandas DataFrame 형태로 가져 옵니다.

![19대 문재인 대통령 지지율 DataFrame 변환](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/tableji.PNG)

위키피디아 페이지와 차이가 있어 보입니다만, Table head와 Table data를 용이성을 위해 구분했을 뿐 동일한 결과입니다.

> 실제로 HTML을 Parsing한 결과, 19대 대통령 표만 조사기간이 Table head가 반영되어 있고, 나머지 대통령 표는 조사 기간과 결과가 모두 Table data로 반영되어 개별적으로 확인을 해야했습니다. HTML5가 표준이 되면서 Tag 정보가 대체적으로 정확히 반영되어 있으나 HTML 언어 자체가 자유도가 높기 때문에 Data 준비에는 기존 코드가 있더라도 매번 상당한 확인이 필요합니다. 

반환된 결과는 위키피디아처럼 연도별로 별도 열로 구분되어 있으므로 기간과 조사결과, 2개 열로 병합합니다. 아래는 19대 대통령 지지도 조사를 정리한 DataFrame의 첫 10개 행 결과입니다. 13대부터 18대까지 동일한 과정을 반복합니다.

![19대 대통령 지지율 DataFrame 변환 및 병합](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/tableji2.PNG)

## 3. 분석 방법

준비된 DataFrame으로 현 19대 대통령 지지율 그래프를 그려 봅시다.

가로축은 주(Week), 세로축은 지지율입니다. 출범 초기 80% 내외의 높은 지지율이 임기에 따라 지속적으로 하락하는 모습을 보입니다.

![19대 대통령 지지율 비교](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/weekt_19.png)

18대 조사결과와 병합하여 같이 확인해 보도록 합시다.

Graph scale이 바뀌면서 상대적으로 19대 정부의 지지도가 18대 대비하여 높음을 알 수 있습니다. 18대 정부의 경우, 180주차를 넘어서면서 탄핵 정국에 들어서며 지지율이 크게 하락하였습니다.

![18대 및 19대 대통령 지지율 비교](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/weekt_1819.png)

13대부터 17대 대통령 임기 간에는 지지도 조사가 매 분기, 즉 3개월마다 이루어졌습니다. 서로 비교를 할 수 있도록 18, 19대 대통령 지지도 주차별 조사 결과를 Pandas의 Groupby method를 사용하여 분기별로 변환합니다.

## 4. 데이터 분석

분기별로 정리된 DataFrame을 활용하여 본격적인 데이터 분석을 시작합니다.


### 4.1 조사 횟수 및 결측치

13대 대통령부터 5년 단임제로 대통령 임기가 제한되었으므로, 분기별 지지율 조사가 성실히 수행될 경우 5년 간 총 20개의 데이터가 확보되어야 합니다. 아직 임기 중인 19대 문재인 대통령의 경우 15개, 탄핵으로 임기를 채우지 못한 18대 박근혜 대통령의 경우 16개, 그리고 나머지 대부분의 대통령은 20개 데이터가 확보 되었습니다 *(아래 표 'count'행 참조)*. 13대 노태우 대통령의 경우, 6개의 데이터가 누락되었는데 아마 조사 초기라 조사의 어려움이 있지 않았을까 추측해 봅니다 (아직 군사정권이었기 때문에 발표가 어려웠을 수도 있습니다).

![역대 대통령 지지율 요약](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/describe.png)

### 4.2 평균

조사 결과의 평균을 비교하면 19대 현 정부가 56%의 지지율로 가장 높은 평균 지지율을 보이고 있습니다. 다만 이 결과는 보통 임기 말에 지지율이 낮아짐을 고려할 때, 초기의 높은 지지율로 인해 편중되었을 가능성이 높으므로 이를 고려해야 합니다.

임기가 끝나지 않은 현 대통령을 제외하면 김대중 대통령, 박근혜 대통령, 김영삼 대통령 순으로 평균 지지율이 높았습니다. 반면, 노무현 대통령 및 노태우 대통령은 임기 중 평균적으로 크게 인기가 없던 대통령이었음을 확인할 수 있습니다.

![역대 대통령 지지율 평균](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/mean.png)

임기 연도별 평균을 비교하면 1년차와 5년차를 제외하면 2~4년차에서 모두 현 19대 문재인 대통령의 지지율 평균이 가장 높은 것으로 확인됩니다 *(아래 표 가장 우측 'MAX'열 참조)*. 이미 임기가 종료된 1~3년차 균의 경우을 볼 때 현 정부의 인기가 상당히 높았음을 알 수 있습니다. 

또한 연도별 평균을 통해 임기가 진행됨에 따라 모든 대통령에게서 지지율 하락이 뚜렷이 나타남을 확인할 수 있습니다. 특히 임기 5년차에는 가장 우수한 15대 김대중 대통령 조차도 평균 지지율은 30%가 채 되지 않습니다.

![역대 대통령 지지율 연도별 평균](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/mean2.png)

### 4.3 산포

산포 측면에서 김영삼 대통령 지지율이 가장 큰 변화가 있었습니다. 이명박 대통령과 대비하면 표준 편차 및 최대-최소 차이가 2배 이상의 산포를 보입니다. 문민정부 출범 당시 상당한 기대와 지지를 받았습니다만, 정권 말기 IMF로 인한 지지율 감소가 원인이 아닐까 추측해 봅니다.

![역대 대통령 지지율 산포](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/std.PNG)

### 4.4 최대 및 최소

역대 가장 높은 지지율은 김영삼 정부 때입니다. 무려 83%나 됩니다. 모두 임기 초반 지지율입니다. 당시 문민정부에 대한 기대가 얼마나 높았는지 간접적으로 알 수 있습니다.

반면 이명박 정부 지지율은 임기 초반 가장 높을 때도 50%를 간신히 넘었습니다.

![역대 대통령 지지율 최대](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/max.png)

역대 가장 낮은 지지율은 박근혜 정부와 김영삼 정부 때입니다. 각각 탄핵과 IMF라는 국가 위기로 인해 대통령 지지도가 크게 하락하고 국정운영에 무리가 있던 시기였습니다. 모두 정권 말기 때 모습입니다 (18대 대통령 지지율 DataFrame은 Weekly로 작성되었기 때문에 Quarter data와 일부 차이가 있습니다).

![역대 대통령 지지율 최소 #1](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/min.png)
![역대 대통령 지지율 최소 #2](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/min2.png)

### 4.5 변화 그래프

분기별 대통령 지지율 변화 그래프입니다. 대통령 지지율은 모든 정권에서 임기 초반에는 높은 수치로 출발하다 점차 하락하는 동일한 경향성을 나타냅니다.

전반적으로 현 19대 문재인 대통령 지지율은 타 대통령과 비교할 때 가장 높은 수준에서 계속 유지되고 있는 것으로 보입니다.

![역대 대통령 지지율 그래프](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/apprate.png)

좀 더 쉬운 이해를 위해 현 19대 대통령을 제외한 18대부터 13대 정부까지의 열을 바탕으로 분기별 평균, 최대, 최소값을 산출했습니다. 해당 결과와 문재인 대통령의 지지율을 분기별 비교한 결과는 아래와 같습니다.

현 문재인 대통령의 지지율이 지속적으로 하락하기는 하나, 기존 대통령의 지지율 평균을 약 15~10% 내외로 크게 상회하며 유지되고 있고, 역대 대통령 분기별 지지율 최대값과 비슷한 수준에서 거동함을 확인할 수 있습니다.

![역대 대통령 지지율 최대, 평균 그래프](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/apprate2.png)

### 4.6 선형 회귀 분석

선형 회귀 모델을 적용하기 앞서 상관계수를 확인해봅시다. 

이미 그래프에서 확인한 것처럼 대통령 임기와 지지율 간에는 강한 음의 상관관계가 존재합니다. 특히 역대 대통령 지지율 평균값과 최대값은 상관관계 절대값이 0.9를 넘어 강한 선형관계를 보입니다. 개별 대통령으로는 김대중 대통령, 김영삼 대통령이 강한 음의 상관관계를 보입니다.

![역대 대통령 지지율 상관계수](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/corr.png)

가장 높은 음의 상관관계를 갖는 역대 대통령 지지율 평균과 임기(분기)간의 회귀 곡선입니다. 일부 Noise를 제외하면 1차 모델이 정확하게 일치한다고 말할 수 있을 것 같습니다. R-squared 값이 무려 **0.946**이나 됩니다.

![역대 대통령 지지율 회귀그래프 - 평균](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/regplotmean.png)

역대 대통령 지지율 평균과 임기 간의 회귀 곡선입니다. R-squared 값이 **0.876**으로 상당히 높은 수치입니다.

![역대 대통령 지지율 회귀그래프 - 최대](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/regplotmax.png)

현 19대 문재인 대통령 지지율과 임기 간의 회귀 곡선입니다. R-squared 값이 **0.723**이며 상기 2개 결과에 비해 적합성이 일부 떨어집니다만, 역대 대통령 지지율 추이 및 R-squared 값을 볼 때 선형 회귀 모델을 적용하는 데는 큰 문제가 없어 보입니다.

![역대 대통령 지지율 회귀그래프 - 19대](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/regplotjim.png)

Scikit-learn library를 활용하여 LinearRegression 모델을 생성합니다. 아래는 해당 모델에 가장 높은 적합성을 보인 역대 대통령 지지율 평균값/최대값 및 현 19대 문재인 대통령 지지율과 임기(분기별) 데이터를 적용시켜 반환된 결과입니다.

![역대 대통령 지지율 회귀그래프 - 19대](https://raw.githubusercontent.com/jamescbjeon/project/main/korea-president-apprate/lm.png)


## 5. 논의

현 19대 대통령 지지율 (위 그래프 내 '#19. Moon Jae-in') 은 기존 13대부터 18대 대통령 지지율 평균을 상회하며 유지되고 있고, 선형 회귀선이 기존 대통령들의 분기별 최대값과 거의 유사하게 거동하고 있는 것을 볼 때 지금까지는 가장 인기 있는 대통령라고 말할 수 있을 것 같습니다 (동의하지 않는 분들도 계시겠지만 지지율 데이터로는 명확합니다).

최근 각종 매체에서 현 정부 지지율이 역대 최저로 떨어졌다는 뉴스가 자극적으로 나오고 있습니다만, 기존 대통령 지지율 이력을 확인할 때 임기가 진행됨에 따라 지지율이 하락하는 것은 모든 대통령이 겪은 결과이며 선형 모델을 따라 높은 신뢰도 수준, 즉 예측 가능한 수준에서 하락함을 확인했습니다.

12월 초 진행된 대통령 지지도 조사에서 40%의 콘크리트 지지율이 무너졌다며 모든 매체에서 대서특필하고 있습니다 ([관련 기사](https://www.donga.com/news/Politics/article/all/20201205/104297349/1)). 해당 기사에서 언급하는 지지율은 14.5분기 기준 39%입니다. 반면 위의 선형모델로 예측된 해당 시기 19대 대통령 지지율은 37.5%입니다. 즉 현 문재인 대통령 지지율은 임기 초부터 하락한 기존 결과값과 아직 유사 수준에서 거동하고 있는 것으로 보입니다.

따라서 현 정부 지지율이 집권 이후 최저라는 뉴스는, 임기에 따라 모든 대통령이 겪는 당연한 사실을 정치적 목적 혹은 통계적 무지에 의해 자극적으로 포장되었을 가능성이 높으며, 이보다는 아래의 지표로 현 정부 지지율을 판단하는 것이 합리적으로 보입니다 (극적인 정국 변화가 없다면 남은 임기 간 문재인 대통령 지지율은 역대 대통령과 동일하게 최저값을 계속 갱신하며 하락 할 것으로 보입니다).

1. 선형 모델 대비한 현 정부 지지도 비교
    * 위 그래프에서 `#19 Prediction by Linear Model`은 임기 시작부터 현재까지의 19대 대통령 지지율을 바탕으로 생성된 선형 모델입니다. 만약 남은 임기에서 조사되는 지지율이 해당 모델보다 빠르게 하락한다면, 현 대통령 지지율이 기존 대비하여 하락 폭이 크다라고 말할 수 있을 것입니다.
2. 기존 정부 평균에 대비한 현 정부 지지도 비교
    * 최근의 정책에 대한 여러 논란에도 불구하고, 데이터가 보여주는 현 대통령의 인기도는 기존 정부 대비하여 상당히 높은 편입니다. 현재까지는 기존 지지율 최대값과 거의 유사한 수준에서 거동 중이나 만약 남은 임기에서 인기 하락으로 인해 지지율 조사 결과가 평균 선에 근접하거나 이보다 하락한다면 현 19대 대통령 지지율이 크게 하락하여 정국 운영에 상당한 어려움이 될 것을 예상할 수 있습니다.

## 6. 결론

대통령 지지율 조사는 현 정부 및 정권에 대한 국민 여론의 바로미터이기 때문에 많은 정치 평론가들이 나름의 정치적 분석을 내놓고 이를 가지고 설왕설래하는 뜨거운 주제입니다. 또한 국민 정서로 통용되는 다른 정성적인 근거에 비해 매주 수치로 조사되는 잘 정리된 데이터 집합이기도 합니다.

본 분석에서는 한국갤럽 조사 결과를 바탕으로 13대부터 19대 현 대통령까지의 지지율을 정치적 분석이 아닌 데이터 및 선형 모델 관점에서 살펴보았습니다. 그리고 이를 통해 대통령 지지율은 높은 신뢰도로 임기에 따른 선형 모델이 적용 가능하며, 지지율 하락이 필연적임을 확인하였습니다.

상기에서 적용된 모델이 1차 선형 회귀로 가장 단순한 모델임에도 불구하고 대부분의 언론 및 매체에서 해당 내용에 대한 간단한 이해도 없이 최신 조사결과를 단지 수 주, 혹은 수 개월 전의 값과 비교하며 여러가지 문제를 제기하는 것은 그다지 합리적으로 보이지 않습니다. 정치적인 해법도 중요하지만 때로는 데이터에 기반한 논평이 진행되어야 해당 여론 조사가 좀 더 목적에 부합한 형태로 사용되는 것이 아닐까하는 생각을 합니다.

---

분석은 Jupyter notebook으로 수행하였고 자세한 결과 및 원본 코드는 [여기][Notebook]에서 확인 가능합니다.

[Notebook]: https://github.com/jamescbjeon/project/blob/main/korea-president-apprate/korea_president_approval_rating.ipynb