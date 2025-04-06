## Learning to Learn at Test Time: RNNs with Expressive Hidden States

- 주소: https://arxiv.org/pdf/2407.04620
- 공부기간(날짜): 2025.04.06
- 문제정의
  - 기존 RNN은 hidden state가 단순한 벡터로 작동하며, test time에서 새로운 정보를 빠르게 반영하지 못함
  - 따라서 sequence에서 distribution shift나 새로운 패턴에 적응하는 능력이 제한됨

- 해결 방법 :
  문제1 -> test time 적응 불가능한 고정된 hidden state 구조  
  방법1 -> hidden state 자체를 학습 가능한 파라미터로 취급해, test time에서 meta-learning 방식으로 업데이트 가능하게 구성

  문제2 -> 일반적인 meta-learning은 파라미터 업데이트를 별도 학습 루프에서 진행해야 함  
  방법2 -> RNN 내부에서 self-supervised loss를 통해 직접 hidden state를 업데이트하는 end-to-end 구조 제안 (gradient descent within the hidden state)

- 방법에대한 세부설명:
  - Expressive RNN (eRNN) 구조를 통해 hidden state를 'model within a model'처럼 동작하게 구성함
  - hidden state는 단순한 memory가 아니라 학습 가능한 파라미터처럼 gradient descent로 loss를 최소화하도록 업데이트됨
  - 이 업데이트는 test time에 수행되며, explicit supervision 없이 self-supervised loss를 기반으로 진행됨
  - 예: 현재 hidden state에서 다음 step 예측 loss를 계산하고, 이를 기반으로 hidden state를 inner gradient descent 방식으로 업데이트함
  - 전체 모델은 이 inner update까지 포함해 meta-learn되므로, test time에서도 일반화 및 적응력이 향상됨

- Recap :
  - 기존 RNN의 고정된 hidden state 구조는 test time 적응에 한계가 있음
  - eRNN은 hidden state를 학습 가능한 구조로 확장해, self-supervised 방식으로 test time에서도 loss를 최소화하도록 유도함
  - hidden state를 파라미터화하고, 모델 내에서 자체 gradient descent를 수행하게 만들어, meta-learning을 실시간으로 구현함
