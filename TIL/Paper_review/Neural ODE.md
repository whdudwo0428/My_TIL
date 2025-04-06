## Neural Ordinary Differential Equations  
#### 2025-02-02 / [https://arxiv.org/abs/1806.07366](https://arxiv.org/abs/1806.07366)

### Problem Statement
- 기존 딥러닝 모델은 **고정된 깊이의 layer stack**을 사용해 데이터를 변환하지만, 이는 계산 그래프가 정해져 있고 **매끄러운 연속적인 시간 변화(dynamic transformation)**를 표현하기 어려움.
- 또한 ResNet, Highway Network 등은 skip connection을 통해 깊은 모델을 안정적으로 학습하지만, 본질적으로는 여전히 **이산적인 레이어 구조(discrete depth)**를 가진다.
- 따라서 **연속적인 시간 변화로 정의된 신경망 구조**, 즉 수학적으로 **미분 방정식(ODE)**을 통해 feature를 연산할 수 있는 프레임워크가 요구됨.

### Solution Approach
![image](https://github.com/user-attachments/assets/1bf77707-17cf-4992-8e3d-630b79b8a6ab)


- 즉, layer 쌓기를 수치적 미분 방정식 해법으로 대체하고, ODE solver를 통해 **연속적으로 정의된 hidden state**를 계산한다.

### Methodology Details

#### 1. Core Idea: ODE 대신 forward propagation
![image](https://github.com/user-attachments/assets/9fe8b02d-602c-44d0-8130-1ec0866a7aac)


#### 2. 학습: Adjoint Sensitivity Method
![image](https://github.com/user-attachments/assets/b90da7db-2c6c-4b0b-9a04-267fcf13300b)

- 이 방식은 역전파 동안 hidden state를 모두 저장하지 않아도 되기 때문에 **메모리 사용량이 상수 수준(O(1))**으로 유지됨

#### 3. Neural ODE의 구성 요소
- **정방향 계산**: ODE solver를 사용해 hidden state를 적분함
- **역전파 계산**: adjoint ODE를 통합하여 gradient 계산
- **학습**: mini-batch SGD로 파라미터 업데이트
- **ODE Solver**: Runge-Kutta, Dormand–Prince, Euler 등 다양한 수치해법 사용 가능

#### 4. 응용 사례
- 이미지 분류(MNIST, CIFAR-10) 등에서 기존 ResNet과 비교
- Latent ODE 모델을 통해 시계열 모델링 및 **불규칙 시간 간격 데이터 처리** 가능
- Normalizing Flow에도 응용되어 **Continuous Normalizing Flows (CNF)** 개념으로 확장됨

### Recap
Neural ODE는 전통적인 layer stacking 방식의 신경망을 일반화하여, **feature transformation을 시간에 따른 연속적인 미분 방정식으로 정의한 새로운 모델**이다. Forward pass는 ODE solver를 통해 적분으로 수행되고, backward는 adjoint sensitivity method를 사용해 효율적으로 gradient를 계산한다. 이 구조는 특히 **연속 시간 모델링, low memory cost training, 그리고 역동적인 표현 학습**에 강점을 가지며, 이후 Latent ODE, FFJORD, CNF, Score-based 모델 등 다양한 확장으로 이어졌다.

---

**한계점 및 후속 발전 방향**
- ODE solver의 연산량이 고정되어 있지 않고, 문제 난이도에 따라 **adaptive step 수가 달라짐** → 연산량 예측 어려움
- 훈련 속도가 느리고, stiff ODE (급격히 변화하는 함수)에 대한 해석에 한계가 있음
- 이후 FFJORD는 **ODE 기반 flow 모델을 확장**하고, ANODE는 **state augmentation**을 통해 표현력을 개선함

**느낀 점**
- ODE 기초부터 Neural의 수치적접근을 코드로 구현하는 과정까지 등 넓게 이해하려 함
- 이거하면서 옛날에 공부했던 것들의 loss도 같이 보면서 수학공부 엄청함...
