## Fast R-CNN  
#### 2025-01-23 ~ 01-24 / [https://arxiv.org/abs/1504.08083](https://arxiv.org/abs/1504.08083)

### Problem Statement
- R-CNN은 정확한 객체 탐지가 가능하지만, 각 Region Proposal에 대해 CNN을 **반복적으로 실행**하기 때문에 **연산량이 매우 많고 느림**.
- 또한, R-CNN은 훈련 과정이 복잡함: feature extraction, SVM 학습, bounding box regression이 **세 단계로 분리**되어 있어 end-to-end 학습이 불가능함.
- 이로 인해 효율성과 학습 통합 측면에서 개선이 필요함.

### Solution Approach
- Fast R-CNN은 **하나의 이미지에서 단 한 번만 CNN을 실행하여 feature map을 얻고**, 이 위에서 각 Region Proposal에 대해 ROI Pooling을 적용해 고정된 크기의 feature를 뽑음.
- 이후 이 feature를 classification과 bounding box regression에 **공동으로 사용하는 multi-task loss**를 통해 **end-to-end로 학습**이 가능하게 함.
- R-CNN 대비 속도와 정확도 모두를 향상시킴.

### Methodology Details
- **입력**: 입력 이미지 + Region Proposal (Selective Search 등으로 얻은 수천 개의 제안 영역)
- **단일 CNN 처리**: 전체 이미지를 CNN에 한 번만 통과시켜 **공통 feature map**을 생성
- **ROI Pooling**: 각 Region Proposal을 feature map 상의 영역으로 매핑한 뒤, 고정 크기의 벡터로 변환하는 **ROI Pooling layer** 사용
  - 이로 인해 다양한 크기의 영역을 동일한 fully-connected layer에 입력 가능
- **Fully Connected + Output**:
  - ROI feature는 fully-connected layer를 거친 후, 두 개의 출력 브랜치로 분기됨:
    1. **Softmax classification**: 각 ROI가 어떤 객체 클래스에 속하는지 예측
    2. **Bounding box regression**: 해당 ROI의 위치 보정값(x, y, w, h) 예측
- **Multi-task Loss**:
  - Classification loss + Bounding Box Regression loss를 함께 학습하여 end-to-end 방식으로 네트워크를 학습시킴

#### 주요 기술 포인트
- **공유 Feature Map**: 전체 이미지에 대해 CNN을 한 번만 수행하여 연산량을 대폭 절감
- **ROI Pooling**: 다양한 크기의 Region Proposal을 고정 크기로 변환하여 CNN의 입력 제한 문제를 해결
- **End-to-End 학습**: 하나의 네트워크에서 classification과 regression을 함께 학습할 수 있음
- **Fine-tuning 단순화**: SVM 없이 softmax를 이용하므로 별도 분류기 훈련이 필요 없음

### Recap
Fast R-CNN은 R-CNN의 비효율적 구조(Region마다 CNN 반복 수행, 복잡한 학습 절차)를 개선하여, 이미지 전체에 대해 단 한 번 CNN을 수행하고, ROI Pooling을 통해 모든 Region Proposal을 처리하는 효율적 구조를 제안하였다. Softmax 분류기와 bounding box regression을 end-to-end로 학습할 수 있으며, 속도와 정확도 모두에서 R-CNN과 SPP-Net을 능가한다. 이 구조는 이후 Faster R-CNN과 Mask R-CNN의 기반이 되었고, 현재까지도 ROI 기반 detection 구조의 핵심으로 남아 있다.

---

**한계점 및 후속 발전 방향**
- Region Proposal은 여전히 **Selective Search와 같은 외부 모듈**에 의존함 → 여전히 느리고 연산 비용이 큼.
- 이를 해결하기 위해 **Region Proposal Network(RPN)**를 CNN 내에 통합한 **Faster R-CNN**이 등장함.
