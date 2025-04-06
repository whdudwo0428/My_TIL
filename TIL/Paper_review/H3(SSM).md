## Hungry Hungry Hippos: Towards Language Modeling with State Space Models  
#### 2025-03-04 ~ 03-12 / [https://arxiv.org/abs/2212.14052](https://arxiv.org/abs/2212.14052)

### Problem Statement
- Transformer 기반 언어 모델은 뛰어난 성능을 보이지만, **quadratic 연산 복잡도와 길이에 비례하는 메모리 요구**로 인해 긴 시퀀스 처리에서 비효율적이다.
- State Space Model (SSM) 계열은 이산 시간의 recurrence를 이용해 **long-context dependency와 효율적인 메모리 사용**이 가능하지만, 기존 모델들은 **언어 모델링 성능에서 Transformer 대비 부족**한 면모를 보여왔다.
- 따라서 SSM 기반 구조를 유지하면서도 **Transformer 수준의 표현력과 언어 모델링 성능을 확보하는 것**이 주요 목표다.

### Solution Approach
- 본 논문에서는 **H3:Hungry Hungry Hippos**라는 이름의 **hybrid architecture**를 제안한다.
- H3는 **SSM 구조와 attention-like 기제의 융합**을 통해 Transformer가 처리하는 복잡한 언어 구조를 포착하면서도, SSM 특유의 **학습 안정성과 효율성**을 유지한다.
- 특히 Induction Head, Associative Recall 등 Transformer의 강점을 필요로 하는 task에서 기존 SSM 모델보다 훨씬 높은 성능을 보인다.

### Methodology Details

#### 1. 구조적 배경
![image](https://github.com/user-attachments/assets/eae95981-6a86-40ce-b94a-2204288ee5dd)
- 이를 convolution kernel로 변환하면 **parallelizable하고 long-context 처리에 강한 구조**가 된다.
- 하지만 기존 SSM은 **token 간 상호작용과 symbol-to-symbol 연산이 약함** → Transformer처럼 symbol binding 기능 필요

#### 2. H3 Layer 설계
- H3는 입력 시퀀스 \( x \)에 대해 다음 세 가지 흐름을 설계:
  1. **Key 흐름**: 과거 입력 정보를 delay-convey 구조로 흐르게 함 (SSM 기반 shift 적용)
  2. **Value 흐름**: Key와 동일한 방식으로 시간 축 이동
  3. **Query**: 현재 입력으로부터 생성, Key–Value 흐름과 element-wise로 상호작용

- 최종 연산은 다음과 같이 구성됨 (수식 없이 설명):
  - Key는 시간 축으로 지연되며 이전 정보를 전달
  - Value도 Key와 같은 시간 흐름을 따름
  - Query는 현재 입력 기준으로 필요한 정보를 선택적으로 추출
  - 전체 연산은 Conv1D 기반 구조로, 병렬 처리 및 GPU 가속에 적합

#### 3. Gated State Space 설계
- H3는 단순한 SSM recurrence가 아닌 **Gate 연산을 추가한 Gated SSM 구조**를 사용해 표현력을 강화함
- 이로써 attention 없이도 sequence 내 정보를 위치에 따라 다르게 조절할 수 있게 됨

#### 4. 실험: Expressivity Task
- **Induction Head**: 특정 토큰 이후의 정보를 기억하고 추론하는 task
- **Associative Recall**: Key–Value 쌍을 기억하고 Key에 해당하는 Value를 회상하는 task

| Task | Random | S4D | Gated SSM | H3 | Attention |
|------|--------|-----|------------|----|-----------|
| Induction Head | 5.0 | 35.6 | 6.8 | 100.0 | 100.0 |
| Associative Recall | 25.0 | 86.0 | 78.0 | 99.8 | 100.0 |

- 위 표에서 보듯이, **H3는 Transformer 수준의 성능을 expressivity task에서 구현**함

#### 5. Language Modeling 성능
- Pile, WikiText, enwik8 등 다양한 benchmark에서 실험
- **S4D 대비 더 우수하거나 유사한 perplexity 성능**, Transformer 수준에 근접

### Recap
Hungry Hungry Hippos (H3)는 기존 SSM 모델의 한계였던 symbol-level reasoning 부족 문제를 극복하고자, **SSM 흐름과 query-based filtering을 결합한 hybrid 구조**를 제안한다. Key–Value 흐름을 delay-convey 구조로 시간 축에 따라 생성하고, 현재 입력으로부터 생성된 Query가 이를 필터링한다. 이 구조는 expressivity가 뛰어나며, Induction Head, Associative Recall 같은 task에서도 Transformer와 동등한 성능을 낸다. H3는 이후 Mamba 구조로 자연스럽게 확장되며, 고성능 SSM 기반 언어 모델의 새로운 지평을 열었다.

---

**한계점 및 후속 발전 방향**  
- 구조가 기존 SSM보다 복잡하고, 연산 흐름의 설계가 명시적이므로 최적화 여지가 있음  
- 이후 **Mamba**는 이러한 흐름을 더 추상화하여 학습 가능한 state update 함수로 재구성하고, gating 구조를 자연스럽게 통합하여 더욱 유연한 확장 모델로 발전함
