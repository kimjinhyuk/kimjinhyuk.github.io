---
layout: post
title: 머신러닝에서 자주 쓰이는 미분(differentiation)
excerpt: "머신러닝 / 딥러닝 에서 자주 쓰이는 함수의 미분"
categories: [수학]
use_math: true
comments: true
tag: [AI, Mathematic, differentiation]
---

미분 (differentiation)  
  
## 머신러닝 / 딥러닝 에서 자주 쓰이는 함수의 미분  
  
상수를 미분 하면 - 상수가 미세하게 변할 때 함수의 변화는 없다  
  
$f(x) = constant$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10132;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   $f'(x) = 0$  
  
지수에 있던 n 앞으로 나오고 지수는 1개 감소한다  
$f(x) = ax^n$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10132;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $f'(x) = nax^{n-1}$  
  
자연상수를 미분하면 자기자신  
  
$f(x) = e^x$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10132;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $f'(x) = e^x$  
  
자연 로그를 미분하면 1/x  
  
$f(x)=ln{x}$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10132;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $f'(x) = {1 \over x}$  
  
$f(x) = e^{-x}$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10132;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $f(x) = -e^{-x}$  
  
위 수식은 언제든지 나오는 수식이라 암기해놓아야 한다.  
  
ex) $f(x) = 3x^2 + e^x + 7$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10132;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $f'(x) = 6x + e^x$  
  
ex) $f(x) = ln{x} +{1 \over x}$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10132;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ${1 \over x} = x^{-1}$  
  
---
변수 x 에 대한 편미분  
  
$f(x,y) = 2x+3xy+y^3$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10132;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ${\frac {\partial f(x,y)}{\partial x}} = {\frac {\partial (2x+3xy+y^3)}{\partial x}}=2+3y$  
  
변수 y 에 대한 편미분  
  
$f(x,y) = 2x+3xy+y^3$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10132;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;${\frac {\partial f(x,y)}{\partial x}} = {\frac {\partial (2x+3xy+y^3)}{\partial y}}=3x+3y^2$
  
체중 함수가 '체중(야식,운동) 두개의 변수를 가지고 편미분을 이용하면 각각 변수 변화에 따라 체중변화를 예측할 수 있다.   
  
현재 먹는 **야식의 양**에서 조금 변화를 줄 경우 체중은 얼마나 변하는가     

$${\frac {\partial 체중}{\partial 야식}} $$   

현재 하고 있는 **운동량**에서 조금 변화를 줄 경우 체중은 얼마나 변하는가   
  
$${\frac {\partial 체중}{\partial 운동량}} $$  

---  
연쇄법칙 ( chain rule )  -  합성함수란 여러 함수로 구성된 함수로서, 이러한  합성함수를 구성하는 각 함수의 미분의 곱으로 나타내는 연쇄법칙을 이용  

ex1) $f(x) = e^{3x^2}$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10132;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 함수 $e^t$ , 함수 $t = 3x^2$ 
* $f(x) = e^{3x^2}$ 를 연쇄법칙으로 미분하는 경우, $t = 3x^2$ 으로 놓으면 $f(x) = e^t$
	* ${\frac {\partial f}{\partial x}}$ = ${\frac {\partial (e^t)}{\partial t}}$ ${\frac {\partial (3x^2)}{\partial x}}$ = $(e^t)(6x)$ = $(e^{3x^2})(6x) =6xe^{3x^2}$

ex2) $f(x) = e^{-x}$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10132;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 함수 $e^t$ , 함수 $t = -x$
* $f(x) = e^{-x}$ 를 연쇄법칙으로 미분하는 경우, $t = -x$ 으로 놓으면 $f(x) = e^t$
	* ${\frac {\partial f}{\partial x}}$ = ${\frac {\partial (e^t)}{\partial t}}$ ${\frac {\partial (-x)}{\partial x}}$ = $(e^t)(-1)$ = $(e^t)(-1)$ = $-e^{-x}$

  
<iframe width="560" height="315" src="https://www.youtube.com/embed/PnQe3-6812k" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>