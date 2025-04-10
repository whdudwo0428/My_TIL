## PhysMamba: Efficient Remote Physiological Measurement with SlowFast Temporal Difference Mamba  
#### 2025-03-28 ~ 03-31

### Problem Statement
- Remote Photoplethysmography (rPPG)는 비접촉 방식으로 심박수를 추정하는 기술로, 헬스케어·감정 분석·사용자 인식 등에 널리 활용될 수 있다.
- 하지만 rPPG는 **모션 아티팩트, 조명 변화, 낮은 신호 대 잡음비**, **SNR**에 매우 취약하며, 이는 정확한 생리 신호 추정의 큰 장애물이 된다.
- 기존의 딥러닝 기반 접근은 고정된 시간 해상도에서만 학습이 이루어져 **느린 생리 신호와 빠른 노이즈를 구분하지 못하거나**, **연산 효율이 떨어지는 문제**가 있다.
- 따라서 **다양한 시간 스케일의 정보를 분리하고 통합적으로 활용하면서**, **추론 효율성과 정확도를 모두 보장할 수 있는 시계열 모델**이 필요하다.

### Solution Approach
- PhysMamba는 Mamba 계열의 state space model을 기반으로 하되, **SlowFast Temporal Difference 설계를 적용한 rPPG 특화 구조**를 제안한다.
- 생리 신호가 **느리고 미세한 진동 주기**를 가지며, 반대로 대부분의 모션 노이즈는 **고속이고 급변적인 특징**을 갖는다는 점에 착안했다.
- 이를 위해 입력 시퀀스를 **Slow branch와 Fast branch로 분리하여 병렬 처리하고**, **두 출력을 비교(difference)**하여 생리 신호의 핵심만 추출한다.

### Methodology Details

#### 1. SlowFast Mamba Branch
- 입력 얼굴 시퀀스를 두 개의 temporal path로 분리 처리:
  - **Slow-Mamba**: 긴 시간 간격(큰 Δ)을 가진 recurrence로 global하고 안정적인 추세를 학습
  - **Fast-Mamba**: 짧은 Δ로 빠르게 변화하는 signal 변화에 민감하게 반응

- 두 branch 모두 Mamba 구조로 구성되어, **linear-time 병렬 연산과 recurrence 표현력을 동시에 유지**

#### 2. Temporal Difference Mechanism
- 두 branch의 출력을 시간 차원에서 **element-wise로 뺀 결과**를 활용
- 이 차이값은 motion artifact, noise 등 빠른 요소를 억제하고, 생리적 주기성을 부각시키는 역할
- 결과적으로 rPPG 추정 성능이 개선됨

#### 3. Lightweight & Efficient Design
- 모든 연산은 Mamba 구조 특유의 **scan 연산 기반 recurrence**로 처리되어, GPU에서도 매우 빠름
- 전체 모델은 attention 없이 작동하며, 파라미터 수와 FLOPs가 Transformer 기반 모델 대비 훨씬 적음
- 실제 inference latency 측정 결과도 타 모델 대비 가장 우수

#### 4. Application: Remote PPG Estimation
- 최종 출력은 rPPG curve (1D physiological signal) 형태로 복원
- Frequency analysis나 peak-to-peak 간격 등을 통해 **심박수(HR)**를 정밀하게 추정
- 다양한 영상 조건(조도, 움직임, 압축 등)에서 robust하게 동작

#### 5. Evaluation
- 주요 벤치마크(VIPL-HR, MMSE-HR)에서 **HR MAE(metric) 기준 기존 최고 모델 대비 성능 향상**
- 특히 움직임이 많거나 어두운 조건에서도 예측 정확도 우수
- 속도-정확도 균형을 가장 잘 맞춘 최신 모델로 평가됨

### Recap
PhysMamba는 rPPG의 핵심 문제인 **생리 신호의 미세한 주기성과 환경 노이즈의 시간적 차이**에 주목하여, 이를 분리해 처리할 수 있는 **SlowFast Temporal Difference 구조**를 도입한 고효율 생리 신호 추정 모델이다. Mamba의 recurrence 기반 구조를 slow/fast branch로 확장하고, 차이값을 통해 noise를 억제하며 핵심 신호를 추출한다. 이로써 높은 정확도, 빠른 연산, 강인한 추정력을 모두 달성하며, 실제 의료 및 HCI 환경에서의 활용 가능성을 크게 확장했다.

---

**한계점 및 후속 발전 방향**  
- Slow-Fast branch의 Δ 설정이 고정되어 있어 **adaptive temporal scaling** 연구 여지가 있음  
- 얼굴 영역 추출, 얼굴 ROI tracking 등에 따라 성능이 민감할 수 있음  
- 이후 PhysMamba2에서는 multi-scale Mamba 또는 learnable Δ를 도입하는 방향으로 확장 가능함
