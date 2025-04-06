## Sequence to Sequence Learning with Neural Networks  
#### 2025-04-06 / [https://arxiv.org/pdf/1311.2524](https://arxiv.org/pdf/1311.2524)

### Problem Statement
- 고정된 길이의 입력과 출력을 처리하는 기존 신경망 모델들은 입력과 출력의 길이가 다른 문제에 적절하지 않음.
- 예를 들어 기계 번역처럼 입력 문장과 출력 문장의 길이가 달라질 수 있는 문제에서는, 일반적인 feedforward 또는 고정된 구조의 RNN 모델로는 유연하게 대응하기 어려움.
- RNN의 hidden state로 문장을 요약하는 접근은 가능하지만, 긴 시퀀스에서는 정보 손실이 심각하며 효과적인 일반화가 어려움.

### Solution Approach
- 입력 시퀀스를 고정된 벡터로 인코딩한 후, 그 벡터를 기반으로 다른 시퀀스를 디코딩하는 **Sequence-to-Sequence (seq2seq)** 모델을 제안.
- 이를 위해 **두 개의 독립된 RNN (LSTM)** 네트워크 사용: 하나는 입력 시퀀스를 인코딩하고, 다른 하나는 그 벡터를 바탕으로 출력 시퀀스를 생성함.
- 입력 시퀀스를 **reverse**하여 학습 성능 향상 도모.

### Methodology Details
- **Encoder-Decoder 구조**:  
  - **Encoder LSTM**: 입력 시퀀스를 한 번에 입력받아 마지막 hidden state를 생성. 이 state가 전체 문장의 의미를 압축한 벡터로 작용함.
  - **Decoder LSTM**: 해당 벡터를 초기 상태로 받아 출력 시퀀스를 한 단계씩 생성함. 학습 시에는 이전 출력 토큰을 입력으로 넣는 **teacher forcing** 방식 사용.
  
- **Reverse input sequence**:
  - 입력 시퀀스를 역순으로 넣으면, 디코더가 더 빠르게 유의미한 정보를 받을 수 있어 학습 성능이 향상됨.
  - 저자는 이를 통해 gradient가 더 잘 흐르고, 장기 의존성 문제를 완화할 수 있음을 관찰.

- **LSTM 사용 이유**:
  - 기존 RNN은 장기 의존성(long-term dependency)을 처리하는 데 한계가 있음.
  - LSTM은 gating mechanism을 통해 이 문제를 해결하고, seq2seq 모델의 학습 성능을 대폭 향상시킴.

- **기계 번역 실험 (English-French)**:
  - WMT'14 영어-프랑스어 번역 데이터셋을 사용하여 학습.
  - 약 12-layer deep LSTM을 8 GPU에 걸쳐 분산 학습.
  - BLEU score 기준으로 기존 SMT 기반 모델들과 비교 가능한 성능을 달성함.

- **Inference**:
  - 디코딩 시에는 greedy decoding 또는 beam search 사용 가능.
  - 학습된 디코더는 초기 hidden state와 `<EOS>`가 나올 때까지 이전 출력을 입력으로 받아 순차적으로 다음 단어를 생성.

### Recap
입력 시퀀스를 인코딩한 후 이를 바탕으로 출력 시퀀스를 생성하는 seq2seq 구조를 통해, 기존의 고정 길이 입력-출력 한계를 극복하고 다양한 길이의 시퀀스를 처리하는 신경망 모델을 제안함. LSTM 기반의 encoder-decoder 아키텍처를 사용하여 기계 번역 작업에서 좋은 성능을 보였으며, 입력 시퀀스를 역순으로 처리하는 아이디어를 통해 gradient 흐름과 학습 효율을 개선함. 이는 이후 Attention 및 Transformer 모델의 전신 역할을 한 논문으로, 자연어 처리에서 시퀀스 기반 문제 해결의 중요한 전환점을 제시함.

---

이 논문은 seq2seq라는 프레임워크를 정립했다는 점에서 역사적 의미가 크며, 이후 등장하는 attention mechanism과 Transformer 아키텍처의 기반 개념들을 미리 탐색한 구조로 볼 수 있음. Hidden vector 하나로 모든 정보를 담는 구조는 한계가 있지만, 이는 다음 논문인 "Attention Is All You Need"에서 해결됨.
