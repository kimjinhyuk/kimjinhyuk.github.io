---
layout: post
title: 나이브 베이즈 분류기(Bayes' theorem) - Natural language processing
excerpt: "In probability theory and statistics, Bayes' theorem describes the probability of an event, based on prior knowledge of conditions that might be related to the event."
categories: [NLP]
use_math: true
comments: true
tag: [AI, 파이썬, Python, NLP]
---

## 나이브 베이즈 분류기(Bayes' theorem)

확률론과 통계학에서, 베이즈 정리(영어: Bayes’ theorem)는 두 확률 변수의 사전 확률과 사후 확률 사이의 관계를 나타내는 정리다. 베이즈 확률론 해석에 따르면 베이즈 정리는 사전확률로부터 사후확률을 구할 수 있다.

베이즈 정리는 불확실성 하에서 의사결정문제를 수학적으로 다룰 때 중요하게 이용된다. 특히, 정보와 같이 눈에 보이지 않는 무형자산이 지닌 가치를 계산할 때 유용하게 사용된다. 전통적인 확률이 연역적 추론에 기반을 두고 있다면 베이즈 정리는 확률임에도 귀납적, 경험적인 추론을 사용한다.

$\Pr(A\mid B)={\frac{\Pr(B\mid A)\Pr(A)}{\Pr(B)}}$

$Pr(A\mid B)$는 B의 값이 주어진 경우에 대한 A의 사후 확률이다.

$Pr(B\mid A)$는 A가 주어졌을 때 B의 조건부 확률이다.

이때 $A$ 는 불확실성을 계산해야 하는 대상이며, $B$는 관측하여 값을 알아낼 수 있는 대상으로 생각한다면, $A$의 확률은 $B$가 관측된 후 $P(A)$ 에서 $P(A\mid B)$로 변화하며, 베이즈 정리는 이 때의 변화를 계산하는 방법을 제공한다.

### 전체 흐름

1. **데이터 불러오기** - 영화 리뷰를 불러와  `키워드` 를 받아 긍/부 학습하고 테스트를 해서 출력한다.
2. **긍정/부정 키워드** - `데이터` 를 받아 긍/부정으로 나눈다.
3. **train_data** - `데이터`를 훈련 데이터로 메인메소드로 넘겨준다.
4. **데이터 전처리** - `스탑워드' 제거, `토큰화`, `BoW`[^1]  
5. **로그를 이용** - 확률을 구함 (문장이 나올 확률 = 각 단어가 나올 확률의 곱) - 로그를 사용하지 않으면 0에 가까운 수로 수렴하기 때문에 확률 확보용으로 사용
6. **nowords_weight** - train_data에 없는 단어들을 위해 빈도를 임의로 지정
7. **베이즈정리** - 조건부확률을 이용해서 확률 구하기
8. **긍/부 비율 지정** - `정확도`를 조절하기위함, 두 데이터의 비율로 넣어도 무방함
9. **로그의 지수화** - 로그를 지수화 하여 각각이 차지하는 비율 구하기 (Normalize)


[^1]: BoW(bag of words) 를 만드는 이유 - 해당 단어가 나올 확률을 구하기 위한 빈도수를 확보

* 데이터를 불러와 긍/부정 훈련리스트를 생성
{% highlight python %}
def open_csv():
    f = open('MovieReview.csv', 'r', encoding='utf-8')
    csvreader = csv.reader(f)

    pos_doc = []
    neg_doc = []

    for line in csvreader:
        if line[1] == 'positive':
            pos_doc.append(line[0])
        else:
            neg_doc.append(line[0])

    train_datas = [[], []]
    train_datas[0] = neg_doc
    train_datas[1] = pos_doc

    # 리스트 형태는 토큰화하기가 어렵기 때문에, 전부 조인을 통해서 하나의 문자열로 만들어준다
    return [' '.join(train_datas[0]), ' '.join(train_datas[1])]
{% endhighlight %}

* 긍/부정 데이터의 전처리 및 노이즈 생성

{% highlight python %}
def calculate_doc_prob(train_data, test_data, nowords_weight):
    sw_train_data = re.compile('[^\w]').sub(' ', train_data.lower())
    sw_train_token = sw_train_data.split()
    train_vector = dict(Counter(sw_train_token))

    sw_test_data = re.compile('[^\w]').sub(' ', test_data.lower())
    sw_test_token = sw_test_data.split()
    test_vector = dict(Counter(sw_test_token))

    log_prob = 0

    total_wc = len(sw_train_token)

    for word in test_vector:
        if word in train_vector:
            log_prob += log(train_vector[word]/total_wc)
        else:
            log_prob += log(nowords_weight/total_wc)

    return log_prob
{% endhighlight %}

* Bayes' theorem 를 적용한 확률을 구하고 지수화해서 확률 연산을 한다

{% highlight python %}

test_pos_prob = calculate_doc_prob(train_datas[1], test_data, 0.1) + log(pos_prob) 
test_neg_prob = calculate_doc_prob(train_datas[0], test_data, 0.1) + log(neg_prob) 

    maxprob = max(test_neg_prob, test_pos_prob)
    test_pos_prob -= maxprob
    test_neg_prob -= maxprob
    test_pos_prob = exp(test_pos_prob)
    test_neg_prob = exp(test_neg_prob)
    
    normalized_prob = [test_neg_prob/(test_pos_prob+test_neg_prob), test_pos_prob/(test_pos_prob+test_neg_prob)]

{% endhighlight %}

{% highlight python %}
핵노잼
[핵노잼] - 부정적일 확률 : [0.9989498854707781], 긍정적일 확률 : [0.0010501145292218243]
{% endhighlight %}