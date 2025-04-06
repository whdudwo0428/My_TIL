## Learning to Learn at Test Time: RNNs with Expressive Hidden States  
#### 2025-04-06  
[https://arxiv.org/pdf/2407.04620](https://arxiv.org/pdf/2407.04620)  

### Problem Statement  
- 기존 RNN 구조는 **test-time adaptation**(테스트 시점에서의 적응 능력)이 제한적이며, 특히 **expressivity**(표현력)가 부족한 hidden state 구조로 인해 학습된 정보를 동적으로 업데이트하거나 기억을 유연하게 조절하는 능력이 떨어짐.  
- 최근 Transformer 기반 메모리 모델이나 external memory 기반 접근법들은 이 문제를 해결하려 했지만, 복잡한 구조와 높은 계산 비용이 수반됨.  
- 따라서, **단순하고 효율적이면서도 높은 표현력을 지닌 RNN 기반 아키텍처가 필요**함.  

### Solution Approach  
- 이 논문은 **기존 RNN의 Hidden State를 보다 expressive하게 설계**함으로써, 단순한 구조를 유지하면서도 **test-time에서의 강력한 적응 능력**을 가능하게 하는 새로운 아키텍처를 제안함.  
- 핵심은, hidden state를 단순 벡터로 유지하지 않고 **상태 간의 연산이 동적 매핑(dynamic mapping)을 학습할 수 있도록 확장**하는 것.  
- 구체적으로는, hidden state가 단순 state vector가 아니라 **함수(f) 자체**가 되도록 설계함으로써, **연속적인 memory 업데이트와 메타 러닝 성질**을 구현함.  

### Methodology Details  
- **Expressive Hidden State**는 일반적인 벡터가 아니라, 입력 시퀀스를 처리하며 학습된 **파라미터화된 함수**로 작동함.  
- 이 함수는 각 time step에서 입력에 따라 새로운 hidden state function으로 업데이트되며, 이는 다음 입력에 적응하는 방식으로 작동함. 즉, hidden state 자체가 **"learning algorithm"**이 되는 구조임.  
- 구조적으로는 다음과 같은 방식으로 정의됨:  
  - Hidden state \( h_t \)는 \( f_t(x_t) \)로 표현되며, \( f_t \)는 이전까지의 입력에 기반한 함수.  
  - 이때 \( f_t \)는 RNN cell 내부에서 재귀적으로 정의되며, 고정된 파라미터가 아닌 **동적으로 업데이트되는 파라미터**를 가짐.  
  - 이러한 구조 덕분에 **test-time adaptation**이 자연스럽게 가능해짐.  
- 논문은 이 구조를 **meta-RNN**이라 부르며, 일반적인 RNN에 비해 훨씬 expressive한 memory 동작을 보임.  
- 다양한 synthetic task (e.g., Copy, Reverse, Add, etc.) 및 실제 시계열 적응 문제에서, 기존 LSTM, GRU, Transformer보다 더 우수하거나 비교 가능한 성능을 보여줌.  

### Recap  
이 논문은 기존 RNN의 한계를 극복하기 위해 **hidden state를 함수화(Functional Hidden State)**하여 RNN이 **학습 알고리즘 자체를 내재**할 수 있도록 만드는 새로운 아키텍처를 제안한다. 이를 통해 모델은 test-time에서 적응할 수 있는 능력을 갖추게 되며, 구조는 단순하지만 expressive한 meta-learning 구조로 작동한다. Hidden state는 단순한 벡터가 아니라 동적으로 변화하는 함수이며, 이를 통해 memory update와 적응을 동시에 수행할 수 있다.  

### 한계 및 향후 방향  
- 논문은 아직까지 relatively simple한 task에 초점을 맞추고 있으며, **대규모 실제 데이터셋에서의 성능 검증**은 부족한 편이다.  
- 향후 expressive hidden state 구조를 기반으로 한 **multi-modal 학습, long-context memory, continual learning**과의 결합이 유망해 보인다.
