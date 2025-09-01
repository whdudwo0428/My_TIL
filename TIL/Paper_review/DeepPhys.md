## DeepPhys: Video-Based Physiological Measurement Using Convolutional Attention Networks

#### 2025-09-01

### Problem Statement

* 기존의 영상 기반 생체 신호 추정(rPPG) 연구들은 얼굴 ROI를 단순히 선택하거나, 광학 흐름(optical flow) 기반 접근을 통해 피부의 미세한 변화로부터 심박수를 추정했음.
* 하지만 이러한 방식은 조명 변화, 얼굴 움직임(motion artifact), 피부 질감(texture) 등의 외부 요인에 크게 취약하다는 문제점이 있었음.
* 따라서 실제 환경에서 안정적이고 정확한 심박수 추정을 위해, **조명과 움직임 변화를 동시에 보정할 수 있는 학습 기반 모델**이 필요했음.

### Solution Approach

* DeepPhys는 이 문제를 해결하기 위해 **Convolutional Attention Network**(**CAN**)을 도입함.
* 기본 아이디어는:

  * **Motion Representation**: Optical flow 대신 프레임 간 차분(difference)으로 동적 정보를 추출.
  * **Appearance Representation**: 원본 프레임에서 정적 피부 정보를 함께 학습.
  * **Attention Mechanism**: Appearance stream을 이용해 motion stream에서 생체 신호와 관련 있는 부분을 강조(attend)하고, 불필요한 부분을 억제.
* 즉, 얼굴 영상에서 심장 박동과 연관된 시공간적 특징만 집중적으로 학습하도록 설계.

### Methodology Details

* **입력 구조**:

  * Appearance stream: 원본 영상 프레임을 입력받아 얼굴 ROI의 정적 정보를 학습.
  * Motion stream: 연속된 프레임의 차분을 입력으로 받아 미세한 피부 색 변화와 움직임 패턴을 학습.
* **네트워크 구조**:

  * 두 스트림은 각각 CNN으로 특징을 추출.
  * Appearance stream의 출력을 **attention mask**로 변환하여 motion stream feature map에 곱해줌.
  * 이 과정을 통해 조명이나 얼굴 전체 움직임은 억제하고, 혈류 변화와 관련된 미세 신호만 강화.
* **학습 목표**:

  * Ground truth PPG 신호와의 회귀(regression)를 통해 CNN을 학습.
  * 최종 출력은 HR(heart rate) 값뿐 아니라 원 신호 waveform 재구성도 가능.
* **데이터셋 & 결과**:

  * RGB 얼굴 영상 + 동기화된 PPG 데이터셋을 이용해 학습.
  * 조명/움직임이 포함된 다양한 환경에서 기존 optical flow 기반 방법보다 우수한 HR 추정 성능을 보임.

### Recap

DeepPhys는 영상 기반 심박수 추정에서 발생하는 조명 변화와 움직임 문제를 해결하기 위해 **Convolutional Attention Network**을 도입한 연구이다.
프레임 간 차분으로 얻은 motion representation과 원본 appearance representation을 결합하고, attention 메커니즘을 통해 생체 신호와 관련된 특징만 강조하여 추정 성능을 향상시켰다. 이 방식은 실제 환경에서도 안정적으로 작동할 수 있는 학습 기반 rPPG 추정 방법의 초기 단계로 평가된다.

---

이 논문은 이후 등장하는 TS-CAN, MTTS-CAN 등 attention 확장 모델들의 기반이 되었음.
다만 초기 CNN 기반 구조라 sequence modeling 능력이 제한적이어서, 긴 temporal dependency를 다루는 데는 한계가 있었다.

---

혹시 이어서 **MTTS-CAN**이나 **BigSmall** 같은 후속 연구 리뷰도 같은 형식으로 정리해드릴까요?
