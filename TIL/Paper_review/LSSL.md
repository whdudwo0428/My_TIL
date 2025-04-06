## LSSL: Linear State-Space Layers for Sequence Modeling  
#### 2025-03-04 ~ 03-12 / [https://arxiv.org/abs/2210.01795](https://arxiv.org/abs/2210.01795)

### Problem Statement
- Transformer는 우수한 시퀀스 처리 능력을 보이지만, **quadratic한 연산 복잡도와 긴 시퀀스 처리의 비효율성**이 문제로 지적되어 왔다.
- 반대로 S4와 같은 Structured State Space Model은 이론적으로 뛰어난 long-range dependency 모델링 능력을 보유하지만, **구현 복잡성, 계산량, 학습 효율성** 측면에서 접근성이 낮다.
- 따라서 **간결하면서도 효율적이고, long-context sequence도 잘 처리할 수 있는 구조**가 필요하다.

### Solution Approach
- LSSL은 SSM 기반 구조의 장점을 유지하면서도 **선형적으로 동작하는 매우 단순한 구조의 Layer**를 제안한다.
- 핵심은 **입력 시퀀스를 선형 필터로 처리하는 구조**를 채택하고, 이 필터의 핵심 파라미터(A, B, C, D)를 간결하게 구성하여 **높은 계산 효율과 학습 안정성**을 달성하는 것이다.

### Methodology Details

#### 1. Layer 구조
- LSSL은 일반적인 SSM 구조처럼 A, B, C, D 행렬을 사용하지만, 학습 가능한 파라미터 수를 제한하고 효율적 구현에 집중한다.
- 학습 중에는 입력 시퀀스 \( u \)에 대해 출력 \( y \)를 다음과 같은 convolution-like 연산으로 처리한다:

  - 출력 = 입력에 필터 커널을 선형적으로 적용 (즉, 1D convolution 형태)
  - 이 필터는 SSM의 해석적 해에 기반한 형태로, **frequency domain에서 계산 가능**하도록 설계됨

#### 2. Efficiency와 병렬성
- 기존 SSM은 recurrence 구조 때문에 병렬화가 어렵지만, LSSL은 convolution 구조로 구현되므로 **완전한 병렬 처리 가능**
- 특히 FFT 기반 구현이 가능해 long sequence 처리에서도 효율적이다

#### 3. 구조적 단순성과 확장성
- S4는 HiPPO 기반의 엄격한 A matrix 구조를 따르지만, LSSL은 **임의의 A 구조를 자유롭게 선택 가능**
- 예를 들어 diagonal A, normal A 등 다양한 구조 실험이 가능하며, 이는 유연한 실험과 task 맞춤 최적화를 가능케 한다

#### 4. 실험 결과
- LSSL은 다양한 long-range 시퀀스 벤치마크 (Long Range Arena, Speech, Language Modeling 등)에서 **Transformer나 기존 SSM 계열 대비 뛰어난 성능과 효율성**을 달성함
- 특히 계산량 측면에서 매우 유리하고, 학습도 안정적임

### Recap
LSSL은 복잡한 recurrence나 상태 추적 없이도 SSM의 장점을 그대로 가져오면서, 입력 시퀀스를 선형 필터로 처리하는 구조를 제안한다. 이 방식은 기존 SSM과 달리 완전히 병렬화 가능하며, frequency domain에서도 효율적으로 계산할 수 있다. 구조는 간단하지만 표현력은 높고, 다양한 시퀀스 처리 작업에서 높은 정확도와 효율을 보인다. S4처럼 복잡하지 않으면서도 Transformer를 대체할 수 있는 실용적인 long-range sequence layer의 유력한 대안으로 평가받는다.

---

**한계점 및 후속 발전 방향**
- 고정된 filter structure는 매우 길거나 구조가 복잡한 의존 관계 모델링에 제한이 있을 수 있다  
- 이후 **Mamba**에서는 gating 메커니즘을 결합하여 expressive power를 높이고, LSSL의 구조적 단순성과 효율성을 그대로 계승함
