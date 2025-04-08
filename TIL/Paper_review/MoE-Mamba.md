## MoE-Mamba: Efficient Selective State Space Models with Mixture of Experts  
#### 2025-04-09

### Problem Statement
- 기존 **State Space Model (SSM)** 기반 시계열 아키텍처들은 긴 dependency를 효율적으로 처리하지만, 여전히 **모든 입력에 대해 전체 SSM 연산을 수행**하기 때문에 계산 자원이 비효율적으로 소모된다.
- 특히 **Mamba**와 같은 모델은 구조적으로 연산 효율이 뛰어나지만, **토큰 간 중요도가 다르다는 사실**을 활용하지 못한다.
- 다양한 입력 간의 복잡도 차이를 고려하지 않는 점, 즉 **uniform processing의 비효율성**이 문제로 제기된다.

### Solution Approach
- 이러한 비효율을 해결하기 위해, **입력 토큰마다 필요한 연산량을 동적으로 조절**할 수 있는 **MoE (Mixture of Experts)** 구조를 SSM 기반 모델에 결합함.
- **MoE-Mamba**는 각 입력 시퀀스 토큰이 다양한 expert SSM 중 일부만 선택적으로 사용하는 구조로, **계산 효율성과 표현력**을 동시에 추구한다.

### Methodology Details
- **Backbone**: Mamba 구조 기반 SSM 사용
  - 기존 Mamba와 동일하게, hidden state update는 continuous-time SSM 형태로 이루어짐
  - Delta update → state update → output projection으로 이어지는 구조 유지

- **Expert Pool**:
  - 각 expert는 별도의 Mamba block (SSM 구조)을 사용
  - 총 \( E \)개의 expert 중 각 토큰은 상위 \( k \)개 (top-k routing) expert만 활성화됨

- **Router**:
  - 입력 토큰의 feature를 기반으로 softmax-based scoring → top-k expert 선택
  - 선택된 expert만 forward pass에 참여 (sparse activation)
  - routing 과정은 differentiable하게 학습되며, GShard-style routing loss 포함

- **Training Efficiency**:
  - Sparse dispatch를 통해 token 별 연산을 제한
  - Routing + SSM 계산을 하나의 연산 그래프 내에서 묶어 GPU 병렬성 확보

- **Loss Composition**:
  - Classification / Language Modeling loss + Auxiliary Load Balancing Loss
  - Expert 간 token 분배가 균형 있게 유지되도록 유도

- **Experiments**:
  - Long-range sequence classification (Long Range Arena)
  - Language modeling (PG-19, WikiText103 등)
  - Mamba, Mega, S4 등 기존 SSM 및 MoE-BERT 대비 우수한 성능 및 FLOPs 절감

### Recap
MoE-Mamba는 Mamba 기반의 State Space Model 구조에 Mixture of Experts를 결합하여 입력 토큰마다 연산 경로를 동적으로 선택하는 구조를 제안한다. 이를 통해 연산 효율을 획기적으로 높이는 동시에 long-range dependency 처리 성능을 유지한다. 핵심은 **Mamba의 연속 상태 업데이트 구조를 유지하면서도, token 별로 일부 expert만 선택적으로 사용하는 sparse routing 구조**에 있다. 실험 결과, 다양한 시계열 및 텍스트 데이터셋에서 기존 모델 대비 성능 및 효율성 면에서 우수한 결과를 보인다.

---

추가로 한계점 및 개선 가능성은 다음과 같다:
- Routing instability로 인한 expert saturation 문제 발생 가능
- Sparse routing이 GPU에서 완전한 이점 제공하지 못하는 상황 존재
- Fine-tuning 시에는 routing freeze 여부에 따라 성능이 달라질 수 있음
