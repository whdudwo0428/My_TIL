## SSD: Single Shot MultiBox Detector  
#### 2025-01-25 / [https://arxiv.org/abs/1512.02325](https://arxiv.org/abs/1512.02325)

### Problem Statement
- YOLO v1은 객체 탐지를 단일 회귀 문제로 단순화하여 **실시간 처리**는 가능했지만, **작은 객체의 탐지 성능이 낮고 localization 정확도**가 떨어지는 문제가 있었다.
- 반면 R-CNN 계열은 정확하지만 **속도가 느려** 실시간 응용에 적합하지 않음.
- 따라서 **정확도와 속도를 동시에 만족**할 수 있는 모델이 요구됨.

### Solution Approach
- SSD(Single Shot MultiBox Detector)는 YOLO처럼 **단일 CNN으로 end-to-end 객체 탐지를 수행**하면서도,
- 다양한 크기의 객체를 탐지하기 위해 **여러 크기의 feature map에서 bounding box를 동시에 예측**하는 구조를 제안함.
- 이를 통해 높은 정확도와 빠른 속도를 동시에 달성함.

### Methodology Details
- **기반 네트워크**: 기본적으로 VGG-16 네트워크를 사용하며, fully connected layer를 제거하고 그 뒤에 **다중 스케일 feature layer**를 추가함.
  
- **Feature Pyramid**:
  - Conv4_3, Conv7 등 다양한 레이어에서 **다양한 해상도의 feature map**을 추출하여, 각 위치에서 박스를 예측.
  - 작은 해상도에서는 큰 객체, 높은 해상도에서는 작은 객체에 유리함.

- **Default Boxes (Prior Boxes)**:
  - 각 feature map 위치마다 다양한 **aspect ratio**와 **scale**을 가진 **기본 anchor box**를 미리 정의함.
  - 네트워크는 이 box들에 대해 class와 offset을 동시에 예측함.
  - 각 default box는 `(cx, cy, w, h)` 형태로 표현되며, 이를 기준으로 실제 박스를 회귀.

- **Prediction 구조**:
  - 각 feature map 위치마다 `k`개의 default box에 대해:
    - class score (C개)
    - box offset (4개: dx, dy, dw, dh)
  - 최종 출력은 다수의 feature map의 모든 위치에서 예측된 box 후보들의 집합

- **Loss Function**:
  - **Multi-task Loss** = Localization Loss(Smooth L1) + Confidence Loss(Softmax)
  - Hard Negative Mining을 적용하여 **배경 클래스 불균형**을 해결 (3:1 비율 유지)
  - Matching: 각 GT box는 IOU ≥ 0.5 이상인 default box와 매칭됨

#### 기술적 특징
- **Single-shot Detection**: 한 번의 forward-pass로 모든 class와 box를 동시에 예측
- **Multi-scale Prediction**: 다양한 크기의 feature map을 활용해 객체 크기 다양성에 대응
- **Default Box Matching**: 다양한 aspect ratio를 고려한 anchor box로 탐지 성능 향상
- **실시간 처리**: 59 FPS(VGG 기반)로 작동하면서도 Fast R-CNN보다 정확도 높음

### Recap
SSD는 YOLO처럼 단일 CNN으로 객체를 예측하지만, **다중 해상도 feature map을 활용하여 다양한 크기의 객체를 더 정교하게 탐지**할 수 있도록 설계되었다. 각 feature layer의 모든 위치에서 사전 정의된 다양한 크기와 비율의 default box를 기반으로 class와 위치를 동시에 예측하며, end-to-end 방식으로 학습된다. SSD는 속도와 정확도의 균형을 매우 잘 이룬 객체 탐지기로, YOLO 대비 작은 객체 성능이 우수하고, Faster R-CNN 대비 처리 속도가 빠르다.

---

**한계점 및 후속 발전 방향**
- default box가 고정되어 있기 때문에 물체의 **형태나 구조에 따라 box가 잘 맞지 않을 수 있음**
- **Post-processing(NMS)** 비용이 GPU 병렬화에 최적화되어 있지 않음
- 이후 RetinaNet은 SSD의 anchor 기반 구조를 유지하면서도 **Focal Loss**를 통해 클래스 불균형 문제를 더욱 효과적으로 해결함.
