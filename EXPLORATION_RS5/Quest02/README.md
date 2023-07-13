# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김석영
- 리뷰어 : 최지수


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 평가문항 3개 중 2개는 해결했고, 나머지 1개도 상세기준에 근접한 점수(113,236점)을 획득하였음.
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 이해됐습니다.
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 별도 설명이 필요한 task에 대한 근거 작성이 있으면 좋을 듯함.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > Task별 적정한 코드에 기반하여 정석적인 Flow로 진행하였으므로 전체적으로 이해에 기반한 코드 작성으로 보임.
- [O] 코드가 간결한가요?
  > 네. 간결합니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
def my_GridSearch(model, train, y, param_grid, verbose=2, n_jobs=5):
    # GridSearchCV 모델로 초기화
    grid_model = GridSearchCV(model, param_grid=param_grid, scoring='neg_mean_squared_error', \
                              cv=5, verbose=verbose, n_jobs=n_jobs)
    
    # 모델 fitting
    grid_model.fit(train, y)

    # 결과값 저장
    # params, score에 각 조합에 대한 결과를 저장합니다. 
    params = grid_model.cv_results_['params']
    score = grid_model.cv_results_['mean_test_score']
    
    # 데이터 프레임 생성
    results = pd.DataFrame(params)
    results['score'] = score
    
    # RMSLE 값 계산 후 정렬
    # RMSLE 값을 추가한 후 점수가 높은 순서로 정렬한 `results`를 반환합니다.
    results['RMSLE'] = np.sqrt(-1 * results['score'])
    results = results.sort_values('RMSLE')

    return results
```

# 참고 링크 및 코드 개선
```python
없는 것 같습니다.
```
