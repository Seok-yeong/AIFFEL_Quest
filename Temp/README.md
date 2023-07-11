# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 조대호
- 리뷰어 : 김석영


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > Project 1의 평가문항의 상세기준(MSE 손실함수값 3000 이하를 달성)에 부합한 결과(2919.91)를 도출하였습니다.
  > Project 2의 평가문항의 상세기준(RMSE 값 150 이하를 달성)에 부합한 결과(141.22)를 도출하였습니다.
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 각 단계/순서별로 각 코드 주제에 대한 주석이 달려 있습니다.
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 본 주제와 관련 기본/정석적인 코드이므로 별도의 에러(syntax, symantic 모두) 발생 가능성은 딱히 보이지 않습니다. 
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 데이터 load부터 모델 구현, 성능 확인(using test data)까지 각 과정들이 무리없이 이행됐으므로 기본적으로 이해에 바탕해 코드가 작성됐다고 볼 수 있습니다.
- [O] 코드가 간결한가요?
  > 특별히 반복/중복되는 코드가 없고, 모델 학습과 결과 확인에 필요한 코드들로만 작성이 돼 있으므로 간결하게 작성됐다 할 수 있습니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
#피처수와 학습률 변경
print(diabetes.feature_names)
df_x1=[]
df_x1=diabetes.data[:, [2,3,7,8]]

print(df_x1.shape)

X_train, X_test, y_train, y_test = train_test_split(df_x1, df_y, test_size=0.2, random_state=42)
#특성 4개
import numpy as np
W = np.random.rand(4)
b = np.random.rand()

#모델 학습하기
losses = []

#모델 구현
def model(X, W, b):
    predictions = 0
    for i in range(4):
        predictions += X[:, i] * W[i]
    predictions += b
    return predictions

#학습도 2000번으로 증가
LEARNING_RATE = 0.1
for i in range(1, 2000):
    dW, db = gradient(X_train, W, b, y_train)
    W -= LEARNING_RATE * dW
    b -= LEARNING_RATE * db
    L = loss(X_train, W, b, y_train)
    losses.append(L)
    if i % 10 == 0:
        print('Iteration %d : Loss %0.4f' % (i, L))

#test로 성능확인
prediction = model(X_test, W, b)
mse = loss(X_test, W, b, y_test)
mse

import matplotlib.pyplot as plt
plt.scatter(X_test[:, 0], y_test)
plt.scatter(X_test[:, 0], prediction)
plt.show()
```

# 참고 링크 및 코드 개선
```python
예측(prediction)의 성능과 관련해, 데이터(feature) 선별시, target('count')과의 상관관계 등을 고려하면, 보다 좋은 성능의 결과를 도출하실 수 있을 것 같습니다.
```
