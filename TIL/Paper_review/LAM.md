## Large Action Models: From Inception to Implementation  
#### 2025-04-30  

### Problem Statement  
- 기존 **Large Language Models** (LLMs)은 자연어 명령을 해석하고 응답하는 데에는 탁월하지만, 실제 환경에서 이를 기반으로 한 **정확한 행동 수행** 능력은 제한적이다.  
- 특히 로봇 제어, GUI 자동화, 시스템 조작 등에서는 언어적 지시를 실제 작업으로 전환하는 과정에서 **지시-행동 간 실행 격차** (executability gap)가 발생한다.  
- 이로 인해, 단순한 텍스트 생성이 아닌 **실행 가능한 행동 시퀀스** 생성 능력이 필수적인 과제로 부각된다.  

### Solution Approach  
- 논문은 이러한 한계를 극복하기 위해 **Large Action Models** (LAMs)라는 새로운 프레임워크를 제시한다.  
- LAM은 언어, 시각, 감각 등 **다중 모달 입력** (멀티센서 관찰 등)을 통합해 **실제 환경에서 수행 가능한 행동 시퀀스**를 생성하는 모델이다.  
- LLM의 표현력과 추론 능력을 유지하면서도, 환경 상의 상태에 따라 **정책** (policy)을 생성해 실제 작업 수행을 가능하게 한다.  

### Methodology Details  
- LAM은 다음과 같은 세 가지 주요 모듈로 구성된다:  
  1. **Observation Encoder**: 이미지, GUI 상태, 센서 입력 등 환경 정보를 임베딩  
  2. **Action Tokenizer**: 연속적 또는 복합적인 행동 공간을 discrete한 토큰 시퀀스로 변환  
  3. **Prompt-conditioned Policy Decoder**: 사용자 지시를 조건으로 주어진 환경 상태에서 적절한 행동 시퀀스를 생성  

- 학습 절차는 두 단계로 구성된다:  
  - **Pretraining**: 대규모 시뮬레이션 또는 로그 데이터를 기반으로, 관찰-행동 시퀀스를 예측하는 방식으로 지도 학습 수행  
  - **Fine-tuning**: 실제 환경에서의 상호작용 기반 강화학습(RL), 모방학습(IL), 또는 RLHF 등을 활용해 실행 가능성 및 정책 정밀도 향상  

- 적용 사례:  
  - **로봇 제어**: 물체 조작, 이동, 도구 사용 등  
  - **웹 자동화**: 브라우저 상의 클릭, 입력, 전환 등  
  - **시스템 작업**: 코드 편집, 소프트웨어 설치, DevOps 작업 등  

- 평가 지표는 다음과 같다:  
  - 작업 성공률 (Task Success Rate)  
  - 미지시 상황 일반화 능력 (Zero-shot Generalization)  
  - 지시 충실도 (Instruction-following Accuracy)  

### Recap  
본 논문은 기존 LLM이 지닌 표현력은 유지하면서, 실제 환경에서 **실행 가능한 행동 시퀀스**를 생성할 수 있도록 확장한 **Large Action Models** (LAMs)를 제안한다. 핵심은 멀티모달 입력을 받아 지시 기반 **정책** (policy)을 생성하고, 이를 통해 다양한 작업을 자동화하는 것이다. Observation Encoder, Action Tokenizer, Policy Decoder의 세 모듈을 통해 구조화된 행동 생성 과정을 구축하고, 사전학습과 RL/IL 기반 파인튜닝을 결합함으로써, 다양한 현실 환경에서 안정적이고 일반화된 행동 수행 능력을 실증하였다.  

### 한계 및 향후 방향  
- 행동 공간의 토크나이징은 복잡한 연속 제어를 다루기에는 제약이 있다.  
- 강화학습 기반 fine-tuning은 환경 상호작용 비용이 크고, sample efficiency가 낮다.  
- 향후에는 **장기 계획 능력 (long-horizon planning)**, **계층적 정책 구조**, **메모리 기반 정책** 통합 등을 통해 복잡한 시나리오에서도 확장 가능성이 기대된다.
