![image](https://github.com/user-attachments/assets/901068ed-2dcb-40cd-9517-7ee56b3df2ac)## Deep Residual Learning for Image Recognition  
#### 2025-02-07 / [https://arxiv.org/abs/1512.03385](https://arxiv.org/abs/1512.03385)

### Problem Statement
- 기존의 Convolutional Neural Network는 깊이가 깊어질수록 성능이 향상될 것으로 기대되지만, 실제로는 **네트워크가 깊어질수록 오히려 training error가 증가하는 현상**, 즉 degradation 문제가 발생한다.
- 이 문제는 단순한 overfitting이 아니라, 깊은 구조 자체가 **identity mapping을 학습하지 못하는 구조적 한계**에서 비롯된다.
- 따라서 네트워크가 더 깊어지더라도 **정보와 gradient가 손실 없이 전달될 수 있는 구조적 장치**가 필요하다.

### Solution Approach
- ResNet은 각 layer가 전체 mapping 함수 \( H(x) \)를 직접 학습하는 대신, **잔차 함수** F(x) = H(x) - x를 학습하도록 유도한다.
- 최종 출력은 다음과 같은 skip connection 구조로 계산된다:
![image](https://github.com/user-attachments/assets/26e83c58-9792-4edf-bd4d-6130d60ee4f5)


- 이 구조는 입력 \( x \)를 그대로 다음 layer에 더해주기 때문에, **gradient 흐름을 보존하고 identity mapping을 쉽게 학습**할 수 있게 한다.
- 이 residual 구조는 **degradation 문제를 해결하고**, 네트워크를 깊게 설계할 수 있도록 해준다.

### Methodology Details

- **Residual Block**은 다음과 같은 방식으로 구성된다:
![image](https://github.com/user-attachments/assets/8e9b37e4-1b97-4e98-9e28-6d1778af5af2)


  여기서mathcal F는 두 개의 3×3 convolution, batch normalization, ReLU로 구성되고, x는 입력 feature이다.

- 입력과 출력의 차원이 다를 경우에는 projection을 사용하여 skip connection을 수행한다:
![image](https://github.com/user-attachments/assets/945fefff-0247-4c47-a248-7d3331972596)


- 구조 구성:
  - ResNet-34까지는 basic block 구조를 사용하고, ResNet-50 이상에서는 bottleneck 구조 (1×1 → 3×3 → 1×1 conv)를 사용하여 파라미터 효율성을 높인다.

- ImageNet에서 ResNet-152는 top-5 error 4.49%를 달성했으며, 이는 당시 VGG나 GoogLeNet 대비 획기적인 성능 향상이다.
- CIFAR-10 등 다양한 데이터셋에서도 shallow network보다 deep residual network가 훨씬 낮은 training error를 기록한다.

### Recap
ResNet은 layer의 출력에 입력을 더해주는 skip connection 구조를 통해, 깊은 신경망에서도 학습이 가능하도록 설계된 모델이다. 네트워크는 복잡한 함수를 직접 학습하는 대신, 그 차이인 잔차를 학습하며, 이로 인해 정보 손실 없이 gradient가 전파될 수 있다. ResNet은 깊은 네트워크 학습의 구조적 문제를 해결하며, 이후 대부분의 딥러닝 모델에 기본 구성 요소로 채택될 정도로 큰 영향을 끼쳤다.

---

**한계점 및 후속 발전 방향**  
- residual connection이 학습을 안정화하긴 하지만, 네트워크 표현력을 높이기 위해서는 더 복잡한 skip 구조가 필요할 수 있다.
- 이후 DenseNet은 skip connection을 단순 덧셈이 아니라 모든 이전 layer 출력을 concat하여 사용하는 방식으로 발전시켰다.
- ResNeXt, Wide-ResNet 등은 ResNet 구조를 확장하거나 병렬화하여 정확도와 효율성을 동시에 향상시켰다.
