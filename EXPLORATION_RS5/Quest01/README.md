 # AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김석영
- 리뷰어 : 박혜원


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 각각의 필요한 부분에 주석을 달아서 이해하기 쉬웠습니다. 
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 각 셀에 대한 결과 값이 전부 정상적으로 출력되고 작동합니다.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네 다만, Project_02_Bicycle.ipynb 중간 부분에 features = ['temp', 'humidity', 'windspeed', 'weather', 'registered'] 만 사용하게 된 분석 과정이 포함되어있었으면 더 좋았을 것 같습니다.

- [O] 코드가 간결한가요? 
  > 네 아주 간결하고 명료합니다. 

# 개선 사항 제안 
Project_02_Bicycle.ipynb 코드 일부 :

```python
#특성간 상관관계 분석
train.corr()['count'].sort_values(ascending=False)
from sklearn.model_selection import train_test_split

#(4) X, y 컬럼 선택 및 train/test 데이터 분리
#X(feature) 에는 어떤 데이터 컬럼을 넣어야 될지 고민해 봅시다.
#만일 모든 데이터 컬럼(특징)을 넣는다면 오차 값이 말도 안 되게 적게 나올 수도 있습니다.   
#count 값을 맞추고자 하므로, y 변수에 count 컬럼의 데이터 넣기

features = ['temp', 'humidity', 'windspeed', 'weather', 'registered']        # 주석 또는 데이터 분석 과정 또는 여러 feature 값에 대한 experiment 등의 과정을 추가하여, 다음과 같은 feature 를 선택하게 된 과정이 포함되어있었다면 데이터 분석 측면에서 좋았을 것 같습니다.

X = train[features]
y = train['count']
```

# 참고 링크 및 코드 개선
