## OverFeat: Integrated Recognition, Localization and Detection using Convolutional Networks  
#### 2025-01-23 / [https://arxiv.org/abs/1312.6229](https://arxiv.org/abs/1312.6229)

### Problem Statement
- 기존의 딥러닝 기반 이미지 분류 모델은 **정확한 위치 정보 없이 전체 이미지에 대한 예측만 수행**함.  
- 따라서 단일 이미지 내 다수의 객체를 탐지하거나 위치까지 정확히 추정하는 **localization** 및 **detection**에는 적합하지 않음.
- 객체 탐지를 위한 기존 접근은 Sliding Window + Classification의 방식이었으나, 연산 비용이 크고 CNN과 통합되지 않았음.

### Solution Approach
- OverFeat는 **하나의 CNN 모델로 이미지 분류(Classification), 위치 추정(Localization), 객체 탐지(Detection)**를 통합적으로 수행하는 구조를 제안함.
- 이를 위해 **fully convolutional 방식의 sliding window**를 도입하여 이미지 전체를 효율적으로 스캔하고, 각 위치에서의 예측을 동시에 수행함.

### Methodology Details
- **기반 모델**: ImageNet Large Scale Visual Recognition Challenge(ILSVRC)에서 성공한 **Deep CNN (Zeiler & Fergus 2013)** 구조 기반.
  
- **Classification**:
  - 표준 CNN 구조를 사용하여 이미지 전체에 대해 분류 작업을 수행.
  - 네트워크는 Supervised Pretraining + Fine-tuning을 통해 학습됨.

- **Localization**:
  - 이미지 내 주요 객체의 중심과 바운딩 박스를 예측하도록 회귀(regression) 출력 채널을 추가함.
  - softmax 대신 회귀 로스를 사용해 바운딩 박스 좌표(center x, y, width, height)를 직접 예측함.

- **Detection**:
  - 이미지의 여러 위치에서 CNN을 **stride를 두고 sliding**하며 실행하여 모든 위치에 대한 detection score를 생성.
  - 여러 스케일로 이미지 피라미드를 만들어 다양한 객체 크기를 처리.
  - 마지막 단계에서 **Non-Maximum Suppression (NMS)**을 적용해 중복 제거 및 최종 detection 결과 생성.

#### 주요 기술 요소
- **Fully Convolutional Sliding Window**: 고정 크기의 crop을 CNN에 반복적으로 넣는 대신, convolutional feature map 상에서 sliding window를 적용하여 **모든 위치를 한 번에 처리**할 수 있음.
- **Joint Architecture**: Classification, Localization, Detection을 단일 네트워크로 통합 수행.
- **Multi-scale Processing**: 다양한 크기의 이미지를 입력하여 다양한 객체 크기에 대응.

### Recap
OverFeat는 CNN의 구조를 확장하여 이미지 분류뿐만 아니라 위치 예측(Localization)과 객체 탐지(Detection)을 하나의 네트워크로 통합한 모델이다. 기존 슬라이딩 윈도우 방식의 비효율을 해결하기 위해 convolutional feature map 위에서 위치마다 예측을 수행하는 **fully convolutional sliding window** 구조를 제안하였다. 또한 바운딩 박스를 직접 회귀하는 localization 레이어를 추가함으로써 detection 정확도를 높였다. 이후 Fast R-CNN 및 YOLO와 같은 실시간 객체 탐지 모델의 중요한 전신이 되었으며, classification-network 기반 detection의 초기 구현으로 평가받는다.

---

**한계점 및 후속 발전 방향**
- OverFeat는 sliding window 방식이지만 여전히 **모든 위치/스케일에 대해 CNN을 반복적으로 수행**하므로 속도에 제한이 있음.
- 단일 네트워크로 모든 task를 처리하지만, 각각의 task에 특화된 최적화는 부족함.
- 이후 YOLO에서는 detection을 완전히 regression 문제로 단순화하고, Faster R-CNN에서는 proposal을 CNN에 통합하여 효율성을 극대화함.

**PS**
- 기존에 조금씩 햇갈리던 기본 CNN 동작 원리를 기존보다 깊게 탐구 (Padding, Strid, Pooling, 각 Layer 내 원리)
- Git에 지금까지의 TIL작성하며 어떤 내용을 공부했나 다시 정리하고 읽어봄
- OverFeat의 개념을 바탕으로 Two stage detector -> One stage detector 핵심 차이를 더 공부해봄
