---
layout: post
title: Risk, Insurance, Portfolio Diversification
subtitle: Financial Markets - Week 1
categories: Investment
tags: [로버트 실러, 금융공학, 시장경제, Coursera]
---


## 1 Welcome to the Course

**Finance is a Technology, for Good or Evil**

Developing world is more interested in our finance technology than in our paltry foreign aid or empty sympathies.  

> 금융 그리고 금융공학은 전기나 바퀴와 같이 인간의 필요로 만들어낸 발명품이라고 볼 수 있을 듯 하다. 다만 후자가 자연의 물리법칙을 이용해 내는 수법이라면 금융은 인간이 돈과 자본이라는 인공의 개념을 고도로 진화시켰다는 면에서 차이가 있을 것이다.


## 2 Variance

### 2.1 VaR

**Value at risk**, 발생 가능한 최대손실 금액 - [Investopia 설명](https://www.investopedia.com/articles/04/092904.asp)
* 1987년 시장 폭락 이후 발명된 개념
* 보통 "정해진 금액 $"에 대해 "주어진 확률"과 "기간"으로 정의
	* 1% one-year Var of 10 million dollar = 주어진 포트폴리오의 연간 $10M 손실 가능성 1%

### 2.2 Stress Test

Dodd Frank Act (2010)는 최소 3가지 경제 상황에 대해 스트레스 테스트를 할 것을 요구

> VaR과 Stress test가 경제위기 발생 시 금융기관의 안정성을 담보할 수 있을까?  
> 정규분포를 보이는 자연 현상과 달리 여러 경제 주체들이 쉴 새 없이 움직이는 시장에서는 Black Swan이 수시로 발생하고 있다. 이를 시장은 큰 수의 법칙이 적용되지 않는다고 말할 수도 있고, 반대로 100여년의 금융 역사가 큰 수의 법칙을 적용하기에 아직 작다고 판단할 수도 있을 것이다. 어쨌건 상기의 결과들은 참고로는 활용 가능하나 절대적 기준이 될 수는 없다.

### 2.3 Stock Market

* 보통 `S&P500`을 Benchmark for Return, 시장수익률 지표로 활용한다
* Very Unstable
	* Law of Large number 적용을 받지 않음
		* Stock market is not independent. 즉, 서로 강한 연관이 있음
* Return이 크면 변동성도 크다. ~~*과연 견딜 수 있을까?*~~
![SP500](/assets/images/post-2022-04-17/fm-w1-1.png)

### 2.4 Beta
```
Beta
= Covariance / Variance = 공분산/분산
= Cov(return(i), return(market)) / Var(return(market))
```
시장 전체 분산 대비 시장과 해당 종목간 공분산의 비율로 정의. 즉, 시장 대비 변화 수준을 의미.

```
# 주식i의 수익률
return(i) 
= return(free) + beta(i) x [return(market) - return(free)]
= [Risk-free Rate] + [Variance (=Beta)] x [Risk Premium]

투자기대수익
= 무위험기대수익(보통 국채) + Beta x [시장수익률 - 국채수익률]
```
어떤 주식의 기대 수익률은 변동성과 시장 및 국채 수익률로 구할 수 있으며, 이는 무위험수익 항목과 위험수익항목으로 구분된다.

> 국채수익률 return(free) 3%, S&P500 수익률 11%, beta 3.0일 경우,  
> [기대수익률, return(i)] = 3 + 3 x (11 - 3) = 27%

![SP500](/assets/images/post-2022-04-17/fm-w1-2.png)

### 2.5 Distribution & Outlier

* CLT, Central Limit Theorem - 중심극한 정리
	* 동일한 확률 분포를 가진 독립 확률 변수 n개의 평균의 분포는 n이 적당히 크다면 정규분포에 가까워진다
* 큰 수의 법칙, 즉 상식은 주식 시장에서 실패한다.
	* 서로간 독립적이지 않음. 밀접하게 연관되어 있음
	* 따라서 분포가 정규분포를 이루지 않음.
		* `Cauchy` 혹은 `Fat-tailed` 형태로 분포 &rarr; Outlier/Black-swan 출몰

![Fat tailed curve](/assets/images/post-2022-04-17/fm-w1-3.png)


## 3 Insurance

### 3.1 [Risk Pooling](https://www.actuary.org/content/risk-pooling-how-health-insurance-individual-market-works-0)

홍수나 지진과 같은 재앙적인 위험으로부터 보험 회사를 보호하기 위해 함께 모여 풀(Pool)을 형성 &rarr; 보험 사업을 가능하게 해주는 원천

* n개의 계약이 독립적이고 각 p라는 청구 확률을 가질 때, 
	* 전체 계약은 이항분포를 갖게됨
	* 전체  표준편차 = `Root(p(1-p)/n)`
	* n이 커질 수록 표준편차는 0에 수렴

> 예시. 10,000개의 계약으로 이루어진 보험이 개별 지급확률이 10%일 때, 전체 표준편차는?  Root(0.1 x 0.9 / 10000) = 0.003

### 3.2 [Moral Hazard](https://www.investopedia.com/ask/answers/09/moral-hazard.asp)

보험 가입을 하게되면 상대적으로 위기 관리에 태만해지며, 심지어 스스로 Risk를 조장(방화 등)하는 형태로 이용할 수 있음.

따라서 이러한 도덕적해이는 부분적으로 공제(deduction) 및 공동보험(coinsurance) 형태로 관리되고 있음

### 3.3 Selection Bias

가령 건강보험은 이미 건강이 좋지 않은 사람들이 집중적으로 가입하여 청구율이 올라가고 이로 인해 아직 건강하나 보험 가입이 필요한 사람을 높은 비용으로 차단할 수 있음 (선택 편향)

이를 막기 위해 그룹 정책, 테스트 및 소개, 의무 정부 보험 등이 활용됨

### 3.4 보험 그 외

미국의 경우, 국가 단위 보험 관리국(Federal Insurance Office)은 없음. 주 단위로 관리

건강보험 - 오바마케어

재해보험 - 지진, 홍수, 허리케인, 재해 등


## 4 CAPM

### 4.1 Portfolio Diversification

Don't put all your eggs in one basket.

Law of large numbers means that spreading over many independent assets reduces risk, has no effect on expected return.

> 좋은 투자를 위해 위험을 감수해야 한다. 위험은 이미 투자 자체에 내재되어 있으며, 위험하지 않다면 추가적인 수익이 없을 것이기 때문에.

> 다만 자산을 한 곳에 모아두는 것이 아니라 여러 곳에 분산시킴으로써 위험은 관리 가능하다. 이에 따라오는 자연스러운 생각, 최고의 다각화된 포트폴리오를 계산한다면 어떨까. 이것이 [Harry Markowitz](https://ko.wikipedia.org/wiki/%ED%95%B4%EB%A6%AC_%EB%A7%88%EC%BD%94%EC%9C%84%EC%B8%A0)가 CAPM을 생각해낸 이유일 것이다.

### 4.2 CAPM

`CAPM`: Capital Asset Pricing Model, [자본자산 가격결정 모형](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B3%B8%EC%9E%90%EC%82%B0_%EA%B0%80%EA%B2%A9%EA%B2%B0%EC%A0%95_%EB%AA%A8%ED%98%95)

자본자산의 기대수익과 위험의 관계를 설명하는 모형.  
즉 자본자산평가 모델은 개별종목의 총위험을 시장에 연관되어 나타나는 위험(체계적 위험)과 시장과 상관없이 나타나는 위험(비체계적 위험)으로 분류하고 시장과 상관없이 나타나는 위험은 분산투자에 의해 제거될 수 있다고 본다.

![CAPM](/assets/images/post-2022-04-17/CAPM.png){: width='400'}

CAPM에서 위험-수익의 관계를 베타(β)로 함축적으로 확인 가능하다.

### 4.3 Risk & Return Pyramid

 ![Risk and Return Pyramid](/assets/images/post-2022-04-17/fm-w1-4.png)

### 4.4 Equity Premium Puzzle

미국 주식의 200년 연평균 성장률은 6.6%. 반면 미국 단기국고채 수익률은 같은 기간 2.7%. 즉, 주식 프리미엄은 3.9%에 달한다. 어떻게 가능했을까?

전세계 주식시장 수익률 중간값은 연 0.8%에 불과. 즉, 미국 자본시장의 성공이 이례적이었으며 위의 질문은 Selection bias에 속함을 알 수 있음.

> 미국 시장에 반하지 말라는 워런버핏의 선견을 알 수 있는 대목인듯. 반면 미국 시장에 투자했기 때문에 성공했다고 볼 수도 있을 듯. 결국 어떤 시장을 택하는가가 성공의 가장 큰 핵심이 될 수도 있을 듯.

### 4.3 Short Sales

보유주식를 음의 값을 가질 수 있음 &rarr; 공매도 (Short Sale)

### 4.4 Calculating the Optimal Portfolio

1. 기대수익 : 개별 자산의 보유 비율에 따른 기대수익의 합
2. 위험도 : 보유 비율에 따른 표준변차와 위험자산 간 공분산의 합
	* **Negative Covariance(음의 공분산) 포함 시, 전체 위험도는 감소**
	* 즉, 기대수익을 높이면서 전체 자산위험은 감소시키는 것이 가능

 ![Optimal Portfolio Calc 1](/assets/images/post-2022-04-17/fm-w1-5.png)
 
 ![Optimal Portfolio Calc 2](/assets/images/post-2022-04-17/fm-w1-6.png)

### 4.5 Efficient Frontier

1. 포트폴리오 구성에 따라 위험과 기대 수익이 변화한다. 이는 개인의 위험회피 성향에 따라 변화 가능하다.
2. Efficient Frontier, 즉 최적포트폴리오 이하의 자산구성은 더 나은 구성을 위해 노력해야 한다. 반면 Frontier line 외곽을 성취하는 것은 불가능하다.
3. 여러 자산을 포함함으로써 Efficient Frontier를 위로 밀어낼 수 있다. 가령 원자재를 포함할 경우, 동일한 위험에서 더 높은 수익을 기대할 수 있다.

 ![Efficient Frontier 1](/assets/images/post-2022-04-17/fm-w1-7.png)

 ![Efficient Frontier 2](/assets/images/post-2022-04-17/fm-w1-8.png)

### 4.6 [Gordon Growth Model](https://www.investopedia.com/terms/g/gordongrowthmodel.asp)

`고든성장 모형, GGM` : 일정한 성장률을 갖는 자산에 대한 현재가치 산출법
~~~
Pv = X / (r - g)
현재 자산가치 평가액 = 배당액 / ( 할인률 - 성장률 )

g: 성장률 (또는 배당금 기대성장률)
r: 할인률 Discount rate (또는 회사의 자기자본 고정비용 혹은 기대수익률)
~~~

* r은 Risk 요소이다. 무위험 자산일 경우 r = 무위험수익률, 위험자산 일 경우 beta값을 통해 r값 상승되어 현재평가가치 하락된다.
* g가 (-)라도 현재가격이 평가가치보다 낮다면 투자할 가치가 있다.