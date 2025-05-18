## Using Fast Weights to Attend to the Recent Past

#### 2025-05-18

### Problem Statement

* RNN (순환 신경망)은 시퀀스의 길이가 길어질수록 과거 정보를 장기적으로 유지하고 조작하는 데 어려움을 겪는다. 이는 **기억 용량의 한계**와 **기울기 소실** 문제 때문.
* Transformer 기반의 Attention 메커니즘은 이 문제를 완화할 수 있지만, 계산량이 커지고 자원이 많이 드는 단점이 있다.
* 따라서 이 논문은 **최근의 과거** 정보에 효율적으로 주의를 기울일 수 있는 **생물학적으로 그럴듯하고 계산 효율적인 메모리 메커니즘**을 제안하고자 한다.

### Solution Approach

* 이러한 문제를 해결하기 위해 논문은 **Fast Weights**라는 빠르게 변하는 가중치 메커니즘을 제안한다.
* 핵심 아이디어는, 최근의 hidden state 정보를 **fast weight matrix**에 저장하고, 이를 통해 현재 시점에서 필요한 과거 정보를 빠르게 참조할 수 있도록 하는 것이다.
* 이는 Transformer의 attention과 유사한 기능을 하되, 계산 비용이 훨씬 적다.

### Methodology Details

* 전체 모델은 \*\*slow RNN (기존 RNN)\*\*과 **fast weights 기반의 연합 기억 메커니즘**으로 구성된다.

* 각 시점 `t`에서 fast weight 행렬 `A_t`는 다음과 같은 **Hebbian 학습 규칙**을 따르며 업데이트된다:

  `A_t = λA_{t-1} + η h_t h_tᵀ`
  여기서,

  * `h_t`는 시점 `t`의 hidden state
  * `λ`는 decay 계수 (이전 메모리를 점차 잊음)
  * `η`는 fast weight의 학습률

* 다음 시점의 hidden state를 계산할 때는 다음과 같이 \*\*내부 반복 계산 (fixed-point iteration)\*\*을 수행하여 fast weight의 영향을 반영한다:

  `h_{t+1} = φ(W x_{t+1} + C h_t + A_t h_t)`
  여기서,

  * `W`: 입력 `x`를 선형 변환
  * `C`: slow recurrent 연결 가중치
  * `φ`: 비선형 함수 (예: ReLU)
  * `A_t h_t`: fast weights 기반의 attention 역할 수행

* 이 구조에서 `A_t h_t`는 **과거 hidden state에 대한 내용 기반 attention 역할**을 수행하지만, Transformer의 attention처럼 pairwise 연산을 수행하지 않기 때문에 계산 효율이 높다.

* 실험은 associative recall, copy task, synthetic language modeling과 같이 **단기 기억**이 중요한 태스크에서 수행되었으며, RNN, LSTM, 심지어 Transformer보다도 더 나은 성능을 보였다.

### Recap

* **Fast Weights**는 RNN에 단기 메모리를 부여하기 위한 메커니즘으로, 최근 hidden state를 fast weight에 저장하고 이를 기반으로 attention 유사 기능을 수행한다.
* Hebbian 방식으로 업데이트되는 fast weight는 Transformer의 attention과 달리 계산 자원이 매우 적게 들며, 생물학적 plausibility도 고려된 구조이다.
* 특히 단기 기억이 요구되는 문제에서 뛰어난 성능을 보이며, 학습 없이도 associative recall이 가능함을 보였다.

**한계점**:

* 긴 시퀀스에 대한 장기 기억은 여전히 제한적이며, Transformer나 외부 메모리 기반 모델이 더 적합하다.
* fast weight의 decay나 learning rate 설정에 민감하여 **수렴 안정성** 확보가 중요하다.
