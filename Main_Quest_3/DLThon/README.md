# Pre-trained Model
`klue/bert-base`

# Tokenizer
`BertTokenizer.from_pretrained("klue/bert-base")`

---

## Directory tree
📦BERT_mskim  
 ┣ 📂data  
 ┃ ┣ 📜test.json
 ┃ ┣ 📜test.csv  
 ┃ ┣ 📜train_aug.csv  
 ┃ ┣ 📜train.csv  
 ┃ ┣ 📜val.csv  
 ┃ ┗ 📜mysubmission.csv  
 ┣ 📜eda.ipynb  
 ┣ 📜bert_10aug.ipynb  
 ┣ 📜preprocessing.ipynb  
 ┗ 📜README.md  
 
---

### File Descriptions

1. 
    - 요약
    > aug_num=10 설정하여 증식 진행한 train data 사용
    - Jupyter 파일 정보
    > `BERT_jsmon/bert_10aug.ipynb`
    - 사용 데이터 정보
    > `BERT_jmson/data/train_aug10.csv`
    ---
    - 데이터 개수
    > train 31600, validation 790
    - 데이터 원본 정보
    > `/aiffel/aiffel/dktc/data/train.csv`
    - 훈련 데이터셋 정보
        - Train : Val 비율
        > `8:2`
        - 모듈 정보
        > `from sklearn.model_selection import train_test_split`
    ---
    - 모델 파라미터
        - `MAX_LEN`: 400
        - `BATCH_SIZE`: 16
        - `LEARNING_RATE`: 2e-5
        - `EPOCH`: 1
    ---
    - 모델 평가
        - `loss`: `0.1136`
        - `accuracy`: `0.9606`
        - `리더보드`:`0.9`
    ---
    - `SUBMISSION` 파일 정보
    > `mysubmission.csv`
