---
layout: post
title: Innovation, Efficient markets, Behavioral finance
subtitle: Financial Markets - Week 2
categories: Investment
tags: [로버트 실러, 효율적 시장 가설, 행동경제학 Coursera]
---

Rober J. Shiller 교수님의 [Financial Market 강좌]({% post_url 2022-04-17-financialmarket0 %}) 중 2주차 요약이다. 유한 책임, 물가연동채권과 같은 금융 시장의 혁신 사례 및 효율적 시장 가설과 현재 할인 가치 (PDV), 그리고 전통 경제학에서 설명되지 않은 비합리성을 다룬 행동 경제학에 대해 공부한다.

## 0 Goal

1. 혁신
	* 유한 책임의 개념과 심리학, 리스크 다양화 및 기업 재무와의 연관성
	* 인플레이션 지수 채권(IID)와 하이퍼 인플레이션 해결을 위해 고안된 통화 혁신
2. Efficient Market
	* 효율적 시장 가설의 핵심 직관과 정의, 그리고 왜 절반의 진실인가
	* 현재 할인 가치 (PDV) - 부동산 시장의 기본, 주식 시장 예측에 대한 가정, 그리고 주식 가격을 매기기 위한 기본 프레임워크
3. 행동 경제학
	* 전망이론 - 가치함수 & 무게함수
	* 희망적 사고 편향과 인지 부조화
	* 반사회적 인격장애와 경계선 인격장애


## 1 Innovation

### 1.1 Invention Take Time

세상이 바뀌기 위해서는 적당한 시간이 필요하다. 보험은 필요한 개념이지만 실제로 적용되는 데 꽤 오랜 시간이 걸렸다.

금융에서 새로운 개념이 탄생하고 시장 전반에 받아들여지기까지는 시간이 필요하다. 그래도 빠르게 앞으로 나아가고 있다.

### 1.2 Limited Liability

`유한책임법`

1811년 뉴욕주에서부터 시작. 주주의 책임을 제한하여, 투자 부담을 줄이고 많은 자본을 끌어오는 원동력 역할을 함

대부분의 회사는 실패한다. 단, 몇 개의 회사는 살아남아 엄청난 성공을 거두게 된다. ~~복권이랑 똑같은데?~~ 여러 개의 회사에 투자를 해도 부담이 없어질 수 있다.

### 1.3 Inflation Indexed Debt

`CPI`: Customer Price Index, 소비자 물가지수  
`Inflation Indexed Debt`: 물가지수연동채권
 
* 인플레이션으로 인해 명목소득/대출이 모두 없어질 수 있다. 이를 반영하여 채권을 발행할 수 있다.
* 칠레에서 1967년 하이퍼 인플레이션 대응을 위해 `Unidad de Fomento`,  UF라는 인플레이션 대응 통화단위를 만들어 사용 중이다. 신문 등에 주기적을 발표되며 부동산 등 큰 거래에 사용된다.

### 1.4 Real Estate

부동산에는 공매도가 없다. ~~*그래서 부동산 가격이 안 떨어지는구나*~~


## 2 Efficient Market

### 2.1 Intuition of Efficiency

시장 가격은 모든 정보를 이미 반영하고 있고, 새로운 정보 역시 즉각 반영된다 &rarr; *효율적 시장가설의 핵심!*

> 시장을 이기는 것은 얼마나 어려운가.  
> 충분한 전문성이나 정보가 없는 나로써는 1) 시장 전체를 사서 마냥 기다리거나, 2) 충분히 합리적인 상상력으로 이를 극복할 수 밖에 없다.

Competition in capital markets is very tough.

> 시장과 싸워서 이기기는 굉장히 어렵다. 이를 순순히 받아들이고 이를 극복할 수 있는 "합리적인 전략"이 필요하다.

Semi-strong form of Efficiency - Incorporate all publicly available information.  

> 효율적 시장가설은 절반만 맞는 이론이다. 얼마나 시장이 효율적인가에 대한 합의는 논란이 있으나, 아마 중간강함 수준이 맞지 않을까 싶다. 이는 시장가격에 내부 정보는 포함되지 않음을 가정한다.

### 2.2 Price as PDV, Present Discounted Value

~~~
### Growing consol model, or Gordon Model
# 가정1. Income = Dividends
# 가정2. Income growth-rate = g, Discunt-rate = r

Price = Earing / (r - g)
P/E = Income / (r - g)
~~~

효율적 시장가설은 낮은 P/E를 바겐세일로 보지 않음. 미래에 수익성장(g)이 낮아질 것으로 이를 설명.


## 3 [Behavioral finance](https://eiec.kdi.re.kr/material/pageoneView.do?idx=1499)

`행동경제학` : 고전 거시경제에서 설명되지 않는 "비합리성"에 대한 "심리적" 이해

### 3.1 [Prospect Theory](https://dbr.donga.com/article/view/1202/article_no/4766/ac/magazine) 전망이론

**사람들은 확률을 왜곡되게 표현하고 손익을 동등하게 다루지 않는다.**  
기존 효용이론(Utility theory)을 보완하며 사람들의 비합리성을 설명

1. 준거 의존성 Reference dependency : 기존값(준거점)에 따라 가치 변화
2. 민감도 체감성 Diminishing sensitivity : 이익/손실의 크기가 커질수록 변화 민감도 감소
3. 손실 회피성 Loss aversion : 같은 크기라도 이익의 효용(기쁨)보다 손실의 비효용(고통)이 더 큼

`Value function`: 이익/손실 모두 준거에서는 민감하나 멀어질수록 둔감. 또한 이익보다 손실의 가치 민감도가 더 크다.
![Value function](/assets/images/post-2022-04-17/fm-w2-1.png)

`Weighting function`: 적은 손실, 확정된 이익에 집중. 이익은 안전한 것을 선호하나 손실은 모험적인 선택을 선호.
![Weighting function](/assets/images/post-2022-04-17/fm-w2-2.png)

### 3.2 Overconfidence 과잉확신

긍정적인 결과를 더 높은 확률로 기대. 실패할 경우, 전망이론에 따라 손실로 인한 상실감 큼

금융 시장의 주식거래의 엄청난 거래량도 설명 가능 - 희망적인 사고 편향 때문

### 3.3 Cognitive dissidence 인지부조화

자신의 신념이 틀렸다는것을 알게 되었을 때 겪게 되는 정신적 갈등

잡지에서 이미 산 차의 광고만 읽고, 사지 않은 차의 광고는 무시 - 이미한 결정이 옳음을 확인받고 싶어 함. 

Disposition effect 처분효과: 주식가격 하락 시 무시. 오르면 바로 처분


### 3.4 Mental Compartments 정신구획

### 3.5 Attention anomalies 주의분산

사람들은 모든 것에 집중할 수 없다

소형주의 경우, 많은 사람들의 주의를 끌지 못하기 때문에 가격이 저렴

### 3.6 Anchoring 정박효과

기존 가치에 개념이 고착되는 현상

".com"이 달려 있으면 회사가 더 멋져 보임

### 3.7 Representativeness 대표성 어림짐작하기

친숙한 유형에 친숙하게 사물을 판단

Random walk에 대해 익숙한 패턴을 찾는 경향. 패턴을 만들어 주가 조작하려고 하기도 함

### 3.8 그 외

* Disjunction 분리효과
* Magical thinking 미신
* Quasi magical thinking 준미신
* Culture 문화
* Antisocial personality disorder 반사회적 성격장애


[Course material - Week 2]({{ site.url }}/assets/pdf/financialmarket/financialmarket_w2.pdf)  
[Coursera - Financial Market - Week 2](https://www.coursera.org/learn/financial-markets-global/home/week/2)