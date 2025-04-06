## YOLO9000: Better, Faster, Stronger (YOLO v2)  
#### 2025-01-26 / [https://arxiv.org/abs/1612.08242](https://arxiv.org/abs/1612.08242)

### Problem Statement
- YOLO v1은 빠른 속도에도 불구하고 다음과 같은 단점을 가짐:
  - **Localization 오류가 큼**: grid 기반으로 위치를 coarse하게 예측
  - **작은 객체 탐지 성능이 낮음**
  - 모델 구조가 제한적이어서 ImageNet 등의 classification task와 통합되기 어려움
- 객체 탐지와 분류(classification)를 **동시에 학습**하여 더 많은 클래스를 다룰 수 있는 탐지기로의 확장이 필요함

### Solution Approach
- YOLO v2는 YOLO v1의 구조를 개선하고, 더 정교한 localization과 작은 객체 탐지 성능 향상을 위해 **anchor box, batch normalization, high-resolution classifier, multi-scale training** 등의 기법을 도입함.
- 또한 WordTree 구조를 이용해 **classification 데이터셋과 detection 데이터셋을 동시에 학습**할 수 있도록 하여, 최대 9000개 클래스 탐지가 가능한 YOLO9000으로 확장.

### Methodology Details
#### 구조 개선 (Better)
- **Batch Normalization**:
  - 모든 convolution layer에 적용 → 학습 안정화 및 mAP 약 2% 향상
- **High Resolution Classifier**:
  - Classification fine-tuning 시 입력 해상도를 448×448로 설정하여, detection resolution과 일치시킴
- **Anchor Boxes**:
  - Faster R-CNN처럼 **사전 정의된 여러 비율의 anchor box**를 도입해 bounding box 회귀를 개선
  - YOLO v1의 (x, y, w, h) 직접 회귀 대신, anchor box 대비 offset을 예측
- **Dimension Clustering**:
  - K-means clustering을 사용하여 학습 데이터에 가장 적합한 anchor box 크기를 자동 도출
- **Location Prediction 개선**:
  - 예측된 box 중심 좌표를 sigmoid 함수를 통해 0~1로 정규화해 grid cell 내부에 고정되도록 보정

#### 성능 개선 (Faster)
- **Passthrough Layer**:
  - 이전 계층(예: fine-grained feature layer)의 정보를 concat하여 작은 객체 정보 보존
- **Multi-scale Training**:
  - 학습 중 입력 이미지 해상도를 매 몇 iteration마다 변경 (e.g., 320~608 사이) → 다양한 스케일의 객체에 강인함

#### 확장 (Stronger, YOLO9000)
- **Hierarchical Classification via WordTree**:
  - ImageNet과 VOC/COCO 등 detection dataset의 label hierarchy를 통합하여 **멀티 태스크 학습** 가능
- **Joint Training**:
  - Detection dataset에는 위치 정보까지 학습시키고, classification-only dataset에는 클래스 계층 정보만 학습
  - 결과적으로 9000개 이상의 클래스를 실시간으로 탐지할 수 있음

### Recap
YOLO v2는 YOLO v1의 속도 장점은 유지하면서, **anchor box와 batch normalization, passthrough layer, multi-scale training** 등을 도입해 정확도를 크게 향상시킨 객체 탐지 모델이다. 또한 WordTree 구조와 공동 학습 방식을 통해 **YOLO9000으로 확장**되며, 분류 전용 데이터셋과 탐지 데이터셋을 동시에 학습해 수천 개의 클래스를 탐지할 수 있는 범용 객체 탐지기로 발전하였다. YOLO 시리즈의 실시간 탐지 철학을 유지하면서, 학습과 확장성 측면에서도 큰 진보를 이룬 논문이다.

---

**한계점 및 후속 발전 방향**
- YOLO v2는 작은 객체 탐지 성능이 개선되었지만, 여전히 **dense 객체 또는 겹쳐 있는 객체들에 대한 탐지 성능은 한계**가 있음.
- 이후 YOLO v3에서는 feature pyramid 구조와 다중 class predictor를 도입하여 이러한 문제를 더욱 개선하였음.
