## Rich feature hierarchies for accurate object detection and semantic segmentation  
#### 2025-04-06 / [https://arxiv.org/abs/1311.2524](https://arxiv.org/abs/1311.2524)

### Problem Statement
- 전통적인 객체 탐지 방식(HOG + SVM + Selective Search)은 단일 스케일의 특징과 고정된 탐지 파이프라인에 의존하므로 복잡한 배경, 다양한 크기/형태의 객체, 조명 변화에 대해 강인하지 못함.
- 기존 딥러닝 기반 분류기(CNN)는 이미지 전체의 분류에는 강하지만, 정확한 객체의 위치를 찾는 데에는 부적합함.
- 따라서 정확한 객체 분할과 인식(semantic segmentation + localization)을 동시에 해결할 수 있는 새로운 접근이 필요함.

### Solution Approach
- 이 논문은 **Region-based Convolutional Neural Networks (R-CNN)**을 제안하여, 기존의 Region Proposal(Selective Search)과 CNN의 강력한 feature extractor를 결합.
- 이 접근은 Region Proposal을 먼저 얻은 뒤, 각 영역을 CNN을 통해 분류하고 박스를 정밀하게 보정(Bounding Box Regression)함으로써 localization과 classification을 동시에 수행함.

### Methodology Details
- **Selective Search**: 입력 이미지에서 약 2000개의 객체 후보 영역(region proposals)을 생성.
- **CNN feature extraction**: 각 후보 영역을 고정 크기(227x227)로 리사이징 후, 사전 학습된 AlexNet 계열 CNN을 통해 고차원 특징 벡터로 추출.
- **SVM Classification**: 추출된 feature를 각 클래스에 대한 SVM에 입력하여 객체 존재 여부를 판단.
- **Bounding Box Regression**: CNN feature를 활용해 예측된 바운딩 박스를 정밀하게 보정함.
- **Fine-tuning**: ImageNet으로 사전 학습된 CNN을 region-level 데이터셋(PASCAL VOC)으로 fine-tuning하여 detection 성능을 극대화.

#### 주요 기술적 포인트
- **Two-stage 구조**: Region Proposal + CNN-based Classification의 2단계 구조로 이후 Fast R-CNN, Faster R-CNN, Mask R-CNN 등의 기반이 됨.
- **CNN을 객체 탐지에 적용**: 이미지 전체가 아닌 ROI(Region of Interest)에 CNN을 적용함으로써 detection accuracy를 대폭 향상.
- **전이 학습(Transfer Learning)**: ImageNet pretraining을 detection task로 전이하여 데이터 부족 문제를 해결.
- **Bounding Box Regression**을 통해 localization precision을 강화.

### Recap
R-CNN은 기존의 전통적인 객체 탐지 방법의 한계를 극복하고자, CNN의 강력한 표현력을 Region Proposal과 결합하여 높은 정확도의 객체 탐지 시스템을 구현한 첫 모델이다. Selective Search로 후보 영역을 추출한 후, 각 영역에 CNN을 적용하여 feature를 추출하고, SVM으로 분류하며, 박스를 회귀(regression)로 보정하는 방식이다. 이후 모든 Region에 대해 반복적으로 CNN을 돌리기 때문에 느리다는 단점이 있었지만, 이후 Fast/Faster R-CNN으로 발전할 수 있는 기반이 되었고, CNN 기반 객체 탐지 연구의 시초가 된 역사적인 논문이다.

---

**한계점 및 후속 발전 방향**
- 모든 Region Proposal에 대해 CNN을 반복적으로 실행하므로 **속도가 매우 느림** (GPU로도 한 이미지 당 수 초 이상).
- 이후 **Fast R-CNN**에서는 feature map을 공유하고, **Faster R-CNN**에서는 Region Proposal Network(RPN)을 도입해 속도 문제를 해결함.
