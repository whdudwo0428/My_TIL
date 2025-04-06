## You Only Look Once: Unified, Real-Time Object Detection  
#### 2025-01-25 / [https://arxiv.org/abs/1506.02640](https://arxiv.org/abs/1506.02640)

### Problem Statement
- R-CNN 계열(Fast/Faster R-CNN 등)의 객체 탐지기는 높은 정확도를 보이지만, 여전히 Region Proposal → CNN → Post-processing으로 이어지는 **복잡한 파이프라인**과 **느린 속도**가 문제임.
- 특히 실시간 애플리케이션에서는 수백 밀리초 단위로 inference 시간이 필요한 기존 방식은 부적합함.
- 객체 탐지를 분류(classification) + 회귀(regression) + 탐색(proposal)의 조합으로 보지 않고, **단일 회귀 문제로 단순화**할 수 있는지에 대한 의문에서 출발함.

### Solution Approach
- YOLO(You Only Look Once)는 객체 탐지를 **end-to-end single neural network**로 처리하여, 이미지를 **한 번만 살펴보며** 객체의 존재 여부와 위치를 동시에 예측하는 구조를 제안함.
- 전체 이미지를 **S × S grid**로 나누고, 각 grid cell이 객체의 중심을 포함할 경우 해당 객체의 bounding box와 class를 예측하게 함.
- 이 방식은 매우 빠르며, detection을 **하나의 회귀 문제로 단순화**하여 실시간 탐지가 가능하게 함.

### Methodology Details
- **입력 처리**:
  - 고정 크기(448×448)의 이미지를 입력으로 받아 CNN을 통과시킴.
  - 마지막 출력은 **S × S × (B × 5 + C)** 크기의 텐서이며,
    - S × S: grid 개수 (보통 7×7)
    - B: 각 grid cell에서 예측하는 bounding box 개수 (보통 2개)
    - 5: 각 bounding box의 위치(x, y, w, h) + confidence score
    - C: 클래스 수 (예: PASCAL VOC의 경우 20)

- **CNN 구조**:
  - 24개의 convolutional layer + 2개의 fully connected layer로 구성.
  - classification network에서 영감을 받아 detection 전용으로 수정됨.

- **Loss Function**:
  - 좌표 예측: MSE (Mean Squared Error)
  - confidence score 예측: 객체 존재 여부에 따라 조정된 가중치 적용
  - class prediction: softmax cross-entropy
  - 위치 오차에 더 큰 비중을 두기 위해 위치 항에는 가중치 λ_coord를 부여함.

- **Prediction 과정**:
  - 한 이미지에서 모든 객체의 위치와 클래스 정보를 한 번에 예측.
  - Non-Maximum Suppression(NMS)을 통해 중복된 박스를 제거.

#### 핵심 개념
- **단일 네트워크 구조**: Region Proposal 없음. CNN → Class + Box → 바로 결과 출력
- **End-to-End Regression**: classification과 localization을 하나의 회귀 문제로 변환
- **실시간 속도**: YOLO는 GPU 기준으로 45fps, 경량화 버전(YOLO Fast)은 155fps까지 도달
- **Global reasoning**: 전체 이미지를 한 번에 처리하므로 context 정보를 더 잘 활용

### Recap
YOLO v1은 객체 탐지를 classification이나 proposal generation의 조합으로 보지 않고, 전체 이미지를 grid로 나누어 **한 번에(Class + Box) 예측**하는 새로운 패러다임을 제시했다. 하나의 CNN으로 detection을 end-to-end 처리하며, 기존 R-CNN 계열보다 수십 배 빠른 속도를 보여주었다. 이 구조는 실시간 애플리케이션에 최적화되어 있으며, 이후 YOLOv2~v8로 이어지는 시리즈의 초석이 되었다. 정확도 측면에서는 localization 정밀도가 다소 낮았지만, 속도와 단순함 면에서는 객체 탐지 역사에서 획기적인 전환점이었다.

---

**한계점 및 후속 발전 방향**
- 위치 예측 정확도가 낮고, 특히 **작은 객체(small object)나 인접 객체 구분이 어려움**
- 각 grid cell이 최대 하나의 객체만 예측하므로 다중 객체가 겹칠 경우 성능 저하
- 이후 YOLOv2에서는 anchor box 개념을 도입하고, 더 깊은 feature extractor를 사용하여 정확도를 개선함.
