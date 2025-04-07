## Test-Time Tuning (Test-Time Training with Self-Supervision for Generalization under Distribution Shifts)  
#### 2025-04-06 ~ 04-07


### Problem Statement
- 딥러닝 모델은 훈련 데이터와 배포 환경(test-time)의 데이터 분포가 다를 경우 성능이 크게 저하됨.
- 기존 접근은 주로 학습 시 일반화(generalization)를 높이거나, 사후 적응(post-hoc adaptation)을 위해 target 도메인 데이터를 추가로 확보해야 함.
- 하지만 실제 상황에서는 test-time에서만 새로운 데이터가 주어지고, label은 없는 경우가 대부분. 이러한 **distribution shift 하에서의 label-free test-time adaptation**은 매우 도전적인 문제임.

### Solution Approach
- 이 논문은 **test-time에 unlabeled 데이터만 주어진 상황에서 모델이 스스로 적응할 수 있도록** self-supervised learning을 활용한 새로운 접근, **Test-Time Training (TTT)**을 제안함.
- 핵심 아이디어는 훈련 시 auxiliary self-supervised task(예: rotation prediction)를 병렬적으로 학습하고, test-time에서는 이를 이용해 unlabeled target data에서 backpropagation을 통해 feature extractor를 업데이트하는 방식.

### Methodology Details
- **Training Phase:**
  - 표준 supervised learning과 함께 auxiliary self-supervised task를 동시에 학습.
  - 대표적인 auxiliary task로는 **image rotation prediction**이 사용됨.
  - 모델 구성: shared feature extractor + supervised head(classifier) + auxiliary head(rotation classifier)

- **Test-Time Training Phase:**
  - test-time에는 label이 없기 때문에 auxiliary task의 loss만 사용하여 feature extractor를 업데이트함.
  - classifier는 고정(frozen) 상태로 두고, **feature extractor만 fine-tune**함.
  - 목표는 target domain에서의 특징 표현이 기존 classifier와 더 잘 맞도록 개선하는 것.

- **Optimization:**
  - test-time inference는 다음과 같은 순서를 따름:
    1. 입력 이미지에 대해 auxiliary task를 수행하여 rotation label 생성
    2. auxiliary loss 계산
    3. loss를 바탕으로 feature extractor만 update
    4. update된 feature를 통해 classifier 예측 수행

- **특징:**
  - label-free adaptation: test-time 데이터에 label이 필요 없음.
  - online adaptation: 하나의 샘플을 받고 바로 update 가능.
  - lightweight: 학습 시에는 추가 cost가 들지만, test-time에는 label이 없고 한 번의 업데이트만으로도 성능 향상 가능.

- **실험:**
  - CIFAR-100-C, ImageNet-C, ImageNet-R 등 다양한 corrupted dataset에서 실험 수행.
  - Baseline에 비해 robustness에서 큰 향상.
  - 특히 자연스러운 corruption(noise, blur 등)에 대해서 test-time tuning이 효과적임.

### Recap
- TTT는 기존 모델이 훈련된 상태 그대로 test 환경에서 적응할 수 있도록 하는 self-supervised 기반의 간단하고 실용적인 방법이다.
- test-time에 label이 없는 상황에서도, 훈련 시 설정된 auxiliary task를 활용하여 feature extractor를 업데이트함으로써 분포 변화(distribution shift)에 적응한다.
- 특히 auxiliary task로 rotation prediction을 사용함으로써, explicit한 label 없이도 feature representation을 개선하여 classifier의 성능을 향상시킨다.
- 사전 학습된 모델에 추가적인 학습 없이 쉽게 적용 가능하다는 점에서 범용성과 실용성이 높음.

**한계 및 개선 가능성:**
- auxiliary task 선택이 모델 성능에 큰 영향을 미치며, task가 target domain과 얼마나 관련성이 있는지가 중요함.
- feature extractor만 update하는 방식이므로, severe shift의 경우 classifier 재학습 필요 가능성 존재.
