## Transformers are SSMs: Generalized Models and Efficient Algorithms Through Structured State Space Duality  
#### 2025-04-09  

### Problem Statement  
- Transformer는 뛰어난 성능에도 불구하고, 긴 시퀀스 처리 시 **quadratic complexity** 문제와 **local context bias**, **global structure 표현 부족** 등의 한계를 가진다.  
- 반면, Structured State Space Models (SSMs)은 긴 시계열(long-range sequence)에서 **선형 복잡도**로 강한 성능을 보이나, Transformer 수준의 범용성과 유연성을 갖추지 못했다.  
- 이 논문은 Transformer와 SSM 간의 구조적 연결고리를 정립하고, 이를 기반으로 **Transformer를 SSM 관점에서 재해석하거나 일반화**할 수 있는 모델 프레임워크를 제안한다.  

### Solution Approach  
- Transformer의 Attention을 포함한 다양한 구조들을 Structured State Space Model의 관점에서 해석하고 일반화할 수 있는 **Structured State Space Duality** 개념을 도입  
- 이 duality를 통해 **Transformer 구조의 핵심을 유지하면서도 SSM의 효율성과 범용성까지 흡수**한 새로운 모델 설계 가능성을 열어준다.  
- 특히, SSM의 **diagonalization, convolutions, linear recurrences** 등의 연산을 기반으로, Transformer와 SSM 사이를 잇는 이론적 프레임워크를 구축하고 **SSM 형태의 Attention 대체 메커니즘**까지 제안  

### Methodology Details  
- **State Space Model 공식**  
  전통적인 SSM은 다음과 같은 1차 선형 시스템을 기반으로 함:  
  - Hidden state 업데이트: `h(t+1) = A h(t) + B x(t)`  
  - 출력 계산: `y(t) = C h(t) + D x(t)`  
  - 이때 A, B, C, D는 학습 가능한 파라미터이며, 이 시스템은 convolution kernel `K(t)` 형태로 변환 가능  

- **Structured State Space Duality**  
  - Attention 구조를 SSM 관점에서 해석하면, 그것 역시 특정 커널을 기반으로 한 convolution 구조로 볼 수 있음  
  - Transformer의 Attention은 다음과 같이 재구성 가능:
    - Query-Key-Value Attention은 실제로 특정 kernel weight `K(t)`와 입력 `x(t)`의 convolution으로 간주할 수 있음
    - 이는 곧 **SSM이 time-invariant linear system으로 Attention을 근사하거나 대체할 수 있다는 이론적 근거**가 된다  

- **SSM의 커널로 Transformer 구조 근사하기**  
  - 논문에서는 고정된 diagonal 구조의 SSM을 이용해 Efficient Attention을 Approximation 할 수 있음을 보임  
  - 이 커널은 convolution operator `K * x` 형태로 표현되며, FFT 기반의 연산 또는 low-rank structured matrix로 효율적으로 계산 가능  
  - Transformer와 동일한 expressive power를 유지하면서도 sub-quadratic 또는 linear time complexity를 달성 가능  

- **Generalization and Unification**  
  - Transformer의 다양한 구조들(Linformer, Performer, Synthesizer, MLP-Mixer 등)이 이 Dual SSM View 하에 모두 하나의 구조적 틀로 수렴됨  
  - 이는 모델 설계 관점에서 Transformer와 SSM을 통합적으로 이해하고, 새로운 구조 설계 시 강력한 지침이 될 수 있음  

### Recap  
이 논문은 Transformer와 Structured State Space Model(SSM) 사이의 수학적 구조 유사성에 주목하여, Transformer의 Attention 메커니즘을 SSM의 convolution 커널 기반 표현으로 재해석하는 **Structured State Space Duality** 개념을 제안한다. 이를 통해 SSM의 효율성과 Transformer의 범용성을 통합한 새로운 모델 설계를 가능하게 하며, 다양한 기존 구조들 또한 하나의 SSM 프레임워크로 일반화할 수 있음을 보인다. Attention의 convolution 표현, kernel-based 연산, diagonal state transition 등은 모두 이 이론의 핵심이며, 효율성과 성능을 모두 갖춘 모델을 설계하는 데 있어 강력한 기반을 제공한다.  

- 본 논문은 Mamba, S4, H3 등의 후속 구조와 논리적으로 연결되며, 특히 **linear recurrence + gating** 구조의 설계에 이론적 토대를 제공  
- 한계로는, 실제 모델링에서 non-linear transformation의 필요성, multi-head 표현의 약화 가능성 등이 있으며, 추후 구현 효율성(예: GPU 상 scan 최적화) 문제도 함께 논의될 필요가 있다.

- 참고하기 좋은 [Blog Review](https://velog.io/@euisuk-chung/Paper-Review-Transformers-are-SSMs-Generalized-Models-and-Efficient-Algorithms-Through-Structured-State-Space-Duality)
