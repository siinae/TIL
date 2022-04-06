# 손실 함수(loss function)

##### 	keras 제공

- `손실함수(loss function) `
  - 정답에 대한 오류를 나타내는 것
    - 모델의 출력값과 사용자가 원하는 출력값의 차이
  - 정답에 가까울수록 작은 값, 오답에 가까울수록 큰 값

---





---

### Binary Cross-entropy(이진 크로스 엔트로피)

- 이진 분류(Binary classification) 문제에서 사용
- label 이 0 또는 1을 값으로 가질 때 사용
- 모델의 마지막 레이어의 활성화 함수 : `시그모이드(sigmoid) `함수

---



---

### Categorical Cross-entropy(범주형 크로스 엔트로피)

- 다중 분류(Multi-class classification) 문제에서 사용

- label이 class를 나타내는 `one-hot-vector`를 값으로 가질 때 사용( 원핫 인코딩 된 형태)
  - ex. 3-class classification 문제라면, label이 [1, 0, 0] , [0, 1, 0] 또는 [0, 0, 1]을 값으로 가질 때 사용

- 모델의 마지막 레이어의 활성화 함수 : 소프트맥스(softmax) 함수

---



---

### Sparse Categorical Crossentropy

- 다중 분류(Multi-class classification) 문제에서 사용
- label이 calss를 나타내는 `class index`를 값으로 가질 때 사용(정수 인코딩 된 형태)
  - ex. 3-class classification 문제라면, label이 0 ,1 또는 2를 값으로 가질 때 사용

- 모델의 마지막 레이어의 활성화 함수 : 소프트맥스(softmax) 함수

---



---

### Mean Squared Error(평균 제곱 오차)

- 실제 데이터와 예측 데이터 편차의 제곱합인 오차제곱합(SSE)을 데이터의 크기로 나누어 평균으로 만든 값
- 회귀분석과 유사한 용도로 사용(연속형 데이터)

---

