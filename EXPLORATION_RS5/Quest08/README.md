# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김석영
- 리뷰어 : 황인준


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 챗봇을 트랜스포머를 이용해서 구현했고, 질문에 대한 답을 생성해 냈습니다.
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 추후에 본인이 확인해 봤을때나 다른 사람들도 이해가 잘 되도록 작성했습니다.
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 에러 없이 잘 동작했습니다.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 에러가 없었고, 결과도 잘 생성된 것을 보면 코드를 이해하고 작성하셨음을 알 수 있습니다.
- [O] 코드가 간결한가요?
  > 기능별로 셀 분리가 이루어 져있어서 가독성이 좋았고 간결하게 작성됐습니다.

# 예시
```python
#주석 예시
# 세 개의 서브 층을 내부적으로 구현한 디코더 함수
# 1) 셀프 어텐션   2) 인코더-디코더 어텐션   3) 피드 포워드 신경망
```

# 참고 링크 및 코드 개선
에포크를 크게 잡고 콜백 함수를 통해서 early stopping을 사용하셨는데, patience가 1로 되어 있어서 약간 일찍 러닝이
끝났을 수도 있겠다는 생각이 듭니다. patience를 2나 3정도로 늘려서 해보는것도 괜찮을것 같습니다.
```python
from keras.callbacks import EarlyStopping
es=EarlyStopping(monitor='accuracy',mode='max',verbose=1,patience=1)

EPOCHS = 100
model.fit(dataset, epochs=EPOCHS, callbacks=[es], verbose=1)
```
