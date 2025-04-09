## Titans: Learning to Memorize at Test Time  
#### 2025-04-09

### Problem Statement
- Sequence modeling에서 RNN, Transformer, SSM 계열 모델은 대부분 *training time*에 메모리 능력을 학습하고, 이를 기반으로 *test time*에서도 작동한다.  
- 하지만 이러한 방식은 *training-test distribution mismatch*에 취약하며, 특히 **test-time에 novel한 pattern**이나 **long-range dependency**를 다룰 수 있는 **유연한 memorization 능력**이 부족하다.  
- 기존 Transformer는 attention을 통해 soft memory를 제공하지만, memory가 고정되어 있고 *pre-trained weights*에 의존하기 때문에 **test-time adaptation**이 불가능하다.  
- 기존의 SSM 기반 모델(S4, Mamba 등)도 hidden state에 memory를 저장하지만, **모델이 학습되지 않은 sequence에 대해 memory를 재구성하거나 업데이트하는 능력은 제한적**이다.

### Solution Approach
- 이러한 문제를 해결하기 위해 Titans는 **test-time에 memory를 직접 조정하고 학습 가능한 구조를 갖는 SSM 기반 모델**을 제안한다.
- 핵심 아이디어는 **SSM state를 parameterized update rule로 재정의하여, test-time에 memory manipulation이 가능하게 하는 구조를 설계**하는 것이다.
- 이로써 Titans는 *training-free adaptation*을 통해 unseen sequence에 대해서도 능동적으로 memory를 형성하고 활용할 수 있다.

### Methodology Details
- Titans는 기존의 **structured state space model (SSM)**의 recursion 구조인  
  `h_{t+1} = A h_t + B x_t`  
  를 확장하여, **state transition matrix A와 input matrix B를 test-time adaptive하게 조정**할 수 있도록 설계한다.
  
- 이를 위해 Titans는 다음과 같은 세 가지 주요 구성 요소를 포함한다:

  1. **Learnable Memory Dynamics**:  
     - 기존 SSM에서는 A, B가 fixed parameter였다면, Titans는 **gating mechanism**과 **test-time learnable parameters**를 통해  
       `A_t, B_t`가 sequence에 따라 동적으로 변하는 구조를 채택한다.

  2. **Memory Editor (Test-time Optimizer)**:  
     - test input이 주어졌을 때, **loss-free** 기준으로 memory를 업데이트하는 경사 기반 editing 방식을 도입.  
     - 이를 위해 **online inner-loop optimization**을 통해 hidden state update를 조정함.  
     - 다시 말해, 모델은 output을 만들기 전에 test sequence를 기반으로 internal memory를 먼저 튜닝한다.

  3. **Memory Loss-Free Training**:  
     - training time에는 memory editing이 없이 SSM 형태로 학습하고,  
     - test-time에만 memory editing 모듈이 작동하여 **inference-only adaptation**이 가능함.  
     - 이는 meta-learning의 MAML 방식과 유사한 개념을 memory에만 적용한 구조로 이해할 수 있다.

- Titans는 다양한 synthetic 및 real-world long-range tasks (Copy, Induction Head, SCAN 등)에서 S4, Mamba, Transformer보다 더 뛰어난 generalization과 adaptation 성능을 보인다.

### Recap
Titans는 test-time에서 unseen sequence를 능동적으로 기억하고 처리하기 위해 memory state를 수정 가능한 구조로 확장한 SSM 기반 모델이다.  
기존 모델들이 training-time memory에만 의존하는 한계를 극복하고자, Titans는 내부 hidden state를 test-time에 gradient descent 방식으로 업데이트하는 **memory editing** 기법을 도입했다.  
이로 인해 모델은 pretraining 없이도 inference 시점에서 새롭게 memory를 구성할 수 있으며, 기존 Transformer 및 SSM 계열보다 훨씬 유연하고 강력한 generalization을 보여준다.  
Titans는 특히 Induction Head, Copy, SCAN 등의 task에서 test-time memorization 능력을 실증적으로 보여주며, **pretraining → inference로 이어지는 기존 패러다임에 균열을 주는 새로운 구조적 제안**이라 할 수 있다.

---

※ 한계점 및 향후 과제
- memory editing 과정은 gradient update이기 때문에 **추론 시간이 증가**하며,  
- 현재는 특정 synthetic task 중심으로 실험되어 **대규모 real-world task 확장에 대한 검증이 부족**하다.  
- 향후에는 Titans 구조를 **multi-layer memory editing**, **cross-modality memory**, **vision-language task** 등으로 확장할 수 있을 것으로 기대된다.
