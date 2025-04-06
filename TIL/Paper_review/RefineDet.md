## RefineDet: Single-Shot Refinement Neural Network for Object Detection  
#### 2025-01-31 / [https://arxiv.org/abs/1711.06897](https://arxiv.org/abs/1711.06897)

### Problem Statement
- One-stage 탐지기(예: SSD, YOLO)는 속도는 빠르지만 정확도가 낮고 특히 **object localization precision과 false positives 문제가 큼**.
- Two-stage 탐지기(예: Faster R-CNN)는 정확하지만 느리고 복잡함.
- 즉, **정확도와 속도의 trade-off** 문제를 해결하고, one-stage 탐지기의 **classification/localization refinement 부족** 문제를 해소할 수 있는 새로운 구조가 필요함.

### Solution Approach
- RefineDet은 **two-stage 탐지기의 정밀도 + one-stage 탐지기의 속도**를 결합한 새로운 single-shot 탐지기 구조를 제안함.
- 전체 네트워크를 두 개의 모듈로 나눔:
  1. **Anchor Refinement Module (ARM)** – 초기 anchor box의 위치 조정 및 배경 제거
  2. **Object Detection Module (ODM)** – refined anchor 기반으로 최종 class 및 bounding box 예측
- 이 구조를 통해 **불필요한 anchor 제거 + 위치 정밀도 향상**을 달성

### Methodology Details

#### 1. **Two-Module Architecture**
- **Anchor Refinement Module (ARM)**:
  - SSD처럼 다중 해상도 feature map에서 anchor box를 배치하고,
  - 각 anchor에 대해 **binary classification (object vs background)** 및 **bounding box regression** 수행
  - 이 과정에서 coarse anchor location 보정 및 배경 anchor filter 수행 (negative anchor suppression)

- **Object Detection Module (ODM)**:
  - ARM에서 보정된 anchor를 입력으로 받아, **multi-class classification** 및 **refined bounding box regression**을 수행
  - feature는 ARM의 feature map을 **transfer connection block**을 통해 이어받음

#### 2. **Transfer Connection Block (TCB)**
- ARM의 feature map을 ODM에 전달할 때 단순 skip이 아니라, **upsampling + conv** 연산을 통해 전달
- 이를 통해 **spatial detail 보존 + semantic 강화** → 높은 detection 정확도 기여

#### 3. **Multi-scale Feature Usage**
- SSD와 마찬가지로 다양한 해상도의 feature map에서 anchor 예측 수행
- 각 단계에서 **refinement → detection** 순서로 진행되며, 효율적으로 작은 객체부터 큰 객체까지 커버

#### 4. **Loss Function**
- 전체 loss는 두 모듈의 loss를 합친 **multi-task loss**로 구성됨:
  - ARM: objectness classification + coarse regression
  - ODM: multi-class classification + refined regression

#### 성능
- PASCAL VOC, MS COCO 등에서 SSD 대비 **정확도 +1~3% 향상**
- RetinaNet, Faster R-CNN 수준의 성능을 유지하면서도 FPS는 더 빠름 (real-time 가능)

### Recap
RefineDet은 one-stage 탐지기의 단점인 localization precision 부족과 false positives 문제를 해결하기 위해, **anchor refinement → object detection**의 **2단계 구조를 통합한 single-shot detector**이다. ARM이 anchor 위치와 배경을 정제한 뒤, ODM이 해당 anchor에 대해 클래스와 박스를 예측하는 방식으로 구성된다. 이로 인해 high recall + low false positive 성능을 유지하며, SSD나 YOLO 대비 정확도가 크게 향상되었다. RefineDet은 one-stage 구조를 유지하면서도 two-stage의 정밀도를 추구한 대표적인 하이브리드 탐지기이다.

---

**한계점 및 후속 발전 방향**
- anchor 기반 구조이므로 anchor 설정(hyperparameter)에 여전히 민감
- 작은 객체 탐지 성능은 SSD보다 낫지만, RetinaNet 수준까지는 도달하지 못함
- 이후 anchor-free 방식(FCOS, CenterNet)이나 transformer 기반 detector(DETR) 등이 등장하며 구조 간소화와 성능 향상이 지속됨
