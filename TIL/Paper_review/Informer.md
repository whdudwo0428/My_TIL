## Informer: Beyond Efficient Transformer for Long Sequence Time-Series Forecasting

#### 2025-08-13

### Problem Statement

* 기존 Transformer 기반 시계열 예측 모델은 **Self-Attention의 O(L²) 연산 복잡도**로 인해 긴 시퀀스(long sequence) 입력 처리 시 연산량과 메모리 사용량이 매우 커진다.
* 일반적인 시계열 데이터는 **복잡한 잡음** (noise)과 **긴 범위 의존성** (long-term dependency)이 혼합되어 있으며, 이를 효율적으로 추출하지 못하면 예측 성능이 저하된다.
* Encoder-Decoder 구조에서 **디코더 입력 길이가 길어질수록** 예측 효율성이 떨어지고 누적 오차가 커지는 문제가 발생한다.

### Solution Approach

* 긴 시계열 입력에서도 효율적인 Attention 계산을 위해 **ProbSparse Self-Attention**을 도입하여 **O(L log L)** 수준으로 연산량을 줄인다.
* **Distilling-based Encoder 구조**를 적용해 계층이 깊어질수록 시계열 길이를 점진적으로 줄이며 정보 밀도를 높인다.
* 디코더에는 **Generative-style Decoder**를 적용하여 한 번의 forward pass로 전체 예측 구간을 출력, 누적 오차를 줄인다.

### Methodology Details

* **ProbSparse Self-Attention**

  * 모든 Query-Key 조합을 계산하지 않고, 정보량이 많은 (큰 magnitude의) Query에 대해서만 Attention을 계산.
  * 이로써 긴 시퀀스에서도 메모리와 연산량을 크게 절감.
* **Distilling Encoder**

  * 각 Encoder Layer 뒤에 시퀀스 다운샘플링 레이어를 두어 시계열 길이를 절반으로 줄임.
  * 이는 깊은 네트워크 구조에서 장기 의존성을 더 압축적으로 학습 가능하게 함.
* **Generative Decoder**

  * Autoregressive 방식 대신 병렬적으로 전체 예측 시퀀스를 생성.
  * 예측 시 디코더 입력 길이를 줄이고, 학습 과정에서도 효율성을 높임.
* **기타 설계 요소**

  * 시계열 특화 Positional Encoding
  * 다변량 (multivariate) 시계열 입력 지원
  * 표준 시계열 예측 벤치마크 데이터셋에서 Transformer 대비 성능 및 속도 개선 검증

### Recap

이 논문은 긴 시계열 예측에서 기존 Transformer의 **O(L²) 연산량 문제**와 **누적 오차 문제**를 해결하기 위해,

* 중요 Query만 사용하는 **ProbSparse Self-Attention**
* 다운샘플링 기반 **Distilling Encoder**
* 병렬 예측 가능한 **Generative Decoder**
  를 결합한 **Informer** 모델을 제안했다.
  이를 통해 긴 시계열에서도 메모리와 연산량을 절감하면서 장기 의존성을 효율적으로 학습하고, 빠르고 정확한 예측을 가능하게 했다.
