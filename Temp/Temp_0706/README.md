# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 최지수
- 리뷰어 : 김석영


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 평가문항 3개 중 2개 해결하였고, 
  > 나머지 1개의 기준(110000 이하의 점수 획득)은 충족 못하였으나, 상세기준에 근접한 점수를 획득하였음.
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 이해됐음. Task별로 잘 구분돼져 있고, 주석도 적정하게 기재돼 있음.
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 에러 유발 가능성은 없어 보임.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > Task별로 처리 과정 및 데이터 간의 관계 등을 상세히 파악하는 식으로 코드를 작성하였으므로 제대로 이해했다고 할 수 있음.
- [O] 코드가 간결한가요?
  > 특별히 중복 사용된 코드가 없고 간결한 편임.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
from sklearn.model_selection import GridSearchCV

gboost = GradientBoostingRegressor()
xgboost = XGBRegressor()
lightgbm = LGBMRegressor()
rdforest = RandomForestRegressor()

models = [gboost, xgboost, lightgbm, rdforest]


def GridSearch(model, x, y, param_grid, verbose=3, n_jobs=16):
    # GridSearchCV 모델로 초기화
    grid_model = GridSearchCV(model, param_grid=param_grid, scoring="r2", \
                              cv=10, verbose=verbose, n_jobs=n_jobs)
    # 모델 fitting
    grid_model.fit(x, y)

    # 결과값 저장
    params = grid_model.cv_results_['params']
    score = grid_model.cv_results_['mean_test_score']
    
    # 데이터 프레임 생성
    results = pd.DataFrame(params)
    results['mean'] = score
    results['score'] = model.score(x, y)

    return results
```

# 참고 링크 및 코드 개선
```python
충분한 시간 속에서 보다 다양한 하이퍼 파라미터 튜닝을 시도해보면 보다 좋은 퍼포먼스를 얻을 수 있을 것임.
```
