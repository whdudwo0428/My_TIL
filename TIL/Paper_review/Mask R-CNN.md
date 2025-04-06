## Mask R-CNN  
#### 2025-01-30 / [https://arxiv.org/abs/1703.06870](https://arxiv.org/abs/1703.06870)

### Problem Statement
- Faster R-CNN은 객체 탐지(object detection)에는 뛰어나지만, 각 객체의 형태를 픽셀 단위로 구분하는 **Instance Segmentation** 작업은 수행할 수 없음.
- 기존의 segmentation 모델들은 semantic segmentation에 초점을 맞추어 **객체 간 구분이 불가능**하고, detection과 분리된 구조를 갖는 경우가 많음.
- 따라서, 객체의 **위치, 클래스, 마스크(형태)를 end-to-end로 예측**할 수 있는 통합된 framework가 필요함.

### Solution Approach
- Mask R-CNN은 Faster R-CNN 구조에 **병렬적으로 segmentation mask branch를 추가**하여, 하나의 네트워크에서 **bounding box + class + binary mask**를 동시에 예측하도록 확장함.
- 특히 ROI Pooling의 정밀도 한계를 극복하기 위해 **ROI Align** 기법을 제안하여, 정확한 pixel-level alignment를 가능하게 함.

### Methodology Details
#### 전체 구조
- **Backbone**: ResNet-50/101 + FPN  
  - 다양한 크기의 객체 탐지를 위해 FPN을 통해 다중 스케일 feature map 생성

- **Region Proposal Network (RPN)**:  
  - Faster R-CNN과 동일하게 anchor 기반으로 객체 후보 영역(region proposals) 생성

- **ROI Align (핵심 기여)**:
  - 기존 ROI Pooling은 quantization으로 인해 feature misalignment 발생  
  - ROI Align은 bilinear interpolation을 통해 **정확한 spatial 위치**의 feature를 보존함 → 마스크 예측의 정밀도 대폭 향상

- **Heads**:
  - Classification Head: ROI에서 클래스 예측
  - Bounding Box Regression Head: ROI 위치 보정
  - **Mask Head (추가된 부분)**:
    - 각 ROI에 대해 고정 해상도(예: 28×28)의 binary mask를 예측하는 **fully convolutional network (FCN)**
    - 클래스 수만큼의 마스크를 예측한 뒤, 해당 클래스의 마스크만 선택

#### Loss Function
- 총 세 가지 loss가 multi-task로 함께 최적화됨:
  - Classification loss (softmax)
  - Bounding box regression loss (smooth L1)
  - Mask loss (per-pixel binary cross-entropy)

#### 성능
- COCO 데이터셋 기준으로 SOTA instance segmentation 성능 달성
- 높은 precision을 유지하면서도 **end-to-end 학습 가능**, 구조도 간결함

### Recap
Mask R-CNN은 Faster R-CNN 구조에 **pixel-level 마스크 분할 기능을 추가한 instance segmentation 모델**이다. 핵심 기여는 ROI Align을 통해 feature misalignment를 해결하고, 각 ROI에 대해 **클래스별 binary mask**를 예측하는 FCN branch를 추가한 것이다. Detection과 segmentation을 하나의 프레임워크에서 통합하면서도, 세 가지 예측(class, box, mask)을 병렬적으로 수행하여 **정확도와 구조적 간결성**을 모두 달성했다. 이후 수많은 segmentation 및 video object tracking 모델들의 기반이 되었다.

---

**한계점 및 후속 발전 방향**
- ROI Align과 3-branch 구조로 인해 Faster R-CNN 대비 **연산량 증가**
- **실시간 적용에는 부적합**하며, 경량화된 variant(Mask R-CNN Lite), anchor-free 구조(CenterMask) 등이 이후 등장
- 최근에는 Sparse R-CNN, DETR처럼 **set prediction 또는 transformer 기반 방식**으로 segmentation을 더 간결하게 수행하려는 시도가 이어짐
