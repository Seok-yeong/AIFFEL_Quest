# AIFFEL Campus Online 5th Code Peer Review
- 코더 : 김석영
- 리뷰어 : 최철웅


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [ ]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
  - 데이터 증대를 통해 총 32129개의 샘플 생성
    ```python
    print(len(all_que_corpus))
    print(len(all_ans_corpus))
    ```
    
- [x]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
  주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - `build_corpus()` 함수 구현시 각 단계별로 주석
      ```python
      from konlpy.tag import Mecab

      def build_corpus(src_data, tgt_data, tokenizer, max_len=40):
          # 토큰화
          src_corpus = []
          tgt_corpus = []
      
          # 중복 체크를 위한 set
          pair_set = set()
      
          for src, tgt in zip(src_data, tgt_data):
              # 문장 정제
              src_clean = preprocess_sentence(src)
              tgt_clean = preprocess_sentence(tgt)
      
              # 토큰화
              src_tokens = tokenizer(src_clean)
              tgt_tokens = tokenizer(tgt_clean)
      
              # 토큰의 개수가 max_len 이하인지 확인
              if len(src_tokens) <= max_len and len(tgt_tokens) <= max_len:
                  # 중복 문장 확인
                  src_str = ' '.join(src_tokens)
                  tgt_str = ' '.join(tgt_tokens)
      
                  pair_str = src_str + " <SEP> " + tgt_str
      
                  if pair_str not in pair_set:
                      src_corpus.append(src_tokens)
                      tgt_corpus.append(tgt_tokens)
                      pair_set.add(pair_str)
      
          return src_corpus, tgt_corpus
      ```
      
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
  ”새로운 시도 또는 추가 실험을 수행”해봤나요?**
    - 과적합을 확인하기 위해 데이터셋을 나눠 검증 데이터셋을 만듦
      ```python
      # 데이터 분할
      enc_val = enc_train[split_idx:]
      enc_train = enc_train[:split_idx]
      
      dec_input_val = dec_input_train[split_idx:]
      dec_input_train = dec_input_train[:split_idx]
      
      dec_target_val = dec_target_train[split_idx:]
      dec_target_train = dec_target_train[:split_idx]
      ```
  
- [x]  **4. 회고를 잘 작성했나요?**
    - 실험을 위해 검증 데이터셋을 나누려 했지만 커널이 꺼지는 현상이 발생해 다양한 방법을 시도함
      > 프로젝트 요청사항에 데이터 분할(train/val)에 대한 부분은 없으나,
      > 과대적합 여부를 (시각적으로) 명확히 확인하기 위해 train loss와 validation loss를 비교하려
      > train_test_split 메서드를 사용해 train data로 부터 validation data를 분할하려 했으나,
      > 이 메서드를 사용하거나, 그 외 shuffle이나 split을 하려는 코드를 실행하면 kernel이 계속 죽어
      > validation set을 제대로 분할하지 못했으므로
      > 그러한 차원에서 본 시도를 바라봐주기 바라며,
      > overfitting 여부는 학습의 진행상태와 성능 평가로 판단해주기 바랍니다.
    
- [x]  **5. 코드가 간결하고 효율적인가요?**
    - `calculate_bleu()`와 `calculate_bleu_single()`을 통해 BLEU 점수 평가를 함수화 했다.
      ```python
      def calculate_bleu(sentences, reference_sentences, verbose=True):
          total_score = 0.0
          sample_size = len(sentences)
      
          for idx in range(sample_size):
              score = calculate_bleu_single(sentences[idx], reference_sentences[idx], verbose)
              total_score += score
      
          print("Num of Sample:", sample_size)
          print("Total Score:", total_score / sample_size)

      
      def calculate_bleu_single(sentence, reference_sentence, verbose=True, weights=[0.25, 0.25, 0.25, 0.25]):
          # preprocess and tokenize input sentence
          sentence = preprocess_sentence(sentence)
          tokens = mecab.morphs(sentence)
          tokenized_sentence = [word_to_index.get(token, word_to_index["<unk>"]) for token in tokens]
      
          # get predicted translation
          translation = evaluate(sentence)
          candidate = translation.split()
      
          # get reference translation
          reference = reference_sentence.split()
      
          # calculate BLEU score with smoothing function
          score = sentence_bleu([reference], 
                                candidate, 
                                weights=weights, 
                                smoothing_function=SmoothingFunction().method1)
      
          if verbose:
              print("Source Sentence: ", sentence)
              print("Model Prediction: ", candidate)
              print("Real: ", reference)
              print("Score: %lf\n" % score)
      
          return score
      ```

# 참고 링크 및 코드 개선
데이터셋을 분할하실 때 인덱스 리스트만 분할하신 다음 데이터를 가져올때 활용하시면 메모리 부족 문제가 해결되지 않을까 합니다.
