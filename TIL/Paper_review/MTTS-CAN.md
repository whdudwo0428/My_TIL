## MTTS-CAN: Multi-Task Temporal Shift Attention Networks for On-Device Contactless Vitals Measurement

#### 2025-09-01

### Problem Statement

* DeepPhys 및 후속 연구(CAN, TS-CAN)는 영상 기반 생체 신호 추정(rPPG)에서 **motion artifact**와 **illumination 변화** 문제를 완화했지만, 여전히 두 가지 한계가 존재했음:

  1. **단일 과업(single-task)** 중심이라 HR 추정만 가능하고, 호흡률(respiration rate) 같은 다중 생체 지표 동시 추정이 어려움.
  2. **계산량이 크고 GPU 의존적**이라 모바일/엣지 기기(on-device) 환경에서 실시간 처리가 제한적임.
* 따라서 **멀티태스크 학습**과 **경량화된 시공간적 모델링**을 동시에 달성하는 새로운 구조가 필요했음.

### Solution Approach

* MTTS-CAN은 이 문제를 해결하기 위해 **Multi-Task Temporal Shift Attention Network**를 제안함.
* 핵심 아이디어:

  * \*\*Temporal Shift Module (TSM)\*\*을 적용하여 RNN/LSTM 없이도 효율적인 시계열 특징 학습을 가능하게 함.
  * **Multi-task head**를 두어 HR, RR 같은 서로 다른 생체 지표를 동시에 예측.
  * **Attention mechanism**을 통해 motion stream에서 생체 신호와 관련된 영역만 강조.
* 즉, 기존 CAN/TS-CAN의 강점을 유지하면서도 멀티태스크 + 저비용(on-device friendly) 학습을 실현.

### Methodology Details

* **입력 구조**:

  * Appearance stream: 원본 얼굴 프레임 → 정적 피부 및 ROI 정보 학습.
  * Motion stream: 프레임 간 차분 → 미세한 피부 색 변화 및 움직임 학습.
* **네트워크 구조**:

  * CNN backbone + **Temporal Shift Module (TSM)**

    * 1D temporal convolution 대신 feature map을 시간축으로 shift시켜 temporal dependency를 학습.
    * 파라미터와 연산량 증가 없이 sequence modeling 가능.
  * Attention block: Appearance stream을 기반으로 motion feature에 attention 적용.
  * Multi-task head: HR, RR, SpO₂ 등 다양한 physiological signals 동시 회귀(regression).
* **학습 전략**:

  * Loss function은 multi-task regression loss로 설계.
  * HR, RR 각각의 ground truth 신호와 네트워크 출력을 비교하여 공동 최적화.
* **결과**:

  * HR과 RR을 동시에 추정하면서도 기존 단일 과업 모델보다 성능이 떨어지지 않음.
  * Mobile GPU/CPU 환경에서도 실시간 처리 가능할 정도로 경량화됨.

### Recap

MTTS-CAN은 DeepPhys 계열 모델의 한계를 확장하여, **멀티태스크 학습**과 **효율적인 temporal modeling**을 결합한 모델이다.
Temporal Shift Module을 통해 연산량 증가 없이 긴 temporal dependency를 학습할 수 있고, attention 기반 두 스트림 구조를 유지하면서 HR과 RR 같은 복수의 생체 신호를 동시 추정한다.
이는 모바일·엣지 디바이스에서 실시간 contactless physiological measurement를 가능하게 한 중요한 진전으로 평가된다.

---

MTTS-CAN의 의의는 “딥러닝 기반 rPPG 모델이 연구실 단계를 넘어 실제 기기(on-device) 적용 가능성을 열었다”는 점이다.
다만 Transformer 계열 등장 이전 연구라, 매우 긴 sequence 처리 능력이나 더 정교한 temporal modeling에는 한계가 있다.
