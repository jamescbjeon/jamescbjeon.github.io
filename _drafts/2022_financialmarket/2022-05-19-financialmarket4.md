---
layout: post
title: Mortgage, Financial Crisis and Regulation
subtitle: Financial Markets - Week 4
categories: Investment
tags: [로버트 실러, Mortgage, 2008 금융위기, Coursera]
---

Rober J. Shiller 교수님의 [Financial Market 강좌]({% post_url 2022-04-17-financialmarket0 %}) 중 4주차 요약이다. 부동산과 주택담보 대출로 시작하여, 이로 인한 2008년 금융위기가 어떻게 발생되었는지를 돌아본다. 이를 통해 적절한 금융 규제의 필요성 및 규제 기관의 역할에 대해 알아본다.

## 0 Goal

1. 주택담보대출 Mortgage
	* DPP와 REIT의 차이점
	* 담보 대출
	* 10년 만기 국고채 YTM - 30년 만기 주택담보대출 금리 사이의 관계
2. 2008 금융위기
	* 거품 이전의 주택 시장과 2007년 폭락의 원인
	* CMO 및 CDO 정의
3. 금융 규제 Regulation
	* 미시적 그리고 거시적 신중성 규제
	* 터널링
	* 미국의 주, 국가 규제 및 SEC
	* 선행 투자, 중개업 실패 등이 주식 시장 미치는 영향과 예시
	* 규제 기관의 역할


## 1 Mortgage

### 1.1 Commercial Real Estate Vehicles

상업용 부동산 투자 방법 - DPP & REITs

1. `DPP`, Direct Participation Program
	* 부동산 동업 (Real Estate Partnership)
	* 일정한 기간 한정, 소액 투자 불가능 (부자들만 가능)
	* 1986년까지는 실질적 투자목적보다 세금 보정 목적이 더 컸음
2. `REITs`, Real Estate Investment Trusts
	* 부동산 투자 신탁
	* 소규모 투자자를 위한 부동산 투자 모임, 안전을 위한 규제 있음
	* 법인세를 내지 않는 혜택. 따라서, 기업은 리츠라고 칭하는 것은 불가
	* 법인세 혜택 악용을 막기 위해 리치를 아래처럼 별도 정의
		* 자산의 75% 이상은 부동산 또는 현금이어야 함
		* 수입의 75% 이상은 부동산에서 나와야 함
		* 수입의 90% 이상은 부동산,  배당, 이자, 양도소득에서 나와야 함
		* 수입의 95%는 사용되어야 함. 배당률이 이미 법으로 정해짐

### 1.2 Mortgages

`Mortgage`: 주택담보대출, 이자나 원금 상황을 멈추면 주택을 담보로 가져감

2008년 금융위기 시
* 주택 시장 침체로 모기지 대출금보다 집값 하락 발생  
* 주택 포기가 오히려 유리했으며, 상환 불능상태 (Non-recall state)인 사람들이 실제로 실행
* 물론 대부분은 버티며 상환 &rarr; 마이너스 자산 상태 &rarr; 소비 하락 &rarr; **경기 침체**

`FHA`, Federal Housing Administration : 연방주택 관리국

30년 만기 주택담보대출 이자율 vs. 10년 만기 미국 연방정부 국고채권 만기 수익률 : 서로 강하게 연동되며 스프레드 차이에 의해 주택 경기 판단 가능

![10yTR-30yMORT rate](/assets/images/post-2022-04-17/fm-w4-1.png)

### 1.3 PMI, CMOs, CDOs

`PMI`, Private Mortgage Insurance : 주택담보대출보험   
* Fannie & Freddie가 주택담보대출 취급 중 발생하는 손실의 보험 (MGIC 같은 회사가 제공)
* Down payment (계약금)이 주택가격의 20% 미만일 경우, Mortgate 받을 때 PMI 비용도 부담 필요
* 집값 하락으로 LTV (Loan To Value ratio), 대출 잔액이 주택가격의 80% 미만일 경우 PMI 지불 불필요. 반대로 집값 상승으로 LTV 80% 초과할 경우에느 PMI가 요청되지는 않는다 (제도의 허점)
* 물론 PMI 회사가 파산하기도 함

`CMO`, Collateralized Mortgage Obligations : 주택담보대출(모기지) 담보부 증권 
* 모기지를 여러 개의 Tranche (트랑쉐)로 나눠 투자가능하도록 유동화
* 상위 트랑쉐는 하위 트랑쉐가 모두 채무 불이행될 때까지 영향 없도록 설계
* AAA, AA 등급은 문제 없을 것으로 여겨졌으나 믿음이 깨지면서 금융위기 발생

`CDO`, Collateralized Debt Obligations : 대출 담보부 증권
* 주택담보대출 뿐 아니라 광범위한 대출에 대한 담보부 증권
* 서프프라임 모기지를 많이 담고 있었음.
* 금융위기 당시 평가사가 제대로 Downgrading 하지 않은 것에 대한 비판 있었음

> 금융위기 때 CDO/CMO 가격 급락  
> AAA 트랑쉐는 물론 AAA 등급은 아니었으나 이후 떨어진 가격만큼 나쁘지도 않음  
> 모든 투자자는 똑똑해야 할 필요가 있음. 모든 가격은 항상 제대로 책정되는 것은 아님. 종종 효율적 시장가설은 실패하기도 함

## 2 Financial Crisis in 2008

### 2.1 Recessions

> 불황은 실질적으로 심리적인 것이며, 우울증에 걸려 정신과 의사에게 가는 것과 유사하다.  중앙은행 및 정부가 빠른 시일 내에 개선하기는 쉽지 않다.

[장단기 금리역전](https://www.chosun.com/economy/economy_general/2022/04/03/7TSDCIZ3FHG3KQCRTUU2RYDTE/) - 경기 침체를 예견하는 주요지표

<iframe src="https://fred.stlouisfed.org/graph/graph-landing.php?g=PANj&width=670&height=475" scrolling="no" frameborder="0" style="overflow:hidden; width:670px; height:525px;" allowTransparency="true" loading="lazy"></iframe>

<br>경기침체는 실제로 일어나기 전까지는 항상 모호. 단, **실업률**의 급격한 상승은 경기침체의 분명한 신호

### 2.2 Bubble

![Home Price](/assets/images/post-2022-04-17/fm-w4-2.png)

* 2차 세계대전 종료 및 베이비붐 도래와 함께 주택가격 급상승
* 이후 80, 90년대에 일시적인 주택가격 버블 발생
* 80년대 이후로 건축비 상승은 없음. 건축기술 상승과 대량생산 기인
* 인구는 지속적으로 증가하고 있으나 주택가격 상승과는 큰 연관 없어 보임
* 1990년대 말까지 약 100년간 집값 상승은 제한적. 이후 급격한 상승 후 금융위기와 함께 급락

![Housing Start](/assets/images/post-2022-04-17/fm-w4-3.png)

주택가격 vs. 주택착공건수 : 가격에 따라 주택착공은 급격하게 요동치는 경향

![Home Price to Mortgage Spread](/assets/images/post-2022-04-17/fm-w4-1.png)

10년 후 주택가격 기대 상승률과 30년 모기지 이율간 스프레드 : 레버리지를 통한 강한 시세차익 기대 가능 &rarr; **주택가격 급등의 원인**

### 2.3 Post Crisis Regulation

Liar's loan, 즉 부적격자 대출이 금융위기를 촉발

유럽 의회 규제 : 주택담보대출 발행자는 발행한 담보대출 중 5%를 스스로 보유해야 한다. 즉, 판매 책임을 금융기관도 나눠갖도록 규정

Dodd-Frank 법 (2010)에서 해당 아이디어를 차용. 단, QRMs (Qualifying Residential Mortgages, 적격 주택담보 대출)은 해당 규정 미적용. ~~*근데 QRM은 무려 689페이지로 엄청나게 길게 정의되어 있음*~~


## 3 Misbehavior, Crises and Regulation

### 3.1 Regulation

> 왜 불공정행위가 발생할까?
> 모두가 그렇게 하니깐. 경쟁에서 퇴출되면 윤리는 이미 소용 없게 된다.

Regulation, 규제
* 주로 조작 혹은 사기들을 단속하기 위한 목적
* 시스템이 잘 작동하기 위한 목적으로 설정
* 피싱평형 : 서로 속이는 행위가 만연하면 결국 규제가 필요
* 스포츠의 심판과 비슷. 파울을 지적 당하면 싫지만 필요
* **Trade-off**를 갖게 됨. 필요하지만 너무 많은 제한은 생산성을 제한한다

### 3.2 Within-firm Regulation 기업내 규제

`The board of Directors`, 이사회가 내부 규제 역할을 함
* 사외이사는 사회 다양성을 대표. 보통 시간제 근무이며 평판이 좋은 인사로 채움

`Tunneling`, 터널링 - 몰래 터널을 파내 교묘한 횡령을 하는 것을 의미
* 회사 자산을 헐값에 매각
* 비정상가 거래 + 알 수 없도록 비이상적으로 긴 계약서
* 경영진 과다 보상
* 대출 보증
* 지인 등에게 회사 기회 탈취
* 물타기 신주발행
* 내부자 거래 - 호재/악재를 발표 전 미리 선점

### 3.3 Local Regulation 미국 주립정부 규제

`Blue Sky Law`, 창공법 (증권거래법)
* 전화주문이 가능해지며 사기행위 급증하며 제정
* Progressive Era : 20세기 초반 20년을 지칭. 여러 혁신이 발생한 시기

### 3.4 National Regulation 미국 연방정부 규체

`SEC`, Securities and Exchange Commission : 증권 거래 위원회
* 루즈벨트 뉴딜 일환으로 설립. 1934년
* 급진적인 기관으로 최초 인식
* 중요 원칙 - 대중공개 (Disclosure)
	* 상장기업에게 현재 상태에 대한 주기적인 공개를 요구. 이는 대중이 쉽게 접근할 수 있어야 함

`Edgar`, 재무제표 작성 프로그램
* 모든 공공회사에 대한 재무제표 조회 가능
* [sec.gov](https://www.sec.gov/)에서 확인

Private to Public Securities
* Initial Public Offering (IPO) : 대중 공개. SEC 감독을 받게 됨
* 반대로 상장취소도 가능
* 기본적으로 일반 공공투자의 경우, 모든 정보가 투명하게 공개되어야 한다는 원칙

SEC rules
* 모든 브로커는 SEC에 등록(Register)되어 있어야 함
* 모든 거래주식은 등록되어 있어야 함
* 모든 증권은 등록되어 있어야 함
* 등록이 SEC 승인을 의미하는 것은 아님

공정 거래법 위반
* 정보불균형을 대치하기 위해 내부자 거래 제한 필요
* 애널리스트에게 공개된 정보는 즉시 대중에게도 공개되어야 함
* 가짜 뉴스선동도 공정거래법 위반
* 선도거래 (Front running)을 통해 큰 거래량 이전 매수하여 시세차익을 얻을 수 있음

`GAAP`, Generally Accepted Accounting Principles : 일반 회계원칙
* `FASB` (Financial Accounting Standards Board)에서 정의
* Edgar에서 사용 중
* EBITDA 등은 GAAP에서 정의되지 않음. GAAP에 정의 되지 않은 회계 용어가 혼용되며 최근 혼란이 일부 있음

`SIPC`, Securities Inverstor Protection Corporation : 증권투자자보호공사 
* 1970년 창설
* 계좌당 50만 달러에 대해 투자자보호

Rating shopping (평가쇼핑) : 증권가치 평가 체계를 무력화 시키기도 함

### 3.5 International Regulation 국제 규제

`BIS`, Bank for International Settlements : 국제결제은행 (1930년 설립)

`Basel Committee` : 바젤위원회 
* 1974년 은행간 규제 조정을 위해 설립
* Basel I (1988) &rarr; Basel II (2004) &rarr; Basel III (2009)
* G7 (Canada, France, Germany, Italy, Japan, US, UK) 혹은 G20에 의해 주도

> 실러 교수님은 자유시장의 성공 비결은 규제라고 강하게 생각하심  
> Fair rule, 즉 공정한 규칙에서 공정한 경쟁 필요하며, 시장은 항상 제한범위 내에서 규제되어야 한다고 말씀하심.

[Course material - Week 4]({{ site.url }}/assets/pdf/financialmarket/financialmarket_w4.pdf)  
[Coursera - Financial Market - Week 4](https://www.coursera.org/learn/financial-markets-global/home/week/4)
