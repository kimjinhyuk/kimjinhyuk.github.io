---
layout: post
title: 함수 - lambda
excerpt: "함수(function) / lambda 함수를 만들때 사용하는 키워드 def를 사용하지 않고 함수를 작성하는 것을 말합니다"
categories: [파이썬]
use_math: true
comments: true
tag: [AI, 파이썬, Python, lambda]
---

## 함수 - lambda  

 * 람다(lambda)는 한 줄로 함수를 작성하는 방법으로, 익명(anonymous)함수 또는 람다 표현식(lambda expression) 등으로 불림

 * lambda는 파이썬에서 다른 함수의 input 인수(parameter)로 넣을 때 주로 사용되며, 특히 머신러닝에서미분을 계산하기 위해 필요한 수치 미분 (numerical derivative)과 신경망에서 필요한 활성함수(activation function) 등을 표현할 때 이용된다.
 수학에서 함수 표현처럼 $f(x)$ , $f(x,y)$ 등으로 사용되며, 마지막 표현으로 대체된다.

<center> 함수명 = lambda 입력1, 입력2, ... : 대체되는 표현식 </center>
{% highlight python %}
f = lambda x : x+100
for i in range(3):
  print(f(i))
# 100
# 101
# 102
{% endhighlight %}

{% highlight python %}
def print_hello():
  print("hello python")
def test_lambda(s,t):
  print("input ==", s, ", input2 ==", t)
s = 100
t = 200
#s, t 선언 및 할당 값이 없으면 error
fx = lambda x, y : test_lambda(s,t)
fy = lambda x, y : print_hello()

fx(500,1000) # fx(500,1000) = test_lambda(s,t)
fy(300,600)  # fx(300,600) = print_hello()
{% endhighlight %}

이처럼 람다에서 입력으로 받은 모든 변수가 대체되는 형식으로 사용되지는 않는다. test_lambda()에서는 입력받은 500,1000 인자값을 fx함수에서는 값을 사용하지 않는다.
print_hello()에서도 입력받은 300,600 인자값을 fy함수에서는 사용하지 않는다.
