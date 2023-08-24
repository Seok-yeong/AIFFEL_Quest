# AIFFEL Campus Online 5th Code Peer Review
- 코더 : 김석영
- 리뷰어 : [이태훈](https://www.naver.com)

# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 네!

```python
입력 문장: 특히 고도가 높은 곳에서 약해진 육체적 지구력을 일부 회복시켜주는 데 유용하다는 것이

예측된 번역: the korea times reports korea s consumer confidence has seen concerns about the korean peninsula. <end> 

```


- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네! 아래 코드가 의미하는 바를 주석으로 바로 확인이 가능합니다.

```python
# 토큰화를 통해 문장 내 토큰의 개수를 확인합니다.
    if len(mecab.morphs(kor)) <= 40 and len(en.split()) <= 40:
        kor_corpus.append(kor)
        eng_corpus.append(en)
```

- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 네!
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네!, 한국어와 영어 전처리 방식이 다른데 하나로 통합해서 구현했습니다.

```python
def preprocess_sentence(sentence, s_token=False, e_token=False):
    sentence = sentence.lower().strip()
    
    # 특수문자 양쪽에 공백을 추가하지 않고, 특수문자 앞에만 공백을 추가
    sentence = re.sub(r"([?.!,])", r"\1 ", sentence)
    # 두 개 이상의 공백을 하나의 공백으로 변경
    sentence = re.sub(r'[" "]+', " ", sentence)
    # a-zA-Z?.! 와 한글을 제외한 모든 문자를 공백으로 변경
    sentence = re.sub(r"[^a-zA-Z?.!ㄱ-ㅎㅏ-ㅣ가-힣]+", " ", sentence)
    
    sentence = sentence.strip()
    
    if s_token:
        sentence = '<start> ' + sentence
    if e_token:
        sentence += ' <end>'
    
    return sentence
```

- [O] 코드가 간결한가요?
  > 네!

# 예시
```python

```

# 참고 링크 및 코드 개선

```python

```

