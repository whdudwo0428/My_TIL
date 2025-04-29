## UNet++: A Nested U-Net Architecture for Medical Image Segmentation  
#### 2025-04-29

### Problem Statement
- 기존 **U-Net**은 다양한 의료 영상 분할 문제에 효과적이지만, **encoder와 decoder 간의 표현 격차 (semantic gap)**로 인해 스킵 연결을 통해 전달되는 정보가 불완전하거나 노이즈를 포함할 수 있다.  
- 이러한 문제는 특히 복잡한 병변 경계나 작은 구조의 세밀한 분할이 필요한 작업에서 분할 정확도를 떨어뜨릴 수 있다.  
- 또한, 네트워크의 **깊이에 따른 정보 손실**과 **불필요한 계산 낭비** 역시 기존 구조의 제약으로 작용했다.

### Solution Approach
- UNet++는 이러한 문제를 해결하기 위해 **중첩 구조(nested skip pathways)**를 도입한 새로운 U-Net 변형 구조를 제안한다.  
- 주요 아이디어는 skip connection을 단순히 encoder와 decoder를 연결하는 데 그치지 않고, 그 사이에 **점진적인 feature 재조정 경로**를 삽입함으로써 semantic gap을 줄이는 것이다.  
- 이를 통해 각 decoder 레벨이 보다 풍부하고 의미 있는 feature를 바탕으로 학습할 수 있게 된다.

### Methodology Details
- **Dense skip pathways**:  
  - encoder와 decoder 사이의 스킵 연결 경로에 **intermediate convolution block**들을 계층적으로 삽입하여, 정보를 반복적으로 가공하며 전달한다.  
  - 각 노드는 이전 노드의 출력을 입력으로 받아, 더욱 정제된 feature map을 생성하게 된다.
- **Deep supervision**:  
  - 다양한 깊이의 출력 지점에서 분할 결과를 얻고, 이를 모두 학습에 활용함으로써 학습을 안정화시키고 일반화 능력을 높인다.
- **모듈화된 설계**:  
  - UNet++ 구조는 U-Net 대비 더 많은 연산량을 요구하지만, 학습 시 각 부분을 독립적으로 제어할 수 있어 **효율적 제어 및 최적화가 가능**하다.
- 전체 네트워크는 **encoder-bridge-decoder**의 틀을 유지하되, 각 skip path에 여러 depth의 sub-network들이 중첩(nested)되어 배치된다.

### Recap
UNet++는 U-Net 구조의 한계를 보완하기 위해 encoder와 decoder 사이에 중간 convolution block들을 반복적으로 삽입한 nested 구조를 가진다. 이를 통해 feature 간 semantic gap을 줄이고, 보다 정밀한 분할 성능을 달성한다. Dense skip pathways와 deep supervision을 통해 학습의 안정성과 표현력도 크게 향상되었다.

---

※ 한계 및 향후 방향  
- 구조가 복잡하고 연산량이 증가하므로, 메모리와 연산 자원이 제한적인 환경에서는 경량화가 필요하다.  
- 이후 연구에서는 Attention 기반의 skip connection, 경량화 구조(U2-Net 등) 등이 이어지며 성능과 효율성의 균형을 꾀하고 있다.
