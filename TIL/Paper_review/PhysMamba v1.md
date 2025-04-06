## PhysMamba: Efficient Remote Physiological Measurement with SlowFast Temporal Difference Mamba  
#### 2025-03-28 ~ 03-31 / [https://arxiv.org/abs/2401.13807](https://arxiv.org/pdf/2409.12031)

### Problem Statement
- 비접촉 방식의 생체신호 추정(rPPG, remote photoplethysmography)은 영상 기반으로 심박수 등 생리적 정보를 추정하지만, **신호의 매우 미세한 변화**를 포착해야 하므로 **시간 해상도와 주파수 정밀도가 모두 중요**하다.
- 기존 CNN, Transformer 기반 방법은 이질적인 temporal scale 간 정보를 효과적으로 처리하지 못하고, 특히 **real-time 효율성 및 noise-robustness** 측면에서 한계가 있다.
- 따라서 **느리고 빠른 temporal 변화 모두를 포착할 수 있으면서**, **모션 노이즈에도 강인하고 연산 효율이 높은 시계열 모델**이 필요하다.

### Solution Approach
- PhysMamba는 Mamba 구조를 기반으로 하여, **SlowFast Temporal Difference 설계를 결합한 생체신호 추정 특화 모델**이다.
- 핵심은 rPPG 신호가 갖는 **고유한 slow-fast temporal 구조**를 반영하여 두 가지 분리된 Mamba block을 운영하고, 그 차이(difference)를 활용해 더 안정적이고 정확한 추정을 수행하는 것이다.
- 동시에, 복잡한 attention 없이 **linear-time recurrence 모델의 효율성과 병렬성을 유지**한다.

### Methodology Details

#### 1. Overall Architecture
- 입력은 RGB 영상에서 프레임 단위로 추출된 얼굴 patch sequence
- 이 sequence는 **Slow path**와 **Fast path** 두 개의 흐름으로 분기된다:
  - **Slow-Mamba**: 낮은 temporal resolution, global한 context에 민감
  - **Fast-Mamba**: 높은 temporal resolution, 빠른 미세 변화에 민감

- 두 흐름은 서로 다른 Δ를 사용하는 Mamba block으로 구성됨 (Δ는 state update 간의 step 크기)

#### 2. Temporal Difference Mechanism
- Slow와 Fast 흐름의 출력을 서로 비교하여 **시간 차이 기반의 differential feature**를 계산
- 이 차이는 실제 physiological 신호(예: 심박 리듬)와 noise 간 차이를 증폭시키는 효과를 가짐
- 결국 이 구조는 noise에 robust하고, 미세한 진동에도 민감한 추정이 가능함

#### 3. Lightweight Design
- 기존 attention 기반 모델에 비해 parameter 수가 적고, 복잡도는 linear
- 전체 구조는 scan 기반 연산을 사용하여 GPU에서 매우 빠르게 실행 가능

#### 4. Downstream Task: rPPG 추정
- 모델 출력은 신호 형태로 재구성되어, 후처리를 통해 심박수 추정 또는 PPG curve로 복원됨
- 실험은 일반 rPPG benchmark (VIPL-HR, MMSE-HR 등)에서 진행됨

#### 5. 성능
- PhysMamba는 기존 Transformer, RNN, CNN 계열 rPPG 모델 대비:
  - **추정 정확도(heart rate MAE) 향상**
  - **노이즈 환경 (head motion, lighting variation)에 더 강인**
  - **실시간 처리 효율 우수 (낮은 FLOPs, latency)**

### Recap
PhysMamba는 rPPG와 같은 미세 생체신호 추정을 위해 설계된 Mamba 기반 모델로, **SlowFast 이중 시간 해상도 흐름**을 통해 고주파 및 저주파 신호를 모두 효과적으로 포착한다. 두 흐름의 출력을 비교하여 얻은 differential representation은 노이즈에 강인하고, 심박 신호와 같은 정밀 주기성을 잘 복원할 수 있다. Mamba 특유의 선형 시간 연산 및 병렬성을 그대로 유지하면서도, 기존 모델보다 정확하고 효율적인 추정을 가능하게 한다.

---

**한계점 및 후속 발전 방향**  
- Δ를 고정으로 설정할 경우 모든 상황에서 최적은 아님 → task-adaptive Δ 조절 필요  
- facial ROI tracking이 불안정할 경우 성능 저하 우려 있음  
- 이후 PhysMamba2 또는 Titans 계열로 확장 시, **multi-scale gating** 또는 **adaptive recurrence** 구조가 유망함
