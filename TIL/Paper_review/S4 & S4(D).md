## S4 & S4D: Efficiently Modeling Long Sequences with Structured State Spaces + 효율적 변형 및 적용
#### 2025-03-04 ~ 03-12 / [https://arxiv.org/abs/2111.00396](https://arxiv.org/abs/2111.00396), [https://arxiv.org/abs/2206.11893](https://arxiv.org/abs/2206.11893)

### Problem Statement
- Transformer 기반 모델은 시퀀스 전 범위의 관계를 모델링할 수 있지만, **quadratic한 attention 연산**으로 인해 **long sequence 처리에 비효율적**이다.
- 기존 RNN은 시간 순서에 따른 연산이 필수이기 때문에 **병렬화가 어렵고 gradient 흐름이 불안정**해 long-range dependency를 포착하기 힘들다.
- 따라서 **길이가 수천~수만에 이르는 시퀀스도 병렬적으로 처리할 수 있으면서**, **안정적인 학습과 long-range expressivity를 모두 갖춘 새로운 시퀀스 모델**이 필요하다.

### Solution Approach
- **S4** (Structured State Space Sequence model)는 시계열 전체를 처리하는 **State Space Model : SSM**을 구조적으로 재해석하여, 이를 **convolution 형태로 효율적으로 구현**하는 방법을 제안한다.
- **S4D**는 S4의 효율성을 더욱 높이기 위해 A matrix를 단순한 **diagonal 구조로 제약**함으로써, 학습 안정성과 계산 성능을 향상시킨 변형 모델이다.

### Methodology Details

#### 1. 기본 구조 (S4)
- 입력 시퀀스 u(t)를 **state vector** x(t)를 통해 처리하는 continuous-time linear system을 기반으로 구성:

  - 시스템의 핵심 구성은 다음과 같은 선형 recurrence에 기반한다:
    - **A matrix**: 내부 state dynamics를 정의
    - **B vector**, **C vector**: 입력과 출력을 잇는 입출력 계수
    - **Discretization**: continuous system을 시퀀스 데이터에 맞춰 이산화

- 이 시스템은 **convolution kernel로 변환 가능**하며, 긴 시퀀스에 대해 **1D convolution**으로 빠르게 처리할 수 있다.

#### 2. Efficient Implementation
- 시간 복잡도는 O(L*log L)수준의 FFT 기반 convolution으로 낮추었으며,
- 병렬 연산이 가능하기 때문에 Transformer처럼 **batch-level 병렬 학습**이 가능하다.

#### 3. HiPPO 기반 A matrix 설계
- S4는 **HiPPO-LegS**에서 유도된 특정 구조의 A matrix를 사용해, **최근 입력뿐 아니라 과거 입력 전체를 효과적으로 요약**할 수 있도록 설계되었다.
- 이 덕분에 S4는 **long-range memory**가 매우 강력하며, gradient 흐름도 안정적이다.

#### 4. S4D (Diagonal S4)
- A matrix를 일반 복소 행렬이 아닌 **diagonal 행렬**로 단순화하여 효율성과 안정성을 개선
- 이로 인해 S4보다 **메모리 사용량과 연산량이 감소**, 학습 안정성은 향상됨
- 복잡도는 줄였지만 성능은 S4와 거의 동등하거나 더 나은 경우도 있음

#### 5. 실험 및 성능
- **Long Range Arena (LRA)** 등 다양한 long-context benchmark에서 S4는 Transformer, LSTM, TCN 등을 능가
- S4D는 S4보다 가볍지만 대부분의 벤치마크에서 유사한 성능을 유지
- 특히 **speech, genomics, time-series forecasting**에서 강력한 성능 보임

### Recap
S4는 structured state space model을 기반으로 설계된 시퀀스 모델로, **long-range memory와 병렬 처리 능력을 동시에 갖춘** 구조이다. S4는 입력 시퀀스를 convolution kernel 형태로 처리하며, HiPPO에서 유도된 A matrix를 이용해 과거 정보를 정확하게 요약하고 전달할 수 있다. S4D는 이를 diagonal A matrix 구조로 단순화하여 학습 안정성과 효율성을 더 높인 버전이다. 두 모델 모두 Transformer의 한계를 넘는 새로운 long-context modeling의 핵심 프레임워크로 평가받고 있다.

---

**한계점 및 후속 발전 방향**  
- S4는 A matrix가 복소수이므로 **학습과 구현이 어렵고** 복잡도가 상대적으로 높음  
- S4D는 이 문제를 해결했지만, 여전히 gating이나 dynamic update 같은 **적응 능력은 부족함**  
- 이후 **Mamba**에서는 gating을 결합하고, **Titans**에서는 test-time adaptation까지 확장되며 S4를 대체 또는 일반화하는 방향으로 발전함
