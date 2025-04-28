## MCP-Solver: Integrating Language Models with Constraint Programming Systems
#### 2025-04-28

### Problem Statement
- 기존 Constraint Programming (CP) 시스템은 강력한 문제 해결 능력을 가지지만, 문제를 기술하는 과정에서 사람이 명시적으로 제약 조건을 설정해야 한다는 점이 한계로 작용했다.
- 반면 Language Models (LMs)는 자연어로 주어진 설명을 이해할 수 있지만, 복잡한 제약 문제를 풀거나 해를 완전히 보장하는 능력은 부족했다.
- 따라서 자연어로 설명된 복잡한 제약 문제를 효율적이고 정확하게 해결하기 위해, CP의 강점과 LM의 자연어 이해 능력을 통합하는 방법이 필요했다.

### Solution Approach
- 자연어 문제 설명을 **LM**이 파싱하고, 구체적인 제약 조건을 **CP**로 변환하는 **MCP-Solver**를 제안하여 이 문제를 해결한다.
- 즉, **LM**은 문제의 의미를 이해하고 형식적 제약 모델을 생성하는 역할을 하고, 생성된 제약 모델은 **CP Solver**가 최적화 및 탐색을 수행하도록 한다.
- 이로써 자연어-제약 프로그래밍 간의 간극을 줄이고, 양자의 강점을 결합하는 시스템을 구축한다.

### Methodology Details
- **System Architecture**
  - 입력: 자연어로 서술된 제약 문제.
  - 과정:
    - (1) **LM-based Parser**가 입력 문장을 분석하여 제약 변수, 도메인, 제한조건(constraints) 등 CP 모델 요소를 추출한다.
    - (2) 추출된 정보를 바탕으로 공식적인 CP 모델(예: MiniZinc, OR-Tools 형식)로 변환한다.
    - (3) **CP Solver**가 생성된 모델을 풀어 해답을 산출한다.
  - 출력: 문제 조건을 만족하는 해답 혹은 최적 해.

- **Training and Prompt Engineering**
  - 다양한 제약 문제(예: 스케줄링, 할당 문제, 수학 퍼즐)를 자연어-제약모델 쌍으로 수집하여 학습 및 튜닝.
  - 체계적인 프롬프트 설계(prompt templates)와, 문제 요소를 명시적으로 추출하도록 LM을 지도하는 방식 사용.

- **Constraint Programming Backend**
  - MiniZinc, Google OR-Tools 같은 CP 솔버들과 인터페이스하여 실제 최적화 수행.
  - 필요에 따라 Hard Constraints (반드시 만족)와 Soft Constraints (가능한 만족) 구분 처리.

- **Evaluation**
  - 다양한 실제 문제에 대해
    - 문제 해석 정확도 (Parsing Accuracy)
    - 제약 생성 정확도 (Constraint Generation Accuracy)
    - 최적 해 발견률 (Optimal Solution Finding Rate)
    - 문제 해결 시간 (Solving Time)
  를 측정하여 평가.

### Recap
MCP-Solver는 자연어로 주어진 복잡한 제약 문제를 해결하기 위해 Language Model과 Constraint Programming 시스템을 통합하는 접근이다. LM은 자연어 문제를 이해하여 구조화된 제약 모델로 변환하고, CP Solver는 이를 최적화하여 해를 찾는다. 이 시스템은 자연어 인터페이스의 편리성과 CP의 해 보장 능력을 결합함으로써, 기존 CP 접근의 진입 장벽을 낮추고 보다 다양한 사용자가 복잡한 제약 문제를 해결할 수 있게 한다.

---

### 한계 및 개선 가능성
- 자연어 파싱 과정에서 미묘한 의미 차이나 불완전한 표현을 정확히 모델링하는 데 한계가 존재한다.
- 복잡도가 높은 문제에서는 LM이 제약을 누락하거나 부정확하게 해석할 수 있으며, 이는 CP Solver 단계에서 해를 찾지 못하는 결과로 이어질 수 있다.
- 향후에는 대화형 인터페이스를 추가하여 LM이 불확실할 때 사용자로부터 명확한 정보를 요청하는 방식(interactive refinement)을 통해 정확성을 높이는 방향이 제안될 수 있다.
