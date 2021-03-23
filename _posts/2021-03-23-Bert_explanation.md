---
layout: post
title: Comprehensive BERT
excerpt: Bert를 이해 하는데 여러가지 어려운 개념이 많아서, 공부해야할 것 들이 많다. 하나하나 개념을 익히기 위해 중요한 컨퍼런스와 유용한 페이지를 담았고, 시행착오를 겪으며 진행하는 개인적인 정리 노트를 작성해 보았다. 
categories: [Machine Learning, Deep Learning, AI, NLP]
use_math: true
comments: true
tag: [Bert, NLP, OpenAI]
---

# 처음 정리하는 Bert

NLP 자연어 처리를 공부하는데 필요한 개인적인 정리 노트

**레퍼런스** 

1. [BERT for Dummies step by step tutorial by Michel Kana](https://towardsdatascience.com/bert-for-dummies-step-by-step-tutorial-fb90890ffe03)
2. [Demystifying BERT: Groundbreaking NLP Framework by Mohd Sanad Zaki Rizvi](https://www.analyticsvidhya.com/blog/2019/09/demystifying-bert-groundbreaking-nlp-framework/)
3. [A visual guide to using BERT by Jay Alammar](http://jalammar.github.io/a-visual-guide-to-using-bert-for-the-first-time/)
4. [BERT Fine tuning By Chris McCormick and Nick Ryan](https://mccormickml.com/2019/07/22/BERT-fine-tuning/)
5. [How to use BERT in Kaggle competitions - Reddit Thread](https://www.reddit.com/r/MachineLearning/comments/ao23cp/p_how_to_use_bert_in_kaggle_competitions_a/)
6. [BERT GitHub repository](https://github.com/google-research/bert)
7. [BERT - SOTA NLP model Explained by Rani Horev](https://www.kdnuggets.com/2018/12/bert-sota-nlp-model-explained.html)
8. [YOUTUBE - BERT Pretranied Deep Bidirectional Transformers for Language Understanding algorithm by Danny Luo](https://www.youtube.com/watch?v=BhlOGGzC0Q0)
9. [State-of-the-art pre-training for natural language processing with BERT by Javed Quadrud-Din](https://blog.insightdatascience.com/using-bert-for-state-of-the-art-pre-training-for-natural-language-processing-1d87142c29e7)
10. [BERT-Explained FAQs by Yashu Seth](https://yashuseth.blog/2019/06/12/bert-explained-faqs-understand-bert-working/)

## 1. Bert 배경

> BERT is a deep learning model that has given state-of-the-art results on a wide variety of natural language processing tasks. It stands for Bidirectional Encoder Representations for Transformers. It has been pre-trained on Wikipedia and BooksCorpus and requires (only) task-specific fine-tuning.

SQuAD 1.1 데이터셋을 이용해 인간의 정확도 수준을 상회하는 기계 독해 시스템들이 머신러닝 커뮤니티에 파문을 일으키게 되었다. Bert가 자연어처리 판도를 크게 바꿨다고 해도 과언이 아니다. 

라벨이 없는 대규모 데이터 세트에서 훈련된 단일 모델을 이용하며, 동시에 파인튜닝을 진행해 11개의 자연어처리 작업으로 최적의 결과물을 만들어 낼 수 있는 Bert는 우리가 어떻게 모델을 설계해야 하는지에 대한 가이드가 될 수 있다. 

Bert는 최근 자연어 처리 학습 성과와 언어 모델 Google의 TransformerXL, OpenAI의 GPT-2, XLNet, ERINIE2.0, RoBERTa 등에 영감을 주었다.

## 2. 왜 Bert 를 사용하나

기본적으로 트랜스포머 인코더와 함께 놓여져있는 세트로 볼 수 있다. 양방향성을 갖고 있고, 이 개념은 OpenAI 의 GPT 와 차별적인 요소이다. Bert는 내부적인 작업을 양방향으로 수행할 수 있는 모델 이라고 할 수 있다.

- BERT는 트랜스포머의 양방향 엔코더 표현을 의미한다. 여기 있는 각각의 단어는 그것에 의미를 가지고 있고 우리는 그것을 하나씩 마주칠 것이다. 무엇보다 **BERT는 Transformer 아키텍처를 기반으로 한다**는 것이 가장 중요하다.
- BERT는 위키피디아 전체를 포함한 라벨이 없는 큰 말뭉치(2억 5천 5백만 단어!) 와 책 corpus(8억 단어) 사전 훈련된다. 이 사전 훈련 단계는 BERT의 성공에 정말 중요하다. 왜냐하면 우리가 큰 텍스트 corpus 모델을 훈련시킬 때, 우리의 모델은 언어가 어떻게 작동 하는지에 대한 더 깊고 친밀한 이해를 얻기 시작하기 때문이다.이 지식은 거의 모든 NLP 작업에 유용한 스위스 군용 칼 이라고 할 수 있다.

![](https://user-images.githubusercontent.com/6022269/112178059-d38b9a00-8c3c-11eb-9ffa-a8dfa080dcf7.png){: width="70%" height="70%"}

- 이러한 양방향적 이해는 NLP 모델을 다음 단계로 끌어올리는데 매우 중요하다. 그것이 정말로 무엇을 의미하는지 이해할 수 있는 예를 보자. 같은 단어를 가진 두 문장이 있을 수 있지만 아래에서 볼 수 있듯이 앞뒤에 오는 것에 따라 그 의미는 완전히 다를 수 있다.

![](https://user-images.githubusercontent.com/6022269/112177951-b8208f00-8c3c-11eb-8020-6564aff43589.png)

이렇게 맥락을 고려하지 않고는 기계가 의미를 진정으로 이해하는 것은 불가능하며, 그것은 실제로 좋은 것이 아닌 쓰레기 같은 반응을 몇 번이고 버릴 수 있다.

**하지만 BERT는 이것을 고친다. 그래서 BERT는 NLP의 게임체인저가 될 수 있다.**

- BERT의 가장 큰 장점은 이미지넷의 움직임을 가져오게 했다는 것이고, BERT의 가장 인상적인 측면은 다양한 NLP 태스크를 위한 최첨단 모델을 만들기 위해 몇 개의 추가 출력 레이어만 추가하여 미세 조정할 수 있다는 것이다.

## 3. 왜 Bert 가 중요한가

왜 우리가 Bert를 사용 해야 하는지에 대한 이해를 돕기 위한 자료를 보자

![](https://user-images.githubusercontent.com/6022269/112178010-c9699b80-8c3c-11eb-9033-4db4dc0c54aa.png)

모든 GLUE 점수가 매우 의미 있는 것은 아니지만, Transformer(Open-GPT, BERT 및 BigBird)라는 인코더를 기반으로 한 일반 모델은 업무지향 모델과 인간 성능 사이의 격차를 1년 이내로 좁혔다.

## 4. 어떻게 Bert가 작동하나

BERT를 좀 자세히 살펴보고 그것이 왜 언어를 모델링하는 데 그렇게 효과적인 방법인지 이해하자. 우리는 이미 BERT가 무엇을 할 수 있는지 보았지만, 어떻게 할 수 있을까? 이 절에서 적절한 질문에 답이 될 것 이다.

1. Architecture of BERT

    BERT는 다층 양방향 트랜스포머 인코더이다.이 논문에는 두 가지 모델이 소개되어 있다.

    BERT 기본 – 12 레이어 (transformer blocks), 12 attention 헤드, 110 만개 파라미터.

    BERT Large – 24 레이어, 16 attention 헤드, 340 million 파라미터.

    BERT(transformer)의 구성 요소에 대한 심층적인 이해를 위해서는 아래 그림 에서의 transformer 를 확인 해야 한다.

![](https://user-images.githubusercontent.com/6022269/112178047-d1294000-8c3c-11eb-8150-4b4ef5907d5f.png){: width="50%" height="50%"}

1. Preprocessing Text for BERT
2. Pre Training
3. Fine Tuning Techniques for BERT

## 4. Fine Tuning Techniques for BERT

1. Sequence Classification Tasks
2. Sentence Pair Classification Tasks
3. Question-Answering Tasks (Goal of this competition)
4. Single Sentence Tagging Tasks
5. Hyperparameter Tuning