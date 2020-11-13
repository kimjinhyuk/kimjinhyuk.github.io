---
layout: post
title: Linear Regression (선형회귀) - Machine Learning
excerpt: "In statistics, linear regression is a linear approach to modeling the relationship between a scalar response and one or more explanatory variables. The case of one explanatory variable is called simple linear regression. For more than one explanatory variable, the process is called multiple linear regression."
categories: [Machine Learning]
use_math: true
comments: true
tag: [AI, 파이썬, Python, Machine Learning, Linear Regression]
---

## 머신러닝

* 머신러닝에서는 크게 지도학습(Supervised learning), 비지도 학습(Unsupervised Learning), 강화 학습(Reinforcement Learning)으로 나눌 수 있다.

Classification     |  Regression  
:------------:|:---------------------:
kNN           |  Linear Regression
Naive Bayes  |  Locally Weighted Linear
upport Vecto | Locally Weighted Linear
Support Vector| Ridge
Machine Decision | Lasso

지도학습 중에서 Linear Regression (선형회귀) 대해서 확인해 보겠습니다.

## Linear Regression (선형회귀)

  * 어떤 자료에 대해서 그 값에 영향을 주는 조건을 고려하여 구한 평균 
(어떤 데이터들이 굉장히 크거나 작을지라도 전체적으로 이 데이터들은 전체 평균으로 회귀하려는 특징이 있다는 통계학 기법)
시험 공부하는 시간을 늘리면 늘릴 수록 성적이 잘 나옵니다. 하루에 걷는 횟수를 늘릴 수록, 몸무게는 줄어듭니다. 집의 평수가 클수록, 집의 매매 가격은 비싼 경향이 있습니다. 이는 수학적으로 생각해보면 어떤 요인의 수치에 따라서 특정 요인의 수치가 영향을 받고있다고 말할 수 있습니다. 조금 더 수학적인 표현을 써보면 어떤 변수의 값에 따라서 특정 변수의 값이 영향을 받고 있다고 볼 수 있습니다. 다른 변수의 값을 변하게하는 변수를 $x$, 변수 x에 의해서 값이 종속적으로 변하는 변수 $y$라고 해봅시다.

이때 변수 $x$의 값은 독립적으로 변할 수 있는 것에 반해, $y$값은 계속해서 $x$의 값에 의해서, 종속적으로 결정되므로 $x$를 독립 변수, $y$를 종속 변수라고도 합니다. 선형 회귀는 한 개 이상의 독립 변수 $x$와 $y$의 선형 관계를 모델링합니다. 만약, 독립 변수 $x$가 1개라면 단순 선형 회귀라고 합니다.

  * 단순 선형 회귀
    * \( y=ax+b \)
        * a : 기울기
        * b : 절편
  * 다중 선형 회귀
    * \( y = h(x_1, x_2, x_3, ..., x_k; W_1, W_2, W_3, ..., W_k) + \epsilon \)
    * $h()$ : 조건에 따른 평균을 구하는 함수 (회귀 모델)
      * x : 어떤 조건(특성)
      * W : 각 조건의 영향력(가중치)
      * e : ‘오차항’을 의미. 다양한 현실적인 한계로 인해 발생하는 불확실성으로 일종의 잡음(noise)

    최소제곱법

    * 최소제곱법, 또는 최소자승법, 최소제곱근사법, 최소자승근사법(method of least squares, least squares approximation)은 어떤 계의 해방정식을 근사적으로 구하는 방법으로, 근사적으로 구하려는 해와 실제 해의 오차의 제곱의 합이 최소가 되는 해를 구하는 방법이다. 이 방법은 값을 정확하게 측정할 수 없는 경우에 유용하게 사용될 수 있으며, 특히 그 계의 방정식이 어떤 형태인지를 알고 있을 때 방정식의 상수 값들을 추정하는 데에 사용된다.

    * \( a=\frac { (x-x평균)(y-y평균)의 합 }{ { (x-x평균) }^{ 2 }의 합 } \)

{% highlight python %}
# 오차가 최저가 되는 직선
import numpy as np
# 기울기 a를 최소제곱법으로 구하는 함수
def compute_a(x, y, mean_x, mean_y):
    # 분자 부분
    dividend = 0
    for i in range(len(x)):
        dividend += (x[i] - mean_x) * (y[i] - mean_y)

    # 분모 부분  
    divisor = sum([(i - mean_x)**2 for i in x])
    a = dividend / divisor
    return a

mx = np.mean(x)
my = np.mean(y)

a = compute_a(x, y, mx, my)  # 기울기
b = my - (mx * a)            # 절편

y1 = [a * x1 + b for x1 in x]

plt.grid(True)
plt.plot(x, y, 'bo')
plt.plot(x, y1, 'r-o')
plt.show()
{% endhighlight %}

![](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/img/LinearRegression01.PNG?raw=true)


  * 비용함수 (Cost / Cost function) : 그려진 직선 Hypothesis(H(x))와 실제 데이터(y)의 차이
      + Cost = H(x) - y에 데이터를 대입하여 Cost의 총합을 구하는 것이 가능
      + Cost의 총합이 작은 Hypothesis일수록 데이터를 잘 대변하는 훌륭한 Linear Regression
      + Cost는 양수일 수도, 음수일 수도 있기에 이러한 문제를 방지하고자 총합을 구할 때 Cost값을 제곱하여 평균을 내는 방식 (평균제곱오차, MSE, Mean Squared Error)을 사용

      $$ cost(W,b)=\cfrac { 1 }{ m } \sum _{ i=1 }^{ m } { (H({ x }^{ (i) })-{ y }^{ (i) }) }^{ 2 } $$

      $$ H(x)=Wx+b $$

      머신러닝(or 딥러닝)에서 learning의 목적은 Cost를 정의하고 이를 최소화하는 것


출처 : [광주인공지능 사관학교 - Machine Learning 수업]() , [딥 러닝을 이용한 자연어 처리 입문](https://wikidocs.net/21670)
