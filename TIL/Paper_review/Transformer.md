## Attention Is All You Need  
#### 2025-04-04

### Problem Statement
- 기존 sequence-to-sequence 모델들은 주로 RNN 또는 CNN 기반으로 구성되며, 긴 시퀀스를 처리하는 데 있어 **병렬화가 어렵고 long-range dependency를 학습하기 힘든 한계**가 있었다.
- 특히 번역과 같은 자연어 처리 과제에서는 입력과 출력 사이의 복잡한 관계를 모델링할 수 있어야 하는데, RNN 계열 구조는 **시간 순차적 계산 흐름** 때문에 학습 속도와 표현력에 제약이 있었다.
- 따라서 이러한 문제를 해결하기 위해, **순차적 구조 없이 전적으로 attention만으로 구성된 새로운 시퀀스 모델**이 필요했다.

### Solution Approach
- 본 논문은 attention 메커니즘만으로 구성된 최초의 구조인 **Transformer**를 제안한다.
- 핵심 아이디어는 **Self-Attention 기반의 encoder-decoder 구조**로, 각 토큰이 시퀀스 내 모든 다른 토큰을 동시에 참조할 수 있도록 하여, **병렬화 가능성과 표현력을 동시에 확보**한다.
- 또한 positional encoding을 도입하여 순서 정보를 보완함으로써, RNN 없이도 순차적 특성을 반영할 수 있도록 한다.

### Methodology Details

#### 1. 전체 구조
- Transformer는 **encoder와 decoder가 각각 N개의 identical layer로 구성**된 구조
  - 각 encoder layer는 self-attention과 feed-forward network로 구성
  - 각 decoder layer는 masked self-attention, encoder-decoder attention, feed-forward network로 구성

#### 2. Self-Attention
- 입력 시퀀스 내 각 토큰은 자신을 포함한 모든 다른 토큰을 대상으로 attention score를 계산해 weighted sum으로 표현
- 이를 통해 각 토큰은 문맥 정보를 유연하게 조합하며, **순차적인 정보 흐름 없이도 global dependency를 학습**할 수 있다

#### 3. Multi-Head Attention
- 단일 attention head는 표현력에 제한이 있으므로, 여러 개의 head를 두어 서로 다른 subspace에서 attention을 학습하도록 구성
- 각 head는 독립적으로 attention 연산을 수행한 뒤, 이를 concat하여 최종 표현을 생성

#### 4. Positional Encoding
- self-attention은 위치 정보를 사용하지 않기 때문에, 입력 순서를 반영하기 위해 **사인/코사인 함수를 기반으로 한 positional encoding**을 각 입력 임베딩에 추가
- 이로 인해 모델은 각 토큰의 상대적/절대적 위치를 구분할 수 있게 된다

#### 5. Feed-Forward Network & Residual Connection
- 각 layer는 self-attention과 함께 position-wise feed-forward network를 포함하고, **layer normalization과 residual connection**을 적용해 학습 안정성을 높인다

#### 6. 학습 세팅
- 모델은 WMT 2014 영어-독일어 및 영어-프랑스어 번역 작업에서 평가되었고, 기존 RNN 기반 모델들을 뛰어넘는 BLEU 성능을 기록
- 특히 학습 시간과 연산 속도에서 큰 개선을 보였으며, 병렬화 효율성이 매우 뛰어났다

### Recap
Transformer는 RNN이나 CNN 없이, **전적으로 attention 메커니즘만으로 시퀀스를 처리하는 최초의 모델**이다. Self-Attention을 통해 global context를 직접 반영할 수 있고, Multi-Head Attention으로 표현력을 강화하며, positional encoding을 통해 순서 정보까지 반영할 수 있도록 설계되었다. 이 구조는 병렬화가 가능하고 확장성이 뛰어나며, 이후 대부분의 NLP 및 Vision 모델 구조에 깊은 영향을 미친 핵심 패러다임 전환점이다.

---

**한계점 및 후속 발전 방향**  
- attention 연산은 시퀀스 길이에 따라 **quadratic한 메모리 및 연산 비용**을 요구하기 때문에, 긴 시퀀스에서는 비효율적일 수 있음  
- 이후 등장한 Longformer, Linformer, Performer, S4, Mamba 등은 이러한 연산 병목을 해결하기 위해 attention 구조를 경량화하거나 SSM으로 대체하는 방향으로 발전함
