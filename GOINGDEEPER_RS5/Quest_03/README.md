# AIFFEL Campus Online 5th Code Peer Review
- 코더 : 김석영
- 리뷰어 : [이태훈](https://github.com/git-ThLee)


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 네! 저는 못했지만 편향성이 큰 조합들로 시각화했습니다

```python
# 한글 지원 폰트
sns.set(font='NanumGothic')

# 편향성이 큰 조합에 대한 히트맵 그리기
bias_matrix = [[0 for _ in range(len(genre_name))] for _ in range(len(genre_name))]
for comb in bias_combinations:
    i = genre_name.index(comb[0])
    j = genre_name.index(comb[1])
    bias_matrix[i][j] = comb[2]

plt.figure(figsize=(20,20))
sns.heatmap(bias_matrix, xticklabels=genre_name, yticklabels=genre_name, annot=True, cmap='RdYlBu_r')
plt.title('편향성이 큰 영화 장르 간의 WEAT Score', fontsize=20)
plt.show()
```


- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네! 설명이 필요한 구간마다 주석이 자세히 적혀있습니다

```python
# 편향성이 큰 장르 조합 찾기
bias_combinations = []
threshold = 0.8  # 임계값 설정

for i in range(len(genre_name)-1):
    for j in range(i+1, len(genre_name)):
        if abs(matrix[i][j]) > threshold:
            bias_combinations.append((genre_name[i], genre_name[j], matrix[i][j]))
```


- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 네! 😀😀


- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네! 또한, 이해를 돕기위해 여러 변수들을 출력했던 흔적도 남아있습니다!

- [O] 코드가 간결한가요?
  > 네! 대표 단어를 추출하는 코드가 심플하고 이해하기 쉽습니다!

```python
attributes = []
for i in range(len(w)):
    print(genre_name[i], end=': ')
    attr = []
    j = 0
    while (len(attr) < 20):
        if vectorizer.get_feature_names()[w[i][j][0]] in model.wv:
            attr.append(vectorizer.get_feature_names()[w[i][j][0]])
            print(vectorizer.get_feature_names()[w[i][j][0]], end=', ')
        j += 1
    attributes.append(attr)
    print()
```


# 참고 링크 및 코드 개선

> 코드가 깔끔해서 개선할 것이 없습니다!
