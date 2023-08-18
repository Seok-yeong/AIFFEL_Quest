# AIFFEL Campus Online 5th Code Peer Review
- 코더 : 김석영
- 리뷰어 : 황규빈


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 넵, 주어진 문제를 모두 해결하였고 정상 작동 합니다.
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 코드가 다른 사람이 보기 편하게 되어 있습니다.
  > 배려심이 좋은 코드 인거 같습니다.
  > 또한 주석을 보고 코드의 역할을 잘 알 수 있습니다.
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 넵
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
- 네, 배려심이 좋은 코드입니다.
```

# 예측을 위한 훈련 및 테스트 데이터 전처리
from tensorflow.keras.preprocessing.text import Tokenizer
from tensorflow.keras.preprocessing.sequence import pad_sequences

# 토크나이저 정의 (훈련 데이터에 사용한 것과 동일해야 함)
tokenizer = Tokenizer(num_words=vocab_size)
tokenizer.fit_on_texts(x_train)  

# 테스트 데이터 토큰화
x_test_sequences = tokenizer.texts_to_sequences(x_test)  

# 패딩
x_test_padded = pad_sequences(x_test_sequences, maxlen=max(len(l) for l in x_train))
# 원-핫 인코딩 적용
y_test_one_hot = to_categorical(y_test, num_classes=num_classes)
# 모델 평가
test_loss, test_accuracy = model_LSTM.evaluate(x_test_padded, y_test_one_hot)
print(f'Test accuracy: {test_accuracy}')

```


- [O] 코드가 간결한가요?
  > 

# 예시
```python

```

# 참고 링크 및 코드 개선

```python
기존 모델의 갯수만큼 리턴 하는 방식을 아래처럼 배열에 담아서 보내는건 어떠신지 의견 남겨보았습니다.
def train_predict(tfidfv, y_train, tfidfv_test, y_test):
    models = []
    ....
    ....
    models.append(model...)
    ....
    ....
    return models

def train_predict(tfidfv, y_train, tfidfv_test, y_test):
    # 1) 나이브 베이즈 분류기
    model_nb = MultinomialNB()
    model_nb.fit(tfidfv, y_train)
    
    predicted = model_nb.predict(tfidfv_test)            
    print("정확도_나이브 베이즈 분류기:", accuracy_score(y_test, predicted))  
    
    # 2) Complement Naive Bayes Classifier(CNB)
    model_cnb = ComplementNB()
    model_cnb.fit(tfidfv, y_train)
    
    predicted = model_cnb.predict(tfidfv_test)           
    print("정확도_CNB:", accuracy_score(y_test, predicted))
    
    # 3) 로지스틱 회귀(Logistic Regression)
    model_lr = LogisticRegression(C=10000, penalty='l2', max_iter=3000)
    model_lr.fit(tfidfv, y_train) 
    
    predicted = model_lr.predict(tfidfv_test)            
    print("정확도_로지스틱 회귀:", accuracy_score(y_test, predicted))  
    
    # 4) 선형 서포트 벡터 머신(LSVM)
    model_lsvc = LinearSVC(C=1000, penalty='l1', max_iter=3000, dual=False)
    model_lsvc.fit(tfidfv, y_train)
    
    predicted = model_lsvc.predict(tfidfv_test)            
    print("정확도_LSVM:", accuracy_score(y_test, predicted))  
    
    # 5) 결정 트리(Decision Tree)
    model_tree = DecisionTreeClassifier(max_depth=10, random_state=0)
    model_tree.fit(tfidfv, y_train)
    
    predicted = model_tree.predict(tfidfv_test)            
    print("정확도_Decision Tree:", accuracy_score(y_test, predicted))
    
    # 6) 랜덤 포레스트(Random Forest)
    model_forest = RandomForestClassifier(n_estimators=100, random_state=0) # 100개의 트리를 사용
    model_forest.fit(tfidfv, y_train)
    
    predicted = model_forest.predict(tfidfv_test)            
    print("정확도_Random Forest:", accuracy_score(y_test, predicted))  
    
    # 7) 그래디언트 부스팅 트리(GradientBoostingClassifier)
    model_grbt = GradientBoostingClassifier(random_state=0)  # verbose=3
    model_grbt.fit(tfidfv, y_train)  # 15분 정도 소요됨.
    
    predicted = model_grbt.predict(tfidfv_test)            
    print("정확도_GradientBoosting:", accuracy_score(y_test, predicted))  
    
    # 8) 보팅(Voting)
    voting_classifier = VotingClassifier(
        estimators=[
            ('model_lr', LogisticRegression(penalty='l2', random_state=0)),
            ('model_cnb', ComplementNB()),
            ('model_grbt', GradientBoostingClassifier(random_state=0))
        ],
        voting='soft' 
    )
    voting_classifier.fit(tfidfv, y_train)
    
    predicted = voting_classifier.predict(tfidfv_test)
    print("정확도_Voting:", accuracy_score(y_test, predicted))
    
    return model_nb, model_cnb, model_lr, model_lsvc, model_tree, model_forest, model_grbt, voting_classifier
```
