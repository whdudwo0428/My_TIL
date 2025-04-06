## Neural Machine Translation by Jointly Learning to Align and Translate  
#### 2025-04-04

### Problem Statement
- 기존 sequence-to-sequence 모델은 인코더가 입력 시퀀스를 하나의 고정된 벡터로 요약하고, 디코더가 이를 기반으로 출력을 생성한다.
- 이 구조는 입력 시퀀스가 길어질수록 정보 손실이 심해지고, 중요한 부분에 집중하기 어렵다는 한계를 가진다.
- 또한 번역 과정에서 입력의 어떤 부분을 참고하는지에 대한 정렬 정보가 제공되지 않아, 해석 가능성과 정확도 측면에서 부족하다.

### Solution Approach
- 이 논문은 디코더가 출력 단어를 생성할 때마다 인코더의 전체 hidden state를 참조하여, **입력의 중요한 부분에 동적으로 집중**하는 **soft attention 메커니즘**을 제안한다.
- 이 구조는 고정된 context vector 대신, **출력 시점마다 입력 전체에서 가변적인 context vector를 구성**하도록 하여 긴 시퀀스에서도 안정적인 정보 전달을 가능하게 한다.
- 이와 동시에, 디코더가 입력과의 **정렬 정보(alignment)**를 학습하게 되어 번역의 해석 가능성도 높아진다.

### Methodology Details

#### 1. 인코더-디코더 구조
- 인코더는 양방향 RNN으로 구성되어 입력 시퀀스의 각 위치에서 문맥 정보를 포함한 hidden state를 생성한다.
- 디코더는 RNN 기반이며, 각 타임스텝에서 이전 hidden state와 가변적인 context를 기반으로 다음 단어를 생성한다.

#### 2. Soft Attention 메커니즘
- 디코더는 매 시점마다 인코더의 각 hidden state에 대해 점수를 계산하고, 이를 정규화하여 가중치로 변환한다.
- 이 가중치는 입력 시퀀스의 각 위치가 현재 출력에 얼마나 중요한지를 나타내며, 전체 hidden state를 가중합하여 context를 구성한다.
- 이렇게 생성된 context는 디코더의 입력에 반영되어, 현재 시점에 필요한 정보를 동적으로 조합할 수 있도록 한다.

#### 3. 학습 방식과 정렬 해석
- 전체 구조는 end-to-end 방식으로 학습되며, 별도의 정렬 레이블 없이도 attention 가중치가 정렬 역할을 학습한다.
- 이 attention 가중치는 시각화가 가능해, 번역 과정에서 모델이 어느 입력 단어에 집중했는지를 확인할 수 있다.

### Recap
Bahdanau Attention 논문은 고정된 context vector 방식의 한계를 극복하기 위해, **출력 시점마다 입력 전체를 동적으로 참조하여 가변적인 context를 구성하는 soft attention 메커니즘**을 제안한다. 이를 통해 긴 문장을 다루는 번역에서도 정보 손실 없이 출력이 가능하며, alignment 정보가 내재적으로 학습되어 해석 가능성도 확보된다. 이 모델은 이후 attention 기반 모델의 시초가 되었고, Transformer의 기반을 마련하는 중요한 전환점이 되었다.

---

**한계점 및 후속 발전 방향**  
- 모든 출력 시점마다 입력 전체를 참조해야 하므로 연산량이 증가하며, 실시간 처리에는 비효율적일 수 있다.  
- 이후 Luong Attention에서는 계산 효율성을 높이기 위해 score 함수를 단순화하였고, Transformer에서는 self-attention으로 구조를 전면 재설계하여 병렬성과 확장성을 극대화하였다.
