## Mamba: Linear-Time Sequence Modeling with Selective State Spaces  
#### 2025-03-04 ~ 03-27 / [https://arxiv.org/abs/2312.00752](https://arxiv.org/abs/2312.00752)

### Problem Statement
- Transformer는 시퀀스 전체를 다룰 수 있는 표현력을 지녔지만, **quadratic 연산 복잡도**로 인해 긴 시퀀스 처리에 비효율적이다.
- 반면, SSM 계열 모델들은 **long-context modeling**과 **linear-time 연산**이 가능하지만, Transformer가 처리할 수 있는 **복잡한 패턴과 symbol-level reasoning 능력이 부족**하다.
- 특히 H3 계열 모델들은 expressivity를 보완하려 했지만, 여전히 **핵심 구성(shift-convey-filter 흐름)이 고정 구조**라서 표현력에 한계가 있었다.
- 따라서 **효율성과 표현력을 모두 갖춘 SSM 기반 대안 구조**가 필요하다.

### Solution Approach
- **Mamba**는 기존 SSM 구조를 유지하면서도, **state update를 token마다 선택적으로 조절할 수 있는 gating 구조**를 도입한 모델이다.
- 기존 H3가 수동적으로 정의된 흐름을 따랐다면, Mamba는 그 흐름을 **학습 가능한 모듈로 일반화**한다.
- 이를 통해 **symbol-aware, input-dependent, and token-specific 연산**이 가능해졌고, 구조는 RNN과 유사하지만 **완전히 병렬화 가능한 구조**로 구현된다.

### Methodology Details

#### 1. Selective State Space Model 구조
- 핵심은 다음의 **학습 가능한 selective recurrence 구조**에 있다:

  - state는 시점마다 업데이트되며, 각 token마다 다른 방식으로 상태를 갱신함
  - token별 update는 다음 요소로 조절됨:
    - **Δ (Delta)**: 입력 간 시간 간격 또는 step 크기
    - **A, B**: SSM dynamics를 조절하는 학습 가능한 파라미터
    - **Input gate**: 입력을 얼마나 받아들일지 결정
    - **Forget gate**: 과거 상태를 얼마나 유지할지 결정

- 이러한 구조는 H3가 고정적으로 수행했던 shift-convey-filter 흐름을 **학습 가능하고 유연한 방식으로 재정의**한 것

#### 2. 연산 흐름
- Mamba의 token 처리 흐름은 다음과 같은 단계를 거친다:

  1. 입력 \( x \)는 선형 변환되어 gating과 recurrence 연산에 쓰일 feature로 분기됨
  2. 각 token은 개별적으로 Δ, A, B, Gating 값에 따라 상태를 업데이트
  3. 최종적으로 hidden state가 다음 layer 또는 출력으로 전파됨

- 이 모든 연산은 **scan 연산**(prefix-scan, associative op)을 통해 **병렬화 가능**

#### 3. 효율성
- 전체 연산은 linear complexity를 유지하며, GPU에서도 병렬로 효율적으로 작동
- CUDA kernel 최적화가 적용되어 inference latency가 매우 낮음

#### 4. 성능
- **Language modeling** (The Pile, enwik8, PG-19, Books3 등)에서 GPT-2, LLaMA 수준의 모델과 대등하거나 상회
- **Induction Head, Associative Recall, SCAN, PathX** 등 expressivity task에서도 Transformer급 성능 달성
- 특히 시퀀스 길이에 따라 성능이 감소하지 않고, **scaling law** 상에서도 매우 유리함

### Recap
Mamba는 기존 SSM 구조를 기반으로 하면서도, **token마다 선택적으로 상태를 갱신할 수 있는 selective recurrence 구조**를 도입해 표현력을 크게 확장한 모델이다. 이는 H3처럼 shift-convey-filter 흐름을 따르지 않고, 각 token의 입력 정보에 따라 **상태를 유연하게 업데이트**하는 구조로, RNN의 시점별 순차 구조와 Transformer의 병렬성을 절묘하게 통합했다. Mamba는 긴 시퀀스에서 효율적으로 작동하며, GPT-2나 LLaMA 등 고성능 모델과 견줄 수 있는 성능을 달성했다.

---

**한계점 및 후속 발전 방향**  
- gating이 추가되면서 구조가 복잡해지고, **이론적으로는 Transformer보다 해석이 어렵다**  
- 시각적으로는 attention map이 없어, **모델이 어떤 정보를 보는지 직관적으로 해석하기 어려움**  
- 이후 **Mamba-2**, **PhysMamba**, **Titan** 등은 이를 더 일반화하거나 test-time adaptation 능력까지 확장하며 발전 중임
