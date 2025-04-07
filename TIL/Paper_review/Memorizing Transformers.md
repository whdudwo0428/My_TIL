## Memorizing Transformers  
#### 2025-04-04  


### Problem Statement  
- Transformer 기반 모델은 긴 컨텍스트를 기억하거나 복잡한 연관 정보를 저장하는 데 한계가 있음.  
- 특히, **지금까지 본 적 없는 새로운 테스트 시간(test-time) 정보**를 빠르게 기억하거나 사용할 수 있는 메커니즘이 부족함.  
- 이로 인해 few-shot learning이나 test-time adaptation이 필요한 상황에서 한계를 가짐.

### Solution Approach  
- 이러한 문제를 해결하기 위해, 저자는 **Key-Value Memory 구조를 Transformer에 통합**한 **Memorizing Transformer**를 제안.  
- 모델이 훈련 또는 추론 중 마주치는 정보들을 외부 메모리에 저장하고, 필요할 때 검색하여 사용하는 구조로, 기억과 검색이 핵심.  
- 핵심 아이디어는: **유사한 이전 경험을 빠르게 검색하고, 그로부터 유용한 정보를 추론에 활용**하는 것.

### Methodology Details  
- **Memory Structure**:  
  - 메모리는 (key, value) 쌍으로 이루어져 있으며, key는 과거의 hidden state, value는 해당 시점의 정보를 나타냄.  
  - 이 메모리는 **훈련 도중 혹은 테스트 도중에도 축적**될 수 있고, 특정 조건에서만 업데이트됨 (e.g., token rarity).  

- **Memory Retrieval**:  
  - 현재 입력 토큰의 hidden state를 query로 사용하여, memory에 있는 key들과의 거리(코사인 유사도 기반)를 측정하여 k-NN 방식으로 가장 유사한 값을 검색함.  
  - 검색된 값(value)은 Transformer의 self-attention 결과와 함께 fused 되어 최종 예측에 사용됨.  

- **Training Strategy**:  
  - 학습 중에도 memory를 동적으로 업데이트함. 특히 **rare token**일 경우 memory에 저장하도록 설계됨.  
  - 학습 과정에서 이 memory는 지워지지 않으며, 이후 test-time에도 그대로 유지되어 inference에서 도움을 줌.  

- **Architectural Integration**:  
  - 기존 Transformer block 안에 memory-based attention 모듈이 삽입되어 self-attention과 병렬적으로 동작하거나 가중합되어 통합됨.  
  - 학습된 메모리는 공유되거나 개별적으로 유지될 수 있음.  

- **Benchmarks**:  
  - **Language modeling** (PG-19, Books3), **Algorithmic reasoning** (Lookup task), **Few-shot learning** (in-context tasks) 등 다양한 벤치마크에서 평가.  
  - 기존 Transformer와 비교해 특히 긴 거리(long-range dependency) 및 test-time adaptation 성능에서 우수함을 보임.

### Recap  
Memorizing Transformer는 test-time에 새롭게 등장하는 정보를 기억하고 활용할 수 있도록 **외부 Key-Value Memory 구조**를 Transformer에 통합한 모델이다.  
이 memory는 과거 hidden state를 key로, 연관된 정보를 value로 저장하며, 현재 입력과 유사한 key를 검색해 대응되는 value를 추론에 활용한다.  
특히 rare token 위주로 memory를 업데이트하고, 학습 중 축적된 memory를 test-time에서도 그대로 활용함으로써 일반 Transformer 대비 **장기 기억 능력과 적응성**에서 뛰어난 성능을 보인다.  
이는 Transformer의 구조적 한계였던 고정 context window와 limited capacity 문제를 메모리 기반 접근으로 해결한 중요한 진전으로 평가된다.  

- 주요 한계로는 memory 검색 비용(k-NN), memory 크기 관리, 희귀성 기반 업데이트의 하드코딩적 기준 등이 있으며, 향후 더 동적인 memory 관리 전략이 필요함.
