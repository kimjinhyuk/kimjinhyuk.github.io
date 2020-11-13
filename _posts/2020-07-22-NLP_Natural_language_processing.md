---
layout: post
title: 텍스트 전처리(Text preprocessing) - Natural language processing
excerpt: "자연어 처리에 있어서 텍스트 전처리는 매우 중요한 작업입니다. 텍스트 전처리는 용도에 맞게 텍스트를 사전에 처리하는 작업입니다. 요리에 있어서 재료를 제대로 손질하지 않으면, 요리가 제대로 되지 않는 것과 같습니다. 텍스트에 대해서 제대로 된 전처리를 하지 않으면 뒤에서 배울 자연어 처리 기법들이 제대로 동작하지 않습니다. 이 챕터에서는 텍스트를 전처리하기 위한 각종 기법에 대해서 배웁니다."
categories: [NLP]
use_math: true
comments: true
tag: [AI, 파이썬, Python, NLP]
---

## 텍스트 전처리(Text preprocessing)  

 > 자연어 처리에 있어서 텍스트 전처리는 매우 중요한 작업입니다. 텍스트 전처리는 용도에 맞게 텍스트를 사전에 처리하는 작업입니다. 요리에 있어서 재료를 제대로 손질하지 않으면, 요리가 제대로 되지 않는 것과 같습니다. 텍스트에 대해서 제대로 된 전처리를 하지 않으면 뒤에서 배울 자연어 처리 기법들이 제대로 동작하지 않습니다. 이 챕터에서는 텍스트를 전처리하기 위한 각종 기법에 대해서 배웁니다.


데이터를 필요에 맞게 전 처리가 되어 있지 않으면 데이터를 사용하고자하는 용도에 맞게 토큰화(tokenization) & 정제(cleaning) & 정규화(normalization) 를 해주어야 한다.

NLTK 패키지, KoNLPY를 통해 실습을 진행하며 토큰화를 진행 해 주며, 한글 처리를 위해 JDK 설치에 관한 `이슈` 가 있었지만 해결 방법이 있다.
[( JDK 설치 및 개발환경 셋팅 이슈 )](https://sdkim817.wordpress.com/2020/01/30/konlpy-설치-및-이용/)

토큰의 기준을 단어(word)로 하는 경우, 단어 토큰화(word tokenization)라고 하지만 여기서 단어(word)는 단어 단위 외에도 단어구, 의미를 갖는 문자열로도 간주되기도 한다.

~~~ Python
from nltk.tokenize import word_tokenize
text = '''
Don't be fooled by the dark sounding name, Mr. Jone's Orphanage is as cheery as cheery goes for a pastry shop.
'''
print(word_tokenize(text))
~~~
~~~ Python
['Do', "n't", 'be', 'fooled', 'by', 'the', 'dark', 'sounding', 'name', ',', 'Mr.', 'Jone', "'s", 'Orphanage', 'is', 'as', 'cheery', 'as', 'cheery', 'goes', 'for', 'a', 'pastry', 'shop', '.']
~~~
word_tokenize는 Don't를 Do와 n't로 분리하였으며, 반면 Jone's는 Jone과 's로 분리한 것을 확인할 수 있다.

{% highlight python %}
#여러 형태의 단어로 추출 할 수 있는 패키지들
# 1
from nltk.tokenize import WordPunctTokenizer
print(WordPunctTokenizer().tokenize(text))
# 2
from nltk.tokenize import TreebankWordTokenizer
print(TreebankWordTokenizer().tokenize(text))
# 3
from nltk.tokenize import sent_tokenize
print(sent_tokenize(text))
#하이픈, '는 붙여서 분절화해준다.
{% endhighlight %}

### 불용어(Stopword)
 갖고 있는 데이터에서 유의미한 단어 토큰만을 선별하기 위해서는 큰 의미가 없는 단어 토큰을 제거하는 작업이 필요합니다. 여기서 큰 의미가 없다라는 것은 자주 등장하지만 분석을 하는 것에 있어서는 큰 도움이 되지 않는 단어들을 말합니다. 예를 들면, I, my, me, over, 조사, 접미사 같은 단어들은 문장에서는 자주 등장하지만 실제 의미 분석을 하는데는 거의 기여하는 바가 없는 경우가 있습니다. 이러한 단어들을 불용어(stopword)라고 하며, NLTK에서는 위와 같은 100여개 이상의 영어 단어들을 불용어로 패키지 내에서 미리 정의하고 있습니다.

### 1. NLTK를 통해서 불용어 제거하기

{% highlight python %}
from nltk.corpus import stopwords
sw = ['.', ',', "'"]
sw_removed = []
for i in words:
    if i.lower() not in sw:
        sw_removed.append(i)

print(sw_removed)
{% endhighlight %}

### 2. 한국어에서 불용어 제거하기
{% highlight python %}
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize

example = "고기를 아무렇게나 구우려고 하면 안 돼. 고기라고 다 같은 게 아니거든. 예컨대 삼겹살을 구울 때는 중요한 게 있지."
stop_words = "아무거나 아무렇게나 어찌하든지 같다 비슷하다 예컨대 이럴정도로 하면 아니거든"
# 위의 불용어는 명사가 아닌 단어 중에서 저자가 임의로 선정한 것으로 실제 의미있는 선정 기준이 아님
stop_words=stop_words.split(' ')
word_tokens = word_tokenize(example)

result = []
for w in word_tokens:
    if w not in stop_words:
        result.append(w)
# 위의 4줄은 아래의 한 줄로 대체 가능
# result=[word for word in word_tokens if not word in stop_words]

print(word_tokens)
print(result)
{% endhighlight %}
{% highlight python %}
['고기를', '아무렇게나', '구우려고', '하면', '안', '돼', '.', '고기라고', '다', '같은',
 '게', '아니거든', '.', '예컨대', '삼겹살을', '구울', '때는', '중요한', '게', '있지', '.']
['고기를', '구우려고', '안', '돼', '.', '고기라고',
 '다', '같은', '게', '.', '삼겹살을', '구울', '때는', '중요한', '게', '있지', '.']
{% endhighlight %}

한국어 불용어를 제거할때는 코드 내에서 직접 정의하지 않고 txt 파일이나 csv 파일로 수많은 불용어를 정리해놓고, 이를 불러와서 사용한다.

### 3. 워드클라우드 출력

{% highlight python %}
# 토큰화를 위한 모듈
from konlpy.tag import Okt  
# 빈도수 딕셔너리를 만들기 위한 모듈
from collections import Counter
# 워드클라우드
from wordcloud import WordCloud
import matplotlib.pyplot as plt
ktext = '''
어벤저스 엔드 게임 뒷이야기라는 점을 신경 쓰느라
정작 `피터 파커` 스파이더맨의 이야기는 제대로 설명하지 못한 아쉬운 영화네요.
그리고 웃긴 점은 이 스파이더맨 전 편 `스파이더맨 홈커밍`만 보고 온 관객이라면,
모를 수밖에 없는 인물들이 등장하고, 스토리도 이해가 안 될 수 있어요.
이 영화를 보려면 전 편은 당연히 봐야 하는 거고, 어벤저스 엔드게임부터, 아이언 맨까지
하 아~ 마블 영화 피로도 극에 달한다.
이제 마블도 손절할 때인가?
그래도 마블 캐릭터 중에 저의 최고 애정 캐릭터인 스파이더맨인데
이번 영화는 온통 아이언맨 오마주로 점철돼버려서,
이게 스파이더맨인지 아이언맨 주니어인지 헷갈릴 정도입니다.
악당조차 반 아이언맨 연합(?) 구성이라니.;;
이런 식으로 흘러가다 보니 주인공이어야 할 스파이더맨의 스토리가 너무도 빈약합니다.
mj한테 어찌 사랑의 감정을 느꼈는지 영화에서 설명을 안 해줘요.
그냥 `여행 가서 고백을 해야지`... 이러면서 얼렁뚱땅 넘어가요.
스파이더맨이 악당한테 당하고 좌절했을 때
그를 각성 시킨 것은 해피의 단 한 마디였죠.
더 이상 시간을 줄 수 없었나 봐요.
아이언맨 따까리 스파이더맨이니 더 이상 분량 요구는 괘씸한 거죠.
차라리 예전 어두웠던 스파이더맨이
가난했고, 삼촌의 죽음에 자책하고 슬퍼하던 그 친구가 그리워지는 영화였습니다.
'''

words = Okt().morphs(ktext)

sw = ['.', ',', "'", '\n', '이', '가', '을', '를']

sw_removed = []
for i in words:
    if i.lower() not in sw:
        sw_removed.append(i)

count_list = Counter(sw_removed)

my_wc = WordCloud(font_path='NanumSquareEB.ttf', background_color='white')
plt.imshow(my_wc.generate_from_frequencies(count_list))
plt.axis('off')
plt.show()
{% endhighlight %}

![워드크라우드](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/capture_word_cloud.PNG?raw=true)

 출처 :  [딥 러닝을 이용한 자연어 처리 입문 wiki_docs](https://wikidocs.net/book/2155)
