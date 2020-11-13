---
layout: post
title: 퍼셉트론(Perceptron)
excerpt: "In machine learning, the perceptron is an algorithm for supervised learning of binary classifiers. A binary classifier is a function which can decide whether or not an input, represented by a vector of numbers, belongs to some specific class"
categories: [Deep Learning]
use_math: true
comments: true
tag: [AI, Machine Learning, Deep Learning]
---

> 인공신경망의 한 종류로서, 1957년에 코넬 항공 연구소(Cornell Aeronautical Lab)의 프랑크 로젠블라트 (Frank Rosenblatt)에 의해 고안되었다.

일반적으로 인공 신경망 시스템은 동물의 신경계를 본따 만들었기 때문에 개념적으로나 그 형태로나 비슷한 부분이 많다.

![](https://image.slidesharecdn.com/lecture29-convolutionalneuralnetworks-visionspring2015-150504114140-conversion-gate02/95/lecture-29-convolutional-neural-networks-computer-vision-spring2015-9-638.jpg?cb=1430740006)
*출처 : https://www.slideshare.net/jbhuang/lecture-29-convolutional-neural-networks-computer-vision-spring2015

위의 그림 처럼 퍼셉트론은 실제 뇌를 구성하는 신경 세포 뉴런의 동작과 유사하기 때문에 신경세포의 동작 원리를 알아야 한다.

![](https://wikidocs.net/images/page/24958/%EB%89%B4%EB%9F%B0.PNG)
*출처 : https://wikidocs.net/24958*

가지돌기는 인공신경망의 입력값(input) 혹은 입력벡터의 값을 받아들이는 역할을 한다. 입력받은 값이 일정한 값 임계치(Threshold) 이상이면 축삭돌기 통하여 전달하는데  인공신경망에서는 가중치(Weights)가 대신한다. 각각의 인공 뉴런에서 보내진 입력값 $x $ 는 각각의 가중치 $W$ 와 함께 종착지인 인공 뉴런에 전달한다.

각 입력값이 가중치와 곱해져서 인공 뉴런에 보내지고, 각 입력값과 그에 해당되는 가중치의 곱의 전체 합이 임계치(threshold)를 넘으면 종착지에 있는 인공 뉴런은 출력 신호로서 1을 출력하고, 그렇지 않을 경우에는 0을 출력한다.

$$ y = \begin{cases}
0 (w_1x_1+w_2x_2+...+w_nx_n  \leq \theta)
\\1 (w_1x_1+w_2x_2+...+w_nx_n > \theta)
\end{cases}$$

이때 $\theta$ 를 $b$(편향,bias)  로 치환해 numpy 패키지를 이용해 코딩해 보자.

{% highlight python %}
import numpy as np

x1 = float(input("x1 :: "))
x2 = float(input("x2 :: "))

x = np.array([x1,x2])
w = np.array([0.5,0.6])
b = -0.4

# w1x1 + w2x2 + b
ret = np.sum(w*x) + b

if ret <= 0:
    print(0)
else:
    print(1)
{% endhighlight %}
