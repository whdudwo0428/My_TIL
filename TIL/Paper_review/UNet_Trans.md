## TransUNet: Transformers Make Strong Encoders for Medical Image Segmentation
#### 2025-04-29

### Problem Statement
- 기존 **U-Net** 기반 의료 영상 분할 모델들은 국소적인(local) 특성은 잘 포착할 수 있었지만, **전역적(global) 문맥 정보를 효과적으로 캡처하지 못하는** 한계가 있었다.
- CNN 기반 Encoder는 receptive field 확장을 위해 깊은 네트워크가 필요하지만, 이는 계산량 증가와 정보 소실을 초래한다.
- 의료 영상에서는 정확한 구조적 관계와 장기 간 경계를 인식해야 하는데, 기존 CNN만으로는 충분한 전역 이해가 어려웠다.

### Solution Approach
- **Transformer 기반 Encoder**를 사용하여 **전역 정보를 효과적으로 포착**하고,
- 기존 **U-Net 구조의 Decoder**와 결합하여 **세밀한 지역 복원(localization)** 을 동시에 달성하는 하이브리드 아키텍처 제안.

### Methodology Details
- **아키텍처 구성**
  - **CNN 기반 백본** (예: ResNet)으로 먼저 로우 레벨 특징 추출
  - 이후, 특징 맵을 플랫(flatten)하여 **Transformer Encoder**에 입력하여 전역 문맥 정보를 학습
  - Transformer를 거친 feature는 다시 **decoder**로 보내져 해상도 복원 및 세분화(segmentation)를 수행
- **구체적 흐름**
  1. 입력 이미지는 CNN 백본을 통해 다단계 feature extraction.
  2. 마지막 CNN feature를 linear projection을 통해 patch embedding처럼 변환.
  3. 이 embedding을 **ViT(Vision Transformer) 구조**로 처리하여 전역 관계를 학습.
  4. Transformer 출력을 다시 구조화하여 U-Net Decoder에 투입.
  5. Skip Connection을 통해 CNN encoder의 intermediate feature들도 decoder로 전달하여 세밀한 복원 보조.
- **Loss Function**
  - Cross-Entropy Loss와 Dice Loss를 함께 사용하여 불균형 클래스 문제를 완화하고 segmentation 정확도를 높임.
- **실험**
  - Synapse multi-organ segmentation dataset 등 다양한 의료 영상 데이터셋에서 평가.
  - 기존 CNN 기반 segmentation 모델 대비 **성능 향상** 확인.

### Recap
TransUNet은 CNN으로 로우 레벨 특징을 뽑고, Transformer로 전역 정보를 포착한 후 U-Net decoder로 세밀한 복원을 수행하는 하이브리드 모델이다. CNN의 local focus와 Transformer의 global modeling 강점을 결합해 의료 영상에서 장기 구조 간 관계를 더 정확하게 이해하고 분할할 수 있게 했다. 특히 Transformer를 통해 receptive field를 급격히 확장하면서도 세밀한 지역 특성을 잃지 않는 것이 핵심이다.

---
※ 한계점: Transformer block 추가로 인한 연산량 증가 및 학습 데이터 요구량이 상대적으로 크며, 작은 데이터셋에서는 과적합 위험이 있을 수 있다.
