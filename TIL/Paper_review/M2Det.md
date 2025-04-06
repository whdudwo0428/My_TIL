## M2Det: A Single-Shot Object Detector based on Multi-Level Feature Pyramid Network  
#### 2025-01-31 / [https://arxiv.org/abs/1811.04533](https://arxiv.org/abs/1811.04533)

### Problem Statement
- SSD, RetinaNet 등 기존 one-stage 탐지기들은 단일 backbone feature를 기반으로 feature pyramid를 구성하여 다양한 크기의 객체를 탐지하지만,
  - 대부분 **단일 backbone level에서 추출한 feature map을 단순 확장하거나 연결**하여 feature hierarchy를 구성함.
  - 이로 인해 **semantic 표현력은 강하지만 spatial 정보가 부족하거나**, 그 반대인 경우가 많아 **다양한 객체 크기에 모두 강인하지 못함**.
- 따라서 **multi-scale feature representation의 질을 높이고**, 객체의 크기 및 형태 변화에 강한 구조가 필요함.

### Solution Approach
- M2Det(Multi-Level Multi-scale Single-shot Detector)는 기존 SSD 구조를 개선하여,
  - 다양한 depth의 feature를 조합한 **multi-level feature pyramid**를 생성하고,
  - 이 feature pyramid 위에서 detection을 수행함으로써 **정확도와 속도 모두를 개선**함.
- 핵심은 **Thinned U-shape Module (TUM)**과 이를 계층적으로 쌓은 **multi-level fusion 구조**로 강력한 표현력을 갖는 feature map을 구축하는 것.

### Methodology Details

#### 1. **Backbone**
- VGG-16, ResNet-101, DenseNet-121 등 다양한 backbone 사용 가능
- 초기 backbone에서 low-level, mid-level, high-level feature를 추출하여 **base feature**로 사용

#### 2. **Feature Fusion Module (FFM)**
- 서로 다른 레벨의 backbone feature를 하나의 base feature로 융합
- FFMv1: backbone의 여러 scale feature를 결합하여 고차원 feature 생성 (base feature)
- FFMv2: TUM의 마지막 출력을 다시 결합하여 다음 TUM의 입력으로 사용

#### 3. **Thinned U-shape Module (TUM)**
- U-Net에서 착안한 구조이나 **얕고 가벼운 U 구조**
  - encoder-decoder 형태로 multi-scale feature 생성
  - 각 TUM은 입력 feature로부터 다양한 해상도의 feature map을 출력
- 여러 TUM을 쌓아 **multi-level pyramid** 구성
  - 각 TUM은 다양한 semantic depth를 가지므로, 여러 semantic abstraction 수준의 feature를 생성할 수 있음

#### 4. **Scale-wise Feature Aggregation Module (SFAM)**
- 모든 TUM 출력(feature pyramid)을 concat 한 뒤, channel-wise attention(Squeeze-and-Excitation) 기법을 통해 중요 feature 강조
- 최종적으로 **semantic-rich + scale-sensitive한 feature pyramid** 생성

#### 5. **Detection Head**
- 생성된 feature pyramid 각 scale에 대해 SSD-style detection head를 적용하여 class + box 예측

### Recap
M2Det은 기존의 one-stage 탐지기들이 단일 수준의 feature만으로 pyramid를 구성하는 한계를 극복하기 위해, **multi-level + multi-scale의 이중 피라미드 구조**를 제안한 모델이다. Backbone에서 추출된 다양한 레벨의 feature를 기반으로 base feature를 생성하고, 이를 통해 여러 TUM 모듈을 통과하며 다양한 수준의 feature pyramid를 구축한다. 이 과정을 SFAM으로 통합하여 semantic 정보와 spatial 정보를 모두 강화하며, SSD 대비 뛰어난 정확도와 RetinaNet 수준의 성능을 달성하였다.

---

**한계점 및 후속 발전 방향**
- 구조가 복잡해져 **모델 파라미터 수와 연산량이 증가**, 실시간 성능은 다소 저하됨
- FPN 구조에 attention을 결합한 SFAM은 성능 향상에는 기여하지만, **추론 속도와 메모리 사용량에 부담**
- 이후 EfficientDet, YOLOv4 등에서는 feature fusion 구조의 효율성과 경량화를 동시에 달성하기 위한 구조적 개선이 이어짐
