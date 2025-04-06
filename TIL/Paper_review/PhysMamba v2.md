## PhysMamba: Synergistic State Space Duality Model for Remote Physiological Measurement  
#### 2025-04-01 ~ 04-03 / [https://arxiv.org/pdf/2408.01077](https://arxiv.org/pdf/2408.01077)

### Problem Statement
- Remote Photoplethysmography (rPPG)는 카메라 기반으로 심박수 등의 생리 신호를 비접촉 방식으로 추정하는 기술로, 헬스케어, 감정 인식, 사용자 인증 등 다양한 분야에서 중요성이 커지고 있다.
- 그러나 실제 환경에서는 조명 변화, 얼굴 움직임, 압축 artifacts 등으로 인해 **rPPG 신호의 신호 대 잡음비(SNR)가 매우 낮아지고**, 정확한 심박수 추정이 어려워진다.
- 기존 딥러닝 기반 rPPG 모델들은 Attention 기반 또는 CNN 기반 구조를 채택했지만, **시간적 의존성과 주기성 정보를 완전하게 포착하지 못하거나**, **연산량과 latency가 높아 real-time 활용이 어렵다**.
- 따라서 rPPG 추정에 최적화된 **효율적이고 정밀한 시간 구조 표현이 가능한 시계열 모델**이 요구된다.

### Solution Approach
- PhysMamba는 Mamba 계열의 selective state space model을 기반으로 하되, **State Space Duality** 개념을 도입해 **시간 영역과 주파수 영역 표현을 통합적으로 학습하는 구조**를 제안한다.
- 핵심은 **Self-Attention 기반 Branch**와 **State Space 기반 Branch**를 병렬적으로 구성하고, 그 둘 사이의 정보를 **Cross-Attention 방식으로 동기화**하는 이중 구조를 채택하는 것이다.
- 이를 통해 **짧은 구간의 local dynamic과 긴 시간에 걸친 periodic trend**를 동시에 포착할 수 있으며, noise와 motion artifacts에 강건한 rPPG 추정이 가능하다.

### Methodology Details

#### 1. Dual-Branch 구조
- 입력 영상 시퀀스는 두 개의 병렬 경로로 처리된다:
  - **Attention Branch**: Transformer 스타일의 self-attention을 통해 short-term, token-level dependency를 학습
  - **State Space Branch**: Mamba 기반 selective SSM을 통해 long-range, frequency-aware dynamics를 포착

#### 2. Synergistic State Space Duality (SSSD)
- Attention과 State Space 간 **Cross-Attention 연산**을 수행하여 두 representation이 상호 강화되도록 설계
- 이 구조는 고주파 모션 노이즈와 저주파 생리 주기 신호를 구분하고 통합하는 데 최적화됨
- 전체 흐름은 end-to-end 학습 가능하며, lightweight하면서도 표현력이 높은 구조를 형성

#### 3. Efficient Implementation
- Self-Attention Branch는 token 수를 줄여 연산량을 줄이고, Mamba Branch는 scan 기반으로 병렬 연산을 수행
- 전체 네트워크는 rPPG task에 맞춰 parameter 효율성과 속도-정확도 trade-off를 최적화함

#### 4. Downstream Task: Heart Rate Estimation
- 출력은 time-domain rPPG signal이며, 이 신호에서 peak-to-peak 간격 또는 frequency domain 분석을 통해 heart rate를 추정
- 실험은 공개 데이터셋인 VIPL-HR, MMSE-HR, UBFC 등에서 수행

#### 5. 성능
- 기존 SOTA 대비:
  - **낮은 HR MAE (Mean Absolute Error)**  
  - **조명, 압축, 모션 등 어려운 조건에서 뛰어난 추정 안정성**
  - **연산량 감소, inference time 단축**
- 특히 Cross-Attention을 통해 dual-path representation이 상호 보완적으로 작동함을 ablation으로 증명

### Recap
PhysMamba는 생리 신호 추정에 특화된 dual-state 모델로, attention 기반 표현과 state space 기반 표현을 동시에 활용하는 **Synergistic State Space Duality 구조**를 제안한다. Mamba의 효율성과 Transformer의 표현력을 병렬로 구성하고, cross-attention으로 상호 보완함으로써, 고주파 노이즈에 강하고 저주파 주기 신호에 민감한 rPPG 추정이 가능하다. 이 모델은 정확도와 효율성을 동시에 달성하며, 비접촉 심박수 추정의 실용적 한계를 뛰어넘는 새로운 프레임워크로 자리매김한다.

---

**한계점 및 후속 발전 방향**  
- 두 branch 간 cross-attention의 추가로 구조적 복잡도가 다소 증가하며, 일부 환경에서는 latency 개선 여지가 있음  
- 향후 adaptive attention pruning, dynamic state routing 등으로 더 경량화 가능  
- 다중 인물 또는 복합 환경 적용을 위한 확장형 PhysMamba 연구로 이어질 수 있음
- PhysMamba v1 보다 해당 모델의 아키텍쳐가 내가 원하는 Titans과의 구조적 유사성이 겹쳐보였음.
