# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 김석영
- 리뷰어 : 최철웅


# PRT(Peer Review Template)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - klue/bert-base 모델과 NSMC 데이터셋을 잘 불러왔다
    - DataCollator를 이용해 Dynamic Padding를 적용했다.
        ```python
        trainer = Trainer(
            model=klue_model,
            args=training_args,
            train_dataset=train_dataset,
            eval_dataset=val_dataset,
            data_collator=data_collator,
            tokenizer=tokenizer,
            compute_metrics=compute_metrics,
            callbacks=[EarlyStoppingCallback(early_stopping_threshold=0.001, early_stopping_patience=3)]
        )
        ```
        
- [x]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
  주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 로깅을 위해 도큐먼트를 참고해 early stopping, logging 등을 적용하였다.
        ```python
        training_arguments = TrainingArguments(
            output_dir='./results',
            num_train_epochs=1,
            per_device_train_batch_size=required_batch_size,
            per_device_eval_batch_size=64,
            warmup_steps=500,
            weight_decay=0.01,
            logging_dir='./logs',
            logging_steps=10,
            evaluation_strategy="steps",  # 로깅 스텝마다 평가 및 저장
            save_steps=10,
            save_total_limit=2,           # 마지막 2 모델만 저장 (보다 오래된 게 삭제됨.)
            load_best_model_at_end=True   # 평가된 것 중 제일 성능 좋은 모델을 로드함.
        )
        ```
        
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
  ”새로운 시도 또는 추가 실험을 수행”해봤나요?**
    - 과대적합 또는 과소적합을 확인해보기 위해 10 step마다 evaluation을 진행했으며 이를 tensorboard로 확인
      ```python
      training_args = TrainingArguments(
        output_dir='./results',
        num_train_epochs=1,
        per_device_train_batch_size=required_batch_size,
        per_device_eval_batch_size=64,
        warmup_steps=500,
        weight_decay=0.01,
        logging_dir='./logs_tensorboard',  # TensorBoard 로그가 저장될 디렉터리
        logging_steps=10,                  # 얼마나 자주 로그를 저장할 것인지 설정 (예: 10스텝마다)
        evaluation_strategy="steps",
        save_steps=10,
        save_total_limit=2,
        load_best_model_at_end=True,
        group_by_length=True
      )
      ```
      
- [x]  **4. 회고를 잘 작성했나요?**
    - 나온 학습 결과를 통해 훈련 시간과 훈련 속도가 이전보다 개선됨을 확인함
        | STEP 4에 학습한 결과와 bucketing을 적용하여 학습시킨 결과를 비교
        | transformers로 학습한 결과와 bucketing을 적용하여 학습시킨 결과를 비교해보면
        | 훈련 시간은 확실히 줄었으며, 성능의 차이가 크게 나진 않았지만, 훈련 속도의 향상이 있었다고 분석할 수 있습니다.
    
- [x]  **5. 코드가 간결하고 효율적인가요?**
    - 데이터셋 전처리에서 코드를 작업별로 분리하여 함수 정의 코드의 가독성을 높임
      ```python
      def split_dataset(dataset, train_ratio=0.9):
        n = len(dataset)
        train_size = int(train_ratio * n)
    
        train_datasets = [dataset.shard(num_shards=10, index=i) for i in range(int(10*train_ratio))]
        val_datasets = [dataset.shard(num_shards=10, index=i) for i in range(int(10*train_ratio), 10)]
    
        train_dataset = concatenate_datasets(train_datasets)
        val_dataset = concatenate_datasets(val_datasets)
    
        return train_dataset, val_dataset
      ```

# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
