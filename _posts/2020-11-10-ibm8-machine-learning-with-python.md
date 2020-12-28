---
layout: post
title: Machine Learning with Python
subtitle: Course summary - IBM Data Science - 8 Machine Learning with Python
categories: StudyNote
tags: [Data Science, Coursera, IBM, Machine Learning, Python, 정리노트]
---

*본 포스트는 [IBM Data Science 특화 과정][coursera-ibm-ds] 중 [8. Machine Learning with Python][coursera-ibm-ds-8]에 대한 정리노트입니다.*

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
  * [Reg-Simple-Linear-Regression][ipynb-8-reg-1]
  * [Reg-Multiple-Linear-Regression][ipynb-8-reg-2]
  * [Reg-Polynomial-Regression][ipynb-8-reg-3]
  * [Reg-NoneLinearRegression][ipynb-8-reg-4]

[ipynb-8-reg-1]: https://github.com/jamescbjeon/ibmDS/blob/master/8/ML0101EN-Reg-Simple-Linear-Regression-Co2.ipynb
[ipynb-8-reg-2]: https://github.com/jamescbjeon/ibmDS/blob/master/8/ML0101EN-Reg-Mulitple-Linear-Regression-Co2.ipynb
[ipynb-8-reg-3]: https://github.com/jamescbjeon/ibmDS/blob/master/8/ML0101EN-Reg-Polynomial-Regression-Co2.ipynb
[ipynb-8-reg-4]: https://github.com/jamescbjeon/ibmDS/blob/master/8/ML0101EN-Reg-NoneLinearRegression.ipynb

[ipynb-8-reg-5]: https://github.com/jamescbjeon/ibmDS/blob/master/8/
[ipynb-8-reg-6]: https://github.com/jamescbjeon/ibmDS/blob/master/8/
[ipynb-8-reg-7]: https://github.com/jamescbjeon/ibmDS/blob/master/8/


***

## 1 Introduction to Machine Learning

### 1.1 Welcome

### 1.2 Introduction to Machine Learning

* What is machine learning?
  * **Machine learning** is the subfield of computer science that gives computer the ability to learn **without being explicitly programmed**.  - *Arthur Samuel*
  * 기계 학습이란 **명시적(explicitly)으로 프로그래밍하지 않고도** 컴퓨터에 학습 할 수 있는 능력을 부여하는 컴퓨터 과학의 하위 분야입니다.

> 즉 모든 코드를 일일이 작성하지 않더라도 해당 알고리즘이 내재한 규칙을 찾아내고 이를 통해 새로운 예측을 만들어 낼 수 있음.

* Major Machine Learning Technique

| Type       | Technique | Description | Example |
| ---------- | --------- | ----------- | ------- |
|Supervised  |Regression<br>/Estimation|Predict continuous values |집값 예측<br>자동차 모델에 따른 CO2 배출량 |
|Supervised  |Classification|Predict discrete class labels or categories |종양이 음성/악성 여부를 판단 |
|Unsupervised|Clustering|데이터의 구조 파악<br>Summarization|대출 상환 가능성 확인을 위한 은행 고객 분류(segmentation) |
|Unsupervised|Associations|함께 빈번히 발생하는 항목/사건 발견 |마트에서 같이 구매하는 항목 묶기 |
|Unsupervised|Anomaly detection|이상하거나 특이한 사건 확인|신용카드 사기 확인 |
|Unsupervised|Seqeunce mining|다음에 발생할 사건 예측 |Web-site에서 Click-stream 분석 |
|Unsupervised|Dimmension reduction|데이터 크기 축소|(ex) PCA|
|Unsupervised|Recommendation systems|관심사 분석 및 추천|Netflix 추천 시스템 |

* AI vs. Machine Learning vs. Deep learning
  * Artificial intelligence >> Machine Learning >> Deep Learning

> 기계학습은 인공지능의 한 분야이며, Deep learning 역시 기계학습의 진보된 한 분야로 볼 수 있음.


### 1.3 Python for Machine Learning

* Python libraries for machine learning
  * Numpy
  * SciPy
  * matplotlib
  * pandas
  * scikit-learn

### 1.4 Supervised vs. Unsupervised

|                  | Supervised | Unsupervised |
| ---------------- | ---------- | ------------ |
|Example           | Regression<br>- Predict trends using previous labeled data|Clustering<br>- Finds patterns and groups from unlabeled data|
|Evaluation method | Many | Less |
|Environment       | Controlled | Less controlled |

* Supervised learning
  * We **teach the model** then with that knowledge, it can predict unknown or future instances.
  * Training 필요
    * **Labeled** dataset --> Train --> Build model --> Evaluation --> Prediction

* Unsupervised learning


## 2 Regression

### 2.0 Introduction to regression

* Regression : The process of predicting a continuous values

|            | simple X          | multiple Xs        |
| ---------- | ----------------- | ------------------ |
| Linear     | Simple linear     | Multiple linear    |
| Non-linear | Simple non-linear | Multiple nonlinear |

### 2.1 Linear regression

### 2.2 Non-linear regression



***

## 3 Classification

***

## 4 Clustering


***

## 5 Recommender System


***

## 6 Final Project




[coursera-ibm-ds]: https://www.coursera.org/professional-certificates/ibm-data-science
[coursera-ibm-ds-6]: https://www.coursera.org/learn/data-analysis-with-ipynb/home/welcome

[ibm1]: https://jamescbjeon.github.io/studynote/2020/09/29/ibm1-what-is-data-science.html
[ibm2]: https://jamescbjeon.github.io/studynote/2020/10/05/ibm2-tools-for-data-science.html
[ibm3]: https://jamescbjeon.github.io/studynote/2020/10/12/ibm3-data-science-methodology.html
[ibm4]: https://jamescbjeon.github.io/studynote/2020/10/19/ibm4-python-for-ds-n-ai.html
[ibm5]: https://jamescbjeon.github.io/studynote/2020/10/26/ibm5-databases-n-sql-for-data-science.html
[ibm6]: https://jamescbjeon.github.io/studynote/2020/11/03/ibm6-data-analysis-with-python.html
[ibm7]: https://jamescbjeon.github.io/studynote/2020/11/07/ibm7-data-visualization-with-python.html
[ibm8]: https://jamescbjeon.github.io/studynote/2020/11/10/ibm8-machine-learning-with-python.html
[ibm9]: https://jamescbjeon.github.io/studynote/2020/11/17/ibm9-applied-data-science-capstone.html
