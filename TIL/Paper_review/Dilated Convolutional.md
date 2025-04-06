## Multi-Scale Context Aggregation by Dilated Convolutions  
#### 2025-02-06 / [https://arxiv.org/abs/1511.07122](https://arxiv.org/abs/1511.07122)

### Problem Statement
- Semantic segmentation과 같은 dense prediction 문제에서 **다양한 크기의 객체와 넓은 수용 영역(receptive field)** 확보가 핵심이다.
- 일반적인 CNN은 연속된 convolution과 pooling으로 깊어질수록 수용 영역이 넓어지지만, **해상도가 급격히 감소**하여 세밀한 위치 정보를 손실한다.
- 이를 보완하기 위해 사용되는 이미지 피라미드나 CRF 기반 후처리는 **복잡도와 연산량을 증가시키는 단점**이 있다.
- 따라서 **해상도는 유지하면서 수용 영역은 확장할 수 있는 convolution 구조**가 필요하다.

### Solution Approach
- 이 논문에서는 **Dilated Convolution** 또는 **Atrous Convolution**이라는 개념을 도입하여,  
  **해상도를 유지하면서도 필터의 수용 영역을 지수적으로 확장**할 수 있도록 한다.
- 기존 convolution을 일반화하여, 필터 내의 커널 사이 간격을 넓힘으로써 **정보 손실 없이 넓은 컨텍스트를 포착**할 수 있게 설계한다.
- Dilated convolution을 계층적으로 쌓아 다양한 scale의 컨텍스트 정보를 결합할 수 있다.

### Methodology Details

#### 1. **Dilated Convolution 정의**
- 일반 convolution은 \( k \times k \) 커널을 연속적으로 적용하며, receptive field는 느리게 증가한다.
- Dilated convolution은 각 커널 요소 간의 간격을 \( r \)이라 할 때, 다음과 같이 일반화된다:
![image](https://github.com/user-attachments/assets/73211f9d-b96a-4edc-b216-bea7eefd04c1)


  - \( r \): dilation rate (간격 크기)
  - \( r=1 \)이면 일반 convolution과 동일
  - \( r=2, 4, 8 \)처럼 점점 커질수록 더 넓은 영역을 보지만 계산량은 동일

#### 2. **Context Module**
- 여러 층의 dilated convolution을 **계단식으로 쌓아 수용 영역을 지수적으로 증가**
  - 예: dilation rate \( r = 1, 2, 4, 8, 16 \)
- 모든 연산은 **해상도를 유지한 채 수행**되므로, 출력 feature는 입력 크기와 동일
- 중간에 pooling 없이 순수하게 dilated conv만 사용함

#### 3. **적용**
- FCN 기반 semantic segmentation 구조의 **후반부에 dilated conv block을 삽입**
- 복잡한 후처리 없이도 정확한 예측 결과를 달성
- 다양한 크기의 객체에 대해 강인한 예측을 가능하게 함

### Recap
이 논문은 **dilated convolution (또는 atrous convolution)**이라는 핵심 연산을 통해, 해상도를 유지하면서도 수용 영역을 넓힐 수 있는 구조를 제안한다. 이를 통해 기존 CNN 구조보다 더 적은 연산으로 넓은 문맥 정보를 추출할 수 있으며, 특히 semantic segmentation 같은 dense prediction task에서 탁월한 성능을 발휘한다. 이 구조는 이후 DeepLab 시리즈(특히 DeepLabv2, v3, v3+)에서 핵심 컴포넌트로 채택되었고, 현재까지도 다양한 분야에서 사용되고 있다.

---

**한계점 및 후속 발전 방향**
- dilation rate가 커질수록 **그리드 아티팩트(grid artifact)**가 발생할 수 있음
- 이를 해결하기 위해 이후 DeepLab에서는 **ASPP (Atrous Spatial Pyramid Pooling)**을 도입하여 다중 dilation을 병렬적으로 사용함
- 최근에는 dilated convolution을 transformer나 attention 구조와 결합하는 시도도 활발함 (e.g., Dilated Attention)
