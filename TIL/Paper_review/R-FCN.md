## R-FCN: Object Detection via Region-based Fully Convolutional Networks  
#### 2025-01-26 / [https://arxiv.org/abs/1605.06409](https://arxiv.org/abs/1605.06409)

### Problem Statement
- Fast R-CNN과 Faster R-CNN은 ROI마다 **fully connected layer**를 적용하여 정확도는 높지만, **ROI 단위로 연산을 반복**하는 구조로 인해 **속도가 느림**.
- Fully convolutional 방식이 segmentation 등에서는 성공했지만, detection에서는 **위치 민감한(localization-sensitive) feature 추출이 어려워** 잘 활용되지 못함.
- 따라서, Region Proposal 기반 객체 탐지기의 **정확도는 유지하면서도**, **완전한 convolutional 구조로 속도를 개선**할 수 있는 방법이 필요함.

### Solution Approach
- R-FCN은 **완전한 convolutional 네트워크 구조**를 유지하면서도, 객체의 위치 정보를 효과적으로 반영할 수 있도록 **position-sensitive score map**을 제안.
- 각 Region Proposal에 대해 위치별로 특화된 score를 pooling하여, **ROI별 예측을 convolution 연산 수준에서 해결**함.
- 이를 통해 **Faster R-CNN 수준의 정확도**를 유지하면서도, **YOLO/SSD 수준의 속도**에 근접한 성능을 달성함.

### Methodology Details
- **Backbone**: 일반적으로 **ResNet-101**을 사용하며, 마지막 convolutional feature map까지 전체 이미지를 처리함.
- **Position-sensitive score maps**:
  - 마지막 feature map에서 각 클래스마다 k × k개의 **position-sensitive score map**을 생성 (예: 7×7).
  - 즉, 총 클래스 수 C에 대해 k×k×C 개의 channel이 생성됨.
- **Position-sensitive ROI Pooling**:
  - 각 Region Proposal을 k×k grid로 나누고, 각 grid 위치에 해당하는 score map의 channel을 선택하여 pooling.
  - 이를 통해 ROI 내부의 **공간 정보를 유지**하면서, 각 위치의 feature를 정밀하게 추출함.
- **Prediction**:
  - pooling된 k×k feature를 평균(mean)하여 각 클래스에 대한 confidence score를 얻음.
  - 추가적인 fully connected layer 없이 바로 classification 및 bbox regression 수행.
- **BBox Regression**:
  - 별도의 branch에서 conventional 방식으로 regression 예측 수행.

#### 기술적 특징
- **Fully Convolutional Detection**: 전체 네트워크가 convolution 연산만으로 구성되어 연산 효율이 매우 높음.
- **Position-Sensitive Mechanism**: ROI 내부의 공간 정보를 반영하여 정확한 localization 가능.
- **Faster R-CNN 수준의 정확도 + YOLO/SSD급 속도**: 정확도와 효율성의 균형을 이룸.
- **단순한 학습**: End-to-end 구조로 학습이 용이하며, proposal만 있으면 추가 구조 없이 학습 가능.

### Recap
R-FCN은 Faster R-CNN의 정확도는 유지하면서도 연산 속도를 크게 향상시키기 위해, **ROI별 연산을 convolution으로 치환**하는 방식의 Fully Convolutional Detector이다. 핵심은 각 위치에 특화된 feature를 얻기 위해 제안한 **Position-sensitive score map + ROI pooling** 구조로, 이 구조는 classification과 localization 양쪽에 spatial sensitivity를 부여하면서도 연산 효율을 극대화했다. R-FCN은 이후 **Deformable R-FCN**과 같이 구조적으로 더 확장되며 강건한 객체 탐지기로 발전하였다.

---

**한계점 및 후속 발전 방향**
- R-FCN의 position-sensitive pooling은 고정된 grid 기준이기 때문에, **비정형 객체나 자유 형태의 영역 처리에 한계**가 있음.
- 이를 개선하기 위해 **Deformable Convolution + Deformable ROI Pooling**을 결합한 **Deformable R-FCN**이 제안되어, 객체 형태에 따라 유연한 위치 선택이 가능하도록 확장됨.
