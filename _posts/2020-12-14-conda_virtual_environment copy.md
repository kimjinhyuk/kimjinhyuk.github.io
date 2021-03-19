---
layout: post
title: Conda 가상환경 설정하기 
excerpt: 광인사에 노트북 반납하고 나의 맥북을 포맷하는 바람에 가상환경 셋팅을 다시 하게 되었는데 남의 블로그에서 찾기 귀찮아 정리 하는 차원에서 쓴 POST, https://www.anaconda.com/products/individual 에서 다운 받고.. GUI 설치 방법도 있고, Line command 방법이 있는데 터미널에 익숙해서 커맨드로 설치.. 
categories: [Personal, Anaconda3, Tensorflow]
use_math: true
comments: true
tag: [personal, Anaconda, ML, environment]
---

## 맥 OS 아나콘다 및 파이썬 설치

맥을 포맷 하게 되어 개발환경을 새로 다시 설치 하면서 검색 하기가 귀찮아 포스트를 작성

아나콘다에 관한 자세한 설명은 [Anaconda Product Individual](https://www.anaconda.com/products/individual) 이곳에서 확인 하면 되지만, 간단히 요약하자면 데이터 분석등에 활용되는 다양한 라이브러리를 포함하고 있는 패키지형 개발환경 세트라고 할 수 있다. 머신러닝에 필수적인 라이브러리들 넘파이, 판다스, 사이파이, 케라스, 사이킷런 등 쉽게 설치 할 수 있는 장점이 있다.

### 아나콘다 설치 방법

1. 사이트에 접속하여 아나콘다 설치 프로그램 다운

[https://www.anaconda.com/products/individual](https://www.anaconda.com/products/individual)

인스톨러에서 맞는 OS별로 설치를 진행 하면 된다.

~~~ Python
### 아나콘다의 버전 확인
conda --version

### 아나콘다 최신버전 업데이트
conda update conda
~~~

1-1. conda 라는 명령어를 입력할 때 오류가 발생한다면 환경변수를 별도로 설정 해 주어야 한다.

~/.bash_profile 에 내용을 추가
~~~ Python
#본인에 맞는 경로를 적어 주어야 한다.
export PATH="/opt/anaconda3/bin:$PATH"
~~~

~/.bash_profile 재시작
~~~ Python
source ~/.bash_profile
~~~

2. 가상환경 생성

~~~ Python
# 새로운 가상환경 생성
conda create --name "가상환경명" python="파이썬버전"

# 현재 생성된 가상환경 확인
conda info --envs

# 가상환경 활성화
conda activate "생성한 가상환경명"

# 가상환경 나가기
conda deactivate
~~~

3. Jupyter notebook 설치

~~~ Python
### Jupyter Notebook (주피터 노트북) 설치
conda install jupyter notebook
~~~

4. 가상환경에 Tensorflow 설치

~~~ Python
### 가상환경에 텐서플로우 설치
conda install tensorflow
~~~

> [텐서플로우 공식 설치 문서](https://www.tensorflow.org/install/pip?hl=ko&lang=python3) 

~~~ Python
#아래 소스를 실행시킨 후 출력이 정상적으로 되는지 확인
import tensorflow as tf

with tf.compat.v1.Session() as sess:
  hello = tf.constant("Hello")
  world = tf.constant("World!")
  sentence = hello + world
  pr = sess.run(sentence)
  print(pr)
~~~
