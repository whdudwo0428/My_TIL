## YOLOv4: Optimal Speed and Accuracy of Object Detection  
#### 2025-02-01 / [https://arxiv.org/abs/2004.10934](https://arxiv.org/abs/2004.10934)

### Problem Statement
- YOLOv3는 실시간 성능과 정확도의 균형을 잘 맞춘 객체 탐지기였지만, 이후 연구들(예: EfficientDet, RetinaNet, Faster R-CNN 등)은 더 높은 정확도를 달성하고 있음.
- YOLO 시리즈는 **속도는 빠르지만 정확도에서 SOTA를 따라가지 못함**.
- 따라서 **실시간 처리 가능한 속도는 유지하면서도**, COCO와 같은 벤치마크에서 **최신 탐지기들과 경쟁할 수 있는 정확도**를 달성할 필요가 있음.

### Solution Approach
- YOLOv4는 기존 YOLOv3 구조를 계승하면서도 **다양한 최신 딥러닝 기법을 조합적으로 통합**하여 정확도를 극대화한 one-stage 객체 탐지기임.
- 핵심은 새로운 backbone(CSPDarknet53), enhanced neck(PANet + SPP), 그리고 다양한 **Bag of Freebies**와 **Bag of Specials**를 적극 도입하여 **성능 향상과 속도 유지의 두 마리 토끼를 모두 잡음**.

### Methodology Details

#### 1. **Backbone: CSPDarknet53**
- YOLOv3의 Darknet-53을 개선한 **CSPNet(Cross Stage Partial Network)** 기반의 backbone 사용
  - feature duplication 문제를 완화하고, 연산량은 줄이면서도 정확도는 유지
  - ResNet처럼 residual block 기반이면서도, **partial gradient flow** 구조로 효율적인 학습 가능

#### 2. **Neck: SPP + PANet**
- **SPP (Spatial Pyramid Pooling)**: 다양한 receptive field의 정보를 캡처하여 **context 강화**
- **PANet (Path Aggregation Network)**: bottom-up 경로 추가로 **저수준과 고수준 feature 간 정보 흐름 개선**
- 이를 조합하여 backbone에서 얻은 feature를 rich하게 표현

#### 3. **Head**  
- YOLOv3와 동일한 **multi-scale detection head (3개의 feature scale)** 사용  
- anchor-based 방식 유지 + bounding box regression + class 예측 (sigmoid)

#### 4. **Bag of Freebies (훈련 시 성능 개선 요소)**  
- **Mosaic Data Augmentation**: 여러 이미지를 합쳐 다양한 배경과 객체 배치 학습 가능
- **DropBlock Regularization**: overfitting 방지
- **CIoU Loss**: 기존 IoU loss보다 더 강력한 localization 성능 제공
- **Self-adversarial training (SAT)**: 네트워크가 스스로 자신의 약점을 강화하는 방식으로 학습

#### 5. **Bag of Specials (추론 시 성능 향상 요소)**  
- **Mish Activation Function**: ReLU보다 smooth하고 정보 보존력 높은 비선형 함수
- **Cross Mini-Batch Normalization (CmBN)**: 작은 배치에서도 안정적인 normalization
- **SAM block**: spatial attention을 통한 feature 강조

#### 성능
- COCO test-dev 기준:
  - **AP (Average Precision)**: 43.5%
  - **FPS (Tesla V100 기준)**: 실시간에 충분한 62 FPS
- **실시간 조건에서 최고 성능 객체 탐지기**로 등극 (2020년 당시)

### Recap
YOLOv4는 기존 YOLOv3를 기반으로 **최신 백본(CSPDarknet53), 강화된 neck 구조(SPP + PANet), 다양한 학습 및 추론 기법**을 통합함으로써 **속도와 정확도 사이의 균형을 최적화한 one-stage 객체 탐지기**이다. 특히 여러 Bag of Freebies와 Specials의 조합을 통해 추가 연산량 없이 학습 효율을 극대화하며, SOTA 모델들과 경쟁 가능한 성능을 달성했다. 실시간 응용이 중요한 분야에서 가장 균형 잡힌 객체 탐지기로 널리 활용되었다.

---

**한계점 및 후속 발전 방향**
- anchor-based 구조의 한계를 여전히 가지고 있음 (anchor 설정에 민감)
- 구조가 복잡하고 조합이 많아 **이론적 분석보다는 경험적 최적화에 의존**함
- 이후 **YOLOv5~YOLOv8**에서는 PyTorch 기반 구현, anchor-free 방식 도입, 경량화 및 모듈화가 이루어짐

**느낀 점**
- YOLOv4에서는 개인적으로 새로운 개념과 다양한 기법들이 대거 도입된 느낌을 받아 처음 객체탐지 모델 논문을 읽었을 때 처럼 막막한 기분이 들었다. (한줄마다 새로운 개념과 단어들이 계속 나오는... 심지어 그때보다 더 복잡하다...) YOLOv3같은 기존 논문들까지는어느정도 특정 모듈의 개선을 중심으로 발전시켰던 분명 심플한 디자인의 모델이었던것 같은데 말입니다. 특히 Bos, BoF 같은 새로운 개념을 접하며 이전 네트워크 개선에 대한 공부 뿐만 아니라 성능 향상에 기여하는 다양한 요소와 기반지식들을 체계적으로 공부하고 넘어가야할 필요성을 느꼈다. Bos, BoF뿐만 아니라 CSPDarknet53, PANet, CIoU, Mish activation, Mosaic augmentation 등 더 복잡한 개념들을 접하며 너무 힘들었던 review였다...
