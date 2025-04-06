## Feature Pyramid Networks for Object Detection  
#### 2025-01-27 ~ 01-28

### Problem Statement
- 객체 탐지는 다양한 **크기의 객체를 정확히 탐지하는 것**이 핵심 과제인데, 기존 CNN 구조는 **고해상도(초기 레이어)에는 작은 객체**, **저해상도(깊은 레이어)에는 큰 객체**에 유리한 반면,
- 일반적인 CNN은 **feature hierarchy를 classification 목적에 맞게 설계**해 놓았기 때문에, **다중 스케일에서 유의미한 표현력을 갖추기 어렵고**, 작은 객체 탐지에 취약함.
- 기존 방식은 이미지 피라미드(image pyramid)를 만들어 여러 해상도로 네트워크를 반복 실행하는 등 **연산비용이 큰 접근**에 의존했음.

### Solution Approach
- FPN은 CNN의 **자연스러운 피라미드 구조**를 활용하되, top-down 방식의 **feature map upsampling**과 lateral connection을 결합해 **다양한 스케일에서 강한 표현력의 feature pyramid**를 학습함.
- 이를 통해 **작은 객체부터 큰 객체까지 정확히 탐지**할 수 있는 **multi-scale feature representation**을 end-to-end 학습 구조 안에서 효율적으로 구현함.

### Methodology Details
- **Backbone**: 일반적으로 ResNet-50 또는 ResNet-101 사용.
- **Feature Pyramid Construction**:
  - **Bottom-up pathway**:
    - 일반적인 CNN의 feature extraction 흐름 (e.g., Conv1 → Conv2 → Conv3 → Conv4 → Conv5).
  - **Top-down pathway**:
    - 최상위 feature map (예: C5)을 upsample 하여 낮은 계층으로 전달.
    - 각 레벨의 feature map은 **2배 upsampling**되어 바로 아래 레벨과 **lateral connection**을 통해 결합.
    - lateral connection: 1×1 conv로 channel 수 정렬 후 element-wise addition.
  - 이 과정을 통해 P2~P5 같은 **top-down + lateral 통합 feature map**을 생성.
- **Prediction Head**:
  - 각 FPN level (P2~P5)에서 동일한 detection head를 공유하거나 적용하여 객체 탐지를 수행.
  - 작은 객체는 고해상도 레벨(P2), 큰 객체는 저해상도 레벨(P5)에서 탐지.

#### 기술적 특성
- **Feature Sharing across Scales**: 고정된 backbone feature map만으로 모든 scale에 대응 가능
- **Top-down + Lateral 연결 구조**: 고수준 표현력 + 저수준 해상도 정보를 결합
- **Computationally Efficient**: 별도 image pyramid 없이 다중 스케일 처리를 하나의 네트워크에서 해결
- **범용성**: Faster R-CNN, RetinaNet 등 다양한 detection framework에 바로 적용 가능

### Recap
FPN은 CNN의 기본 구조를 그대로 활용하면서도, **top-down + lateral 구조**를 통해 다중 스케일에서 강력한 표현력을 가지는 feature pyramid를 생성한다. 기존의 이미지 피라미드 방식보다 훨씬 효율적이며, 다양한 크기의 객체를 정밀하게 탐지할 수 있게 해준다. FPN은 이후 RetinaNet, Mask R-CNN, Cascade R-CNN 등 다양한 detection/segmentation 모델의 핵심 구성 요소로 자리잡으며, 객체 탐지 네트워크의 구조를 스케일 기반으로 혁신한 대표적 논문이다.

---

**한계점 및 후속 발전 방향**
- Top-down 구조가 고정된 방향성을 가지므로, **feature flow의 유연성이 부족**할 수 있음.
- 이후 BiFPN(EfficientDet), PANet(Mask R-CNN) 등은 FPN을 확장하여 **양방향 정보 흐름** 또는 **가중치 기반 결합** 등으로 성능을 더욱 개선함.

**느낀 점**
- FPN 자체가 새로운 개념보단 이전 모델들을 잘 조합해 성능을 높인거다보니 다른 논문을 공부할 때에 비해 내가 어떤걸 모르고 아는지를 좀 더 명확히 할 수 있었음. 해서 시간투자를 좀 해서 기존 모델들을 복습하고, 아래 내용을 처럼 기본이 되는 내용들을 더 익숙해지는데 집중함
- CNN 내 다양한 Layer들(fc,coonv,Reorg, ResidualConn 등)의 원리부터 Bottom-up, Top-down Pathway, Lateral Connetion 구조 등 다양한 구조적 개념 다시 정리해보는 시간을 가졌음
- K-means Clustering 을 공부하며 이전 논문을 리뷰하며 공부했던 수학개념들을 다시 복습(주로 Loss내 공식에서 찾아봤던 지시함수, 특이값분해, 이중합산 같은 선형대수적 내용)
- FPN을 리뷰하며 이전 논문들도 다시 돌아가서 찾는 경우가 많았고 이제 뭐가 뭔지 좀 알아듣는 느낌이 들었음
