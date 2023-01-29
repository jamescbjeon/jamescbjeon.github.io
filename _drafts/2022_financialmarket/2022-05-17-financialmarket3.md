---
layout: post
title: Interest, Stock and Dividend
subtitle: Financial Markets - Week 3
categories: Investment
tags: [로버트 실러, PDV, Dividend, Coursera]
---

Rober J. Shiller 교수님의 [Financial Market 강좌]({% post_url 2022-04-17-financialmarket0 %}) 중 3주차 요약이다. 채권과 이자, 그리고 주식과 배당에 대해 공부한다.

## 0 Goal

1. Interest 이자
	* 단기 이자율의 영향 및 제도, 그리고 단리 및 복리 이자 계산법
	* 쿠폰(Coupon)과 할인채(Discount bond)의 차이 및 현재 할인가치(PDV) 산정법
	* 영구채(Consol)과 연금(Annuity) - 두 가지 채무증권의 출처, 의미 및 가치
	* 선도금리(Forward rate)의 의미 및 계산법 
2. Stock and Dividend 주식과 배당
	* 기업 시가 총액, Market Cap의 의미 및 계산법
	* 미국 내 법인의 구조와 회사 주식을 소유하는 것의 의미
	* 보통주와 우선주의 차이, 주가희석 Dilution 및 배당의 개념
	* 자사주 매입 Stock Repurchase
	* 기업 지배구조
	* 주식의 가격 결정과 주가수익비율(P/E ratio)


## 1 Interest and Market

### 1.1 Federal Funds and Interest Rates

Federal Funds, 연방기금금리 : 꽤 긴 기간동안 제로금리 수준 유지하다 최근 인상 중

<iframe src="https://fred.stlouisfed.org/graph/graph-landing.php?g=OmUO&width=670&height=475" scrolling="no" frameborder="0" style="overflow:hidden; width:670px; height:525px;" allowTransparency="true" loading="lazy"></iframe>

<br>
[EONIA - European Over Night Index Average](https://www.euribor-rates.eu/en/eonia/) : 마이너스 금리로 상당기간 유지 중. 돈을 빌려주면 오히려 원금 손실 상황!

### 1.2 Compound Interest, 복리

~~~
balance = (1 + r)^t
# interest rate: r, 이자횟수: t

연간 2회 이자지급 시, (1 + r/2)^2t
연간 n회 이자지급 시, (1 + r/n)^nt

n이 무한대, 즉 연속함수일 경우, lim (1 + r/n)^nt = e^rt
~~~

### 1.3 Discount Bonds, 할인채

채권은 정해진 금리로 이자 지급 = `쿠폰`

~~~
# YTM, Yield to Maturity (만기 수익율) = r
# 만기까지 남은 기간 = T

P = 1 / (1+r)^T

YTM = t-root(Face value / Current value) - 1 = t-root(1/P) - 1
~~~

### 1.4 Consol and Annuity, 영구채와 연금

`Consol` : 영구채, 만기가 없음
* 영국정부가 발행. 여전히 지급하고 있음
* 영구채도 완벽하게 안전하지 않음. 발행 주체의 Default risk를 제외하더라도 시장가 변동은 발생한다 (할인율이 변하므로). ~~*발행주체가 영원하더라도 사람은 영원히 살지 않는다*~~
* 땅도 일종의 영구채로 취급할 수 있을 듯
 
`Annuity` : 연금
* 사람은 죽지만 기한이 정해지지 않은 연금은 일종의 영구채로 취급 가능

~~~
### 영구채 및 연급 현재가치 계산법

1) Consol PDV = coupon / r
2) Growing Consol PDV = coupon / (r-g)
3) Annuity PDV = coupon x (1 - 1/(1+r)^T) / r

# coupon 수익, r 할인율
# g 쿠폰성장률 : r = g일 경우, 영구채 가치는 무한대가 된다.
~~~

### 1.5 [Forward Rates](https://cparoh.tistory.com/4) and [Expectation Theory](https://www.investopedia.com/terms/e/expectationstheory.asp)

현재 시점 이자율 = 현물이자율, `Spot rate`  
미래 일정시점 이자율 = 선도이자율, `Forward rate`

~~~
### 선도이자율 계산
(1 + r2)^2 = (1 + r1) x (1 + f2)

# r1 = 1년이자율, r2 = 2년이자율
# f2 = 2년시점 1년 선도이자율
~~~

단기 이자율의 중첩이 만기 이자율과 같다는 간단한 가정으로 계산 가능  
단, 장기채권에 대한 Risk Premium 고려가 없으므로 선도이자율을 과장되게 표현되는 단점이 있다.


### 1.6 Inflation, 인플레이션

명목금리(Nominal rate)는 화폐, 즉 달러로 표현. 반면 실질금리(Real rate)는 시장바구니(Market basket)로 체감

~~~
실질금리 = 명목금리 - 인플레이션
r-real = r-money - inflation
~~~

`TIPS`, [Treasury Inflation Protection Securities - 미국 물가연동채권](https://korealtyusa.com/%EB%AC%BC%EA%B0%80%EC%97%B0%EB%8F%99%EC%B1%84%EA%B6%8C/) 

대부분의 나라가 물가연동채권이 있으며, 대한민국도 [물가연동국고채](https://ktb.moef.go.kr/prcstatIntrlckNtpbnd.do)를 운영 중. 소비자물가지수에 연동되어 원금이 동일하게 상승한다.

### 1.7 Leverage

`레버리지` : 현재 가지고 있는 것보다 더 많은 돈을 자산에 투자하는 것  
*기회를 극대화 하지만, **위험도 같이 증가시킨다***

2008 금융위기는 주택구매자들의 레버리지에 기인  
중국 부채비율은 160%로 미국 70%에 비해 높다. 높은 성장률을 구가하나, 위기에는 취약하다.  
부채는 파산으로 이어지고, 세계 경제 위기의 단초가 된다

디플레이션 : 실질적 부를 채무자에서 채권자로 이동  
디플레이션 &rarr; 화폐가치상승 &rarr; 빚가치 증가 &rarr; 부의 이동 - 채권자 to 채무자 = 아무도 빚을 지려하지 않는다!


## 2 주가와 배당

### 2.1 Market Cap by Country

Stock Market Cap by Country 2014

| Country | %GDP | US$ trillions |
| --- | --- | --- |
| United States | 151% | 26.33 |
| Canada | 107% | 3.183 |
| China | 58% | 6.004 |

* America is in sale. 미국 주식시장은 미국이 아니다. 전세계 수많은 경제 주체에 의해 소유되고 있다.
* 미국 주식시장의 자본화율은 캐나다 또는 중국을 크게 앞선다. 매력적인 시장으로 투자자에게 비춰지고 있음.

미국 가구가 소유한 보통주는 13.9조 달러. 반면, 부동산 보유는 23.7조 달러. 집을 사지 않고 임대한 후 다각화한 포트폴리오에 투자하면 덜 위험하고 더 현명하지 않을까. 그렇게 하지 않는 이유는?

### 2.2 The Corporation 법인

법인. 법적인 인간. 자연인, 즉 사람과 대비
법적으로 사람과 동일한 권리와 의무를 지게된다.

주주 Shareholder --> 이사회 Board of Directors --> CEO

Board of Directors 이사회
* Shareholder's Democracy - 1주 당 1개의 투표권
* CEO에 의해 주최되며, 이사회는 CEO를 선임함
* 독일에서는 감독이사회 (Aufsichstrat), 경영이사회 (Vorstand)로 분리되어 있음

### 2.3 Share and Dividends

My ownership of company (회사 지분율) = My shares divided by total shares 

Splits (액면분할) - 근본적으로 변화 없음

배당을 할 경우, 배당만큼 주가 하락 : 배당락

Ex dividend date : 배당 기준일

주식보유의 기본 사유 = 배당금. 단, 배당지급은 의무가 아님
배당금 누락이 없고 장기적 증가가 주주 신뢰에 중요

### 2.4 Common vs. Preferred - 보통주 vs. 우선주

Common stock, 보통주 : 일반적인 권리. 회사 지분을 갖음. Equity와 동일한 의미
Preferred stock, 우선주 : 배당금 지급은 의무가 아니나 보통주 배당 전 반드시 먼저, 그리고 이상의 배당을 우선주에 할당해야 함. 단, 회사지분 권리는 갖지 못함.
Corporate bonds, 회사채 : 지급해야할 이자(Coupon)과 만기(Maturity date)가 있는 회사 채권

2008년 금융위기 때 US정부에서 GM 등의 우선주를 대거 구입한 이력이 있음. 보통주를 안 산 이유는 자본주의의 원칙을 지키기 위해. 

### 2.5 Corporate Charter

기업정관 - 모든 일반주주는 동등하게 대우 받는다
배당금 지급은 의무가 아니나, 주당 배당금을 동일해야함. Equity라는 단어가 생긴 이유. 주주들의 평등을 의미.
따라서 이사회 결정이 중요

신주인수권
전환사채

주주민주주의는 실제로 이루어지기 어렵다. 의무감에 행동하기 힘들기 때문. 일부 대주주를 위해 회사가 운영될 가능성이 있다. 대한민국 현실과 비슷.
Ownership is so widely scattered that working control can be maintained with but a minority interest.

위임장경쟁 Proxy contest - 1935년 SEC에서 허용

Class of shares
주식의 Class가 있으며 차등 의결권을 인정하기도 함

### 2.6 Corporations raise money

1. Retained Earning 이익잉여금
2. Loan 대출 & Bond 채권
3. Issue shares 신주발행

Dilutes, 주가희석 - 주주가치는 희석. 그러나 회사입장에서는 비용 없는 차입

Pecking Order Theory, 자금조달순서 by Stuart Myers
1) 이익잉여금, 2) 차입, 3) 신주발행
신주 발행 시 주가하락으로 경영진 불신의 문제가 생기므로 가장 후순위
칼 막스의 지적: 신주발행은 제한되고 기존 주식을 가지고 도박판이 벌어진다. 모두 시세차익에만 관심을 둔다.
실제로 93-02년간 주식 시장 호황으로 많은 신주발행이 이루어짐. 

### 2.7 Dilution 주가희석 / Share Repurchase 자사주 매입

Dilution
배당금 대신 주식을 배당 --> 실제 지분율 변화 X --> 주가 희석

Share Repurchase
배당소득세 15%를 회피할 수 있어 최근 점차 증가하는 추세
양도소득세 (Capital gained tax)는 주식 매도를 하지 않으면 미부과. 따라서 과세 이연 효과 존재.

### 2.8 PDV of Expected Dividends

GGM, Gordon Growth Model
P = D / (r-g) 
D : 배당금
r : 주주요구수익률 (이자율, 할인율)
g : 수익 증가율 (배당 성장율)

CAPM, 효율적 시장가설은 'r'과 'g'로 가격변화를 설명
낮은 Price는 주식 세일을 의미하는 것이 아니라 성장율이 하락하였거나 (Low g) Risk가 올라감을 의미 (high r)
가치투자자들은 낮은 Price에서 투자하는 것을 선호

### 2.9 Why do firms pay dividends?

Dividend signalling 신호이론
회사가 스스로의 재무상태를 보여주려는 의도 - 배당이 "0"일 경우, 재정상의 큰 문게가 의심. 적자를 봐도 배당하는 경우가 있다.

하버드 전임 학장 - 4년 대학교육은 신호탄일 뿐. 증명을 위한 기간. 무엇을 위한 증명?
1) 입학 가능 수준의 스마트함
2) 4년을 버틸 수 있는 성실함

[Course material - Week 3]({{ site.url }}/assets/pdf/financialmarket/financialmarket_w3.pdf)  
[Coursera - Financial Market - Week 3](https://www.coursera.org/learn/financial-markets-global/home/week/3)