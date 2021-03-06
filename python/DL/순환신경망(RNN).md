# 순환신경망 ( RNN, Recurrent Neural Network)



---

## 개념

- 입력과 출력을 시퀀스 단위로 처리하는 가장 기본적인 인공 신경망 시퀀스(Sequence) 모델

- LSTM, GRU가 이에 속함

---



---

## 특징

- `셀(cell)` : RNN의 은닉층에서 활성화 함수를 통해 결과를 내보내는 역할을 하는 노드
  - 이전의 값을 기억하려고 하는 일종의 메모리 역할을 수행
  - 메모리 셀, RNN 셀 이라고 표현 
  - `은닉 상태` (hidden state)
    - 은닉층의 메모리 셀은 각각의 시점에서 바로 이전 시점에서의 은닉층의 메모리 셀에서 나온 값을 자신의 입력으로 사용 ---> `재귀적 활동`
    - 메모리 셀이 출력층 방향 또는 다음 시점의 자신에게 보내는 값을 의미

- RNN의 용도

  - 입력과 출력의 길이를 다르게 설계할 수 있어 다양한 용도로 사용 가능
  - 일 대 다 구조(one-to-many)
    - 하나의 입력에 대해 사진의 제목을 출력하는 `이미지 캡셔닝(Image Captioning)`
      - 사진의 제목 --> 단어들의 나열 --> 시퀀스 출력
  - 다 대 일 구조(many-to-one)
    - 입력 문서가 긍정적인지 부정적인지 판별하는 `감성분류(Sentiment classification)`
    - 스팸 메일 분류(spam detection)

  - 다 대 다 구조(many-to-many)
    - 사용자가 문장을 입력하면 대답 문장을 출력하는 `챗봇`
    - 입력문장으로부터 번역된 문장을 출력하는 `번역기`
    - `개체명 인식`, `품사 태깅`

---

