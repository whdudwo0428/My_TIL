## HiPPO: Recurrent Representations for Structured Continuous-Time Memory  
#### 2025-03-04 ~ 03-12 / [https://arxiv.org/abs/2008.07669](https://arxiv.org/abs/2008.07669)

### Problem Statement
- 기존 RNN이나 LSTM은 시계열 데이터를 처리할 때 최근 입력에는 민감하지만, **오래된 정보는 점차 소실되는 구조적 한계**를 갖는다.
- 특히 연속 시간 기반 데이터에서는 이산적인 hidden state 업데이트만으로는 **모든 과거 정보를 효율적으로 요약**하기 어렵다.
- 따라서 **과거 입력 전체를 시간에 따라 압축하고 유지할 수 있는 메모리 표현 구조**가 필요하다.

### Solution Approach
- HiPPO (Higher-order Polynomial Projection Operator)는 입력 시퀀스를 하나의 연속적인 함수로 간주하고, **그 함수를 일정 기준에 따라 압축 요약하는 방법**을 제안한다.
- 이때 사용하는 기준은 특정한 **기저 함수** (basis function)로, 예를 들어 Legendre 다항식, Laguerre 함수 등을 사용할 수 있다.
- 입력 함수의 정보를 이러한 기저 함수에 투영 (projection)하면서, 전체 이력을 요약하는 메모리 벡터를 재귀적으로 업데이트한다.

### Methodology Details

#### 1. Projection-based Memory Update
- 입력 시퀀스는 연속 함수로 해석되며, 그 함수의 정보를 **기저 함수**에 맞춰 projection한다.
- 이 projection 결과를 hidden state처럼 다루며, 시간이 지남에 따라 recurrence 형태로 업데이트한다.
- 이 업데이트는 선형 시스템 형태로 표현되며, 다음과 같은 구성 요소를 가진다:
  - **A matrix**: 시간에 따른 dynamics를 정의
  - **B vector**: 입력값을 상태에 반영하는 방식 정의
  - **Hidden state**: 과거 전체 정보를 요약한 압축된 표현

#### 2. 다양한 HiPPO 인스턴스
- 기저 함수의 종류에 따라 서로 다른 HiPPO 구조가 정의된다:
  - **HiPPO-LegS**: Legendre polynomial 기반의 대표적인 구조. 연속 시간에 강한 특성을 보임.
  - **HiPPO-LagT**: Laguerre 함수 기반으로, 시간 감쇠 특성을 자연스럽게 반영함.
- 이 구조들은 학습 가능한 파라미터가 아니며, **사전 정의된 A, B 행렬 구조로 구성**된다.

#### 3. 연속 메모리 표현
- 일반적인 RNN은 discrete step마다 hidden state를 갱신하지만, HiPPO는 시간 미분 형태를 기반으로 메모리를 구성한다.
- 따라서 연속 시간 상에서 정보를 유지하거나 업데이트할 수 있으며, irregular sampling이나 시계열 예측 문제에 효과적이다.

#### 4. 활용 및 파급
- HiPPO는 단독으로 사용할 수도 있지만, 이후 등장하는 모델들의 **이론적 기반이자 핵심 구성요소**로 쓰인다:
  - **S4** (Structured State Space Sequence model)에서는 HiPPO의 A, B를 convolution kernel로 해석하여 병렬 계산 구조로 확장
  - **Mamba**에서는 gating 메커니즘과 결합해 expressivity를 높임
  - **Titan**, **Physion**, **Mamba2** 등에서도 연속 메모리 표현의 핵심 요소로 사용됨

### Recap
HiPPO는 시계열 입력의 과거 이력을 **기저 함수 기준으로 projection하여 요약 표현하는 메모리 구조**이다. RNN이나 LSTM과 달리 discrete step 단위가 아닌 연속적인 형태로 정보를 압축 저장하며, A matrix와 B vector를 이용해 recurrent하게 hidden state를 업데이트한다. 이 구조는 이후 등장한 **S4**, **Mamba**, **Titans** 등의 구조적 기반이 되었으며, 특히 long-context memory나 irregular sampling이 중요한 문제에서 강력한 성능을 발휘한다.

---

**한계점 및 후속 발전 방향**  
- A, B 행렬은 이론적으로 정의되기 때문에 **유연성이 떨어지며, task-specific 학습이 어려움**  
- 이후 **S4**는 학습 가능한 convolution kernel로 이를 확장했고, **Mamba**는 gating을 결합해 더 expressive한 구조로 발전함  
- **Titans** 계열에서는 HiPPO 기반 메모리를 더욱 일반화해 test-time adaptation 능력까지 부여함
