## YOLOv3: An Incremental Improvement  
#### 2025-01-31 / [https://arxiv.org/abs/1804.02767](https://arxiv.org/abs/1804.02767)

### Problem Statement
- YOLOv2는 YOLOv1보다 정확도가 크게 향상되었으나, 여전히 **작은 객체의 탐지 성능 부족**, **복잡한 장면에서의 낮은 recall**, 그리고 다중 객체에 대한 예측 어려움 등의 문제가 남아 있음.
- 또, 기존 YOLO는 단순하고 빠르지만 **two-stage 방식(Faster R-CNN 등)보다 정확도가 낮은 one-stage 모델**이라는 한계를 지님.

### Solution Approach
- YOLOv3는 YOLOv2 구조를 계승하면서, 정확도를 개선하기 위한 여러 가지 **점진적인 개선(incremental improvements)**을 도입함.
- 주요 개선 사항은 다음과 같음:
  1. **multi-scale prediction (feature pyramid)**을 통한 작은 객체 탐지 향상
  2. **binary cross-entropy 기반 multi-label classification**
  3. **Darknet-53**이라는 더 깊고 효율적인 backbone 도입

### Methodology Details

#### 1. **Backbone: Darknet-53**
- YOLOv3는 새로운 backbone으로 **Darknet-53**을 제안함.
  - 53-layer convolutional network
  - ResNet 스타일의 **residual connection** 사용
  - 기존 YOLOv2의 Darknet-19보다 더 깊고 정확도가 높으며, 속도도 양호

#### 2. **Multi-scale Prediction**
- YOLOv3는 **세 가지 다른 크기의 feature map**에서 예측을 수행함.
  - Large-scale feature map: 큰 객체 탐지
  - Medium-scale: 중간 객체
  - Small-scale: 작은 객체
- 이는 **FPN(Feature Pyramid Network)** 구조와 유사하며, upsample + concatenate 방식 사용

#### 3. **Bounding Box Prediction (Anchor-based)**
- 각 feature map 위치에서 multiple anchor box를 사용하여 object 예측
  - Anchor box는 K-means로 클러스터링된 priors 사용
- 각 anchor box는 4개의 box 좌표 + objectness score + C개의 class 확률 예측

#### 4. **Multi-label Classification (Binary Cross Entropy)**
- YOLOv1, v2는 softmax를 사용하여 **exclusive classification**을 했으나, YOLOv3는 각 클래스에 대해 **독립적인 sigmoid 함수** 사용
  - 이는 multi-label 가능성을 열어주고, loss 계산을 안정화함

#### 5. **Other Improvements**
- Feature concatenation, upsampling, BN 등 최신 CNN 기법 도입
- 기존보다 높은 recall 및 더 균형 잡힌 precision-recall curve 달성

### Recap
YOLOv3는 YOLO 시리즈의 세 번째 모델로, YOLOv2의 속도와 단순성을 유지하면서도 정확도를 더욱 향상시키기 위한 **점진적인 개선들**을 제안하였다. 핵심은 **multi-scale prediction**, **residual 기반의 깊은 backbone(Darknet-53)**, 그리고 **sigmoid 기반 multi-label classification**이다. 이로 인해 다양한 크기의 객체를 정확히 탐지할 수 있으며, one-stage detector로서 Faster R-CNN에 가까운 정확도와 YOLO만의 속도를 동시에 달성하였다. YOLOv3는 이후 YOLOv4~8까지 발전하게 되는 시리즈의 중요한 전환점이 된다.

---

**한계점 및 후속 발전 방향**
- 여전히 anchor-based 구조이기 때문에 **anchor 설정 민감도 존재**
- NMS, confidence threshold 등의 post-processing이 복잡한 구조와 성능에 영향을 줌
- 이후 YOLOv4에서는 **CSPNet, PANet, SAM 등**을 도입해 성능 향상을 추구하고, YOLOv5~v8에서는 **경량화와 실시간성**이 더욱 강화됨.
