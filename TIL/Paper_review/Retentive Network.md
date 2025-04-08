## Retentive Network (A Successor to Transformer for Large Language Models)  
#### 2025-04-08

### Problem Statement
- Transformer 기반 LLM의 **context length 확장성 문제**는 매우 높은 계산비용을 유발하며, 특히 self-attention의 **O(n²)** 연산복잡도는 긴 시퀀스를 처리하는 데 비효율적임.
- FlashAttention과 같은 최적화도 GPU에서만 작동하며, **단일 토큰 처리(latency)** 측면에서도 한계가 존재함.
- 최근 등장한 Mamba(S6) 모델은 low-rank 구조와 scan 기반 처리로 latency와 context 길이 문제를 해결하지만, **parallelism 부족**, **limited expressiveness**, **initialization 민감성**, **gate saturation** 등의 단점이 있음.
- 따라서 긴 context를 효율적으로 처리하고, **Transformer와의 expressive power 격차 없이** 확장 가능한 구조가 필요함.

### Solution Approach
- Transformer의 attention 구조를 **"parallelizable한 retention mechanism"** 으로 대체하여 context handling을 확장함.
- Attention-free 구조를 유지하면서도 **global receptive field**와 **position sensitivity**를 유지할 수 있도록, gating과 positional encoding 구조를 새롭게 설계.
- Mamba 대비 높은 expressivity를 유지하면서도, Transformer 수준의 scalability와 training robustness를 결합한 구조를 제안함.

### Methodology Details
- Retentive Network는 크게 세 블록으로 구성됨:
  1. **Input Projection**: 입력 token을 low-rank 방식으로 transform하여 key-value-like representation으로 분리.
  2. **Retention Layer**: 기존 attention을 대체하는 핵심 구조로, 아래 방식으로 작동함:
     - hidden state hₜ는 retention memory로부터 다음과 같이 업데이트됨:
       - retention(hₜ) = ∑ Wᵢ * decayᵗ⁻ⁱ * xᵢ (여기서 decay는 learnable or fixed exponential decay weight)
     - 즉, 과거 정보를 time-decayed weighted sum 방식으로 집계하는 방식이며, scan 연산을 통해 **parallel 계산 가능**함.
     - attention처럼 모든 token 간 상호작용은 없지만, decay factor와 gating으로 long-term dependency를 유사하게 반영.
  3. **Gating Mechanism**:
     - GLU-like 구조의 **multiplicative gating**을 retention 앞뒤로 사용하여 정보 흐름을 조절.
     - 특히 gating saturation 문제를 피하기 위해 GELU 중심으로 설계하여 안정적인 gradient 흐름을 유지.
- **Positional Encoding**:
  - Rotary positional encoding(RoPE)과 같은 방식이 아닌, learned or fixed decay + positional bias 방식.
  - 이 방식은 Transformer의 relative position encoding과 유사한 효과를 내며, 특히 long context에서도 **position-invariant** 한 generalization이 가능함.
- **Parallel Scan Implementation**:
  - Retention이 recurrence-like 구조지만 scan 알고리즘을 사용하여 Transformer처럼 GPU에서 병렬처리 가능.
  - 이 구조는 Mamba의 selective scan보다 덜 민감하며, GPU 효율성 면에서도 우수함.
- 학습 안정성 측면에서도, Transformer와 유사한 initialization 및 LayerNorm 구조를 가져, **training difficulty를 줄임.**

### Recap
Retentive Network는 Transformer의 attention 구조를 scan 기반 **parallelizable retention mechanism**으로 대체하여 긴 context를 효율적으로 처리하는 LLM 구조이다. 이 모델은 attention-free임에도 불구하고 **long-range dependency**, **scalability**, **position-awareness**를 유지하며, Mamba보다 더 안정적인 학습과 높은 표현력을 제공한다. 핵심은 decay-based memory aggregation, gated update, scan을 통한 병렬성 확보이며, 실제로 여러 LLM 벤치마크에서 Transformer 및 Mamba를 능가하는 성능을 보여준다.

**한계 또는 개선 여지**:
- RoPE나 ALiBi처럼 완전히 position-invariant한 구조는 아님.
- decay 설정이 학습에 큰 영향을 주므로 초기 설정에 따라 성능 변동 가능성 존재.
- 여전히 attention 기반 구조처럼 full token interaction은 불가능하므로 일부 task에서는 제한적일 수 있음.
