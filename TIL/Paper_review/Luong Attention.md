## Effective Approaches to Attention-based Neural Machine Translation  
#### 2025-04-04

### Problem Statement
- Bahdanau Attention 이후로 sequence-to-sequence 모델에서 attention 메커니즘은 중요한 구성 요소가 되었지만, **구현 방식과 성능에 영향을 미치는 다양한 설계 선택들**은 체계적으로 비교된 바가 없었다.
- 특히, alignment function(어텐션 score 계산 방식), global vs local attention, input feeding 등 세부 설계는 논문마다 다르게 적용되어 있어 **성능과 효율 측면에서 어떤 방식이 효과적인지에 대한 정리가 필요**했다.

### Solution Approach
- 본 논문은 Bahdanau의 soft attention 구조를 기반으로, 여러 attention 설계 요소들을 체계적으로 분석하고 개선한다.
- 주요 개선점은 다음 세 가지다:
  1. **간결하고 계산 효율적인 attention score 함수 도입**
  2. **local attention 기법 제안**
  3. **input feeding 방식 도입으로 디코더 정보 흐름 강화**

### Methodology Details

#### 1. Attention Score Function
- Bahdanau는 feedforward neural network 기반 score를 사용했지만, 이 논문은 다음과 같은 **단순하고 효율적인 score 방식**들을 비교 제안한다:
  - dot (내적)
  - general (weight 행렬 곱)
  - concat (Bahdanau 스타일)

- 실험 결과, dot 방식은 가장 간단하면서도 성능이 우수한 경우가 많았고, 학습 속도도 빠르다.

#### 2. Global vs Local Attention
- **Global attention**: 디코더가 매 시점마다 인코더 전체를 대상으로 soft attention을 수행
- **Local attention**: 디코더가 현재 출력 단어와 관련 있는 **일부 입력만 집중**하도록 제한
  - hard monotonic alignment에 가까운 방식
  - 위치 기반 또는 예측 기반으로 주변 context window를 정해 attention 수행

- local attention은 속도와 효율성에서 이점이 있으며, 짧은 문장이나 실시간 처리에서 유리함

#### 3. Input Feeding
- 이전 디코더 출력과 context 벡터를 함께 다음 디코더 입력에 넣는 방식
- 이 구조는 attention 결과가 디코더 상태에 순차적으로 반영되도록 하여, **출력 간의 일관성과 정렬 품질을 높이는 효과**를 가진다
- Bahdanau Attention에서는 각 시점이 독립적이지만, 여기서는 context가 시계열적으로 연결됨

#### 4. 실험 결과
- WMT English-German, English-French 데이터셋 기준으로, local attention과 input feeding이 성능 향상에 효과적
- 단순한 dot product score가 연산 속도 및 정확도 측면에서 좋은 성능을 보임
- attention 가중치 시각화를 통해 local 구조가 더 정확한 alignment를 유도함

### Recap
Luong Attention은 Bahdanau Attention을 기반으로, **score 계산 방식 단순화**, **local attention 도입**, **input feeding을 통한 정보 흐름 강화** 등 실제 번역 성능과 연산 효율을 높이는 다양한 설계 개선을 제안한다. 이 논문은 attention 설계의 다양한 변형을 실험적으로 정리한 기준점 역할을 하며, 이후 Transformer로 넘어가기 전까지 가장 많이 사용된 attention 구조로 자리 잡았다.

---

**한계점 및 후속 발전 방향**  
- local attention은 효과적이지만, 입력과 출력의 정렬이 강하게 대응되는 경우에만 적합하며, 자유로운 word order에는 한계가 있다  
- 이후 Transformer에서는 position embedding과 self-attention을 결합하여 global context를 완전히 병렬적으로 처리함으로써, attention 구조를 더 유연하고 확장 가능하게 만들었다
