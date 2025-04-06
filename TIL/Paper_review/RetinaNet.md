## Focal Loss for Dense Object Detection (RetinaNet)  
#### 2025-01-29 / [https://arxiv.org/abs/1708.02002](https://arxiv.org/abs/1708.02002)

### Problem Statement
- 기존의 two-stage 탐지기(Faster R-CNN 등)는 높은 정확도를 제공하지만, 속도가 느리고 구조가 복잡함.
- 반면 SSD, YOLO 등 one-stage 탐지기는 빠르지만 **정확도가 낮은 이유는 foreground:background 클래스 불균형** 때문이다.
- 대부분의 anchor box가 background이기 때문에, 모델이 쉽게 예측할 수 있는 **“easy negative”에 치중**하면서 학습이 왜곡되고, **hard example은 충분히 학습되지 않음**.

### Solution Approach
- RetinaNet은 one-stage 구조를 유지하면서도 **Focal Loss**를 도입하여, loss 함수 수준에서 **class imbalance 문제를 해결**함.
- Easy negative sample의 loss 기여도를 줄이고, hard positive/negative sample에 더 집중되도록 조정함으로써, **one-stage 모델이 two-stage 수준의 정확도**를 달성할 수 있게 함.

### Methodology Details
#### Backbone & Architecture
- **Backbone**: ResNet-50/101 + FPN (Feature Pyramid Network)
  - 다양한 크기의 객체 탐지를 위해 다중 스케일 feature map을 생성 (P3~P7)
- **Subnets**:
  - **Classification subnet**: 각 위치에서 anchor마다 class 확률 예측
  - **Regression subnet**: 각 위치에서 anchor마다 bounding box offset 예측
  - 두 서브넷은 모든 FPN 레벨에 걸쳐 **공통 구조(shared weights)**로 적용됨

#### Anchor & Prediction
- 각 FPN 레벨의 모든 위치에 대해 다양한 크기와 aspect ratio를 갖는 **anchor box**를 배치
- 총 수십만 개에 달하는 dense anchor box에서 class + box prediction을 동시에 수행

#### Focal Loss (핵심 기여)
- **기존 Cross Entropy Loss의 한계**: easy negative가 전체 loss를 지배
- **Focal Loss 정의**:
    - p_t　: 모델이 정답 클래스에 대해 예측한 확률
    - gamma: focusing parameter (보통 2 사용)
    - alpha: class imbalance를 보완하는 weighting factor
  - 핵심 효과:
    - **확신 높은 예측(예: p_t ≈ 1)은 loss를 거의 0으로 만듦** → easy sample 무시
    - **어려운 예측(p_t 낮음)은 loss가 커짐** → hard sample에 집중

#### 학습 세부사항
- Anchor-box matching은 IOU ≥ 0.5를 기준으로 Positive 할당
- Hard Negative Mining 불필요: Focal Loss가 자동으로 해결
- mAP 기준, RetinaNet은 COCO 벤치마크에서 **Faster R-CNN보다 높은 정확도**를 달성하면서도 one-stage 구조 유지

### Recap
RetinaNet은 one-stage detector의 가장 큰 약점이었던 **foreground-background 클래스 불균형** 문제를 **Focal Loss라는 새로운 손실 함수로 해결**하며, 정확도와 속도 모두를 달성한 모델이다. FPN 기반의 다중 스케일 feature map 위에서 anchor-based prediction을 수행하면서도, loss의 핵심을 근본적으로 재설계함으로써 two-stage 수준의 성능을 달성했다. RetinaNet은 이후의 EfficientDet, FCOS, ATSS 등 수많은 one-stage 탐지기의 설계 기반이 되었으며, dense detection의 새로운 기준을 제시한 논문이다.

---

**한계점 및 후속 발전 방향**
- 여전히 anchor-based 방식이라 anchor 설정(hyperparameter)에 민감
- **Anchor-free 방식**으로 전환한 FCOS, CenterNet 등은 RetinaNet 이후 등장하여 더 단순한 구조로 성능을 개선함
- Focal Loss는 classification에는 효과적이나, regression에는 적용되지 않음 → 향후 localization loss와의 결합 연구로 확장 가능
