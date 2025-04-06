## VQ-VAE: Neural Discrete Representation Learning  
#### 2025-04-06 / [https://arxiv.org/abs/1711.00937](https://arxiv.org/abs/1711.00937)

### Problem Statement
- Variational Autoencoder(VAE)와 일반 Autoencoder는 잠재 공간(latent space)을 **연속적 공간(continuous space)**으로 정의하기 때문에, **텍스트, 음성, 구조적 데이터**와 같은 **이산적(discrete) 표현이 본질적인 데이터**를 효과적으로 다루기 어렵다.
- GAN은 고품질 샘플을 생성할 수 있지만 잠재 표현의 해석 가능성이 낮고, VAE는 해석이 가능하지만 생성 품질이 낮은 단점이 있다.
- 따라서, **이산적인 latent representation을 사용하면서도 end-to-end 학습이 가능한 새로운 생성 모델**이 요구된다.

### Solution Approach
- 이 논문은 **Vector Quantized Variational Autoencoder (VQ-VAE)**를 제안한다.
- 연속적인 latent vector를 사전 정의된 **코드북(codebook)** 내의 벡터로 **양자화(quantization)**하여 이산 표현을 학습한다.
- VAE 구조에 **양자화 단계**를 삽입하고, **backpropagation이 가능한 학습 기법**을 도입하여, discrete latent space를 갖는 생성 모델을 end-to-end로 학습 가능하게 한다.

### Methodology Details

#### 1. 아키텍처 구성
![image](https://github.com/user-attachments/assets/ae8c27fb-3aa1-405f-8df5-c54e4fa32e23)


#### 2. 손실 함수

총 손실은 다음 세 가지 항으로 구성된다:

![image](https://github.com/user-attachments/assets/48983a4a-a7b0-4a3f-8e79-2dca840ee79e)

여기서 **sg**는 **stop-gradient** 연산자로, 해당 항목에서 gradient가 흐르지 않도록 차단하는 역할을 한다.

- **최종 손실 함수**:  
![image](https://github.com/user-attachments/assets/83324295-337a-4810-af4d-c7f099cc626f)


#### 3. 학습 방법
![image](https://github.com/user-attachments/assets/0ed6791c-7fb0-436b-ba7b-796cccc1809a)


#### 4. 활용 사례
- VQ-VAE는 discrete latent code를 활용하여 **WaveNet decoder와 함께 고품질 음성 합성**에 사용되었고,
- 이미지 생성, 텍스트 생성, 강화학습 등 다양한 도메인에서 **이산 표현 학습**에 응용되었다.

### Recap
VQ-VAE는 연속적인 잠재 공간 대신 **이산적인 코드북 벡터로 양자화된 latent representation**을 사용하는 Autoencoder 구조이다. Encoder가 생성한 latent vector는 가장 가까운 코드북 벡터로 대체되며, Decoder는 이를 입력으로 사용해 복원 결과를 생성한다. 손실 함수는 reconstruction, codebook, commitment 항으로 구성되며, stop-gradient와 straight-through estimator 기법을 통해 end-to-end 학습이 가능하다. 이 구조는 이후 **VQ-VAE-2, VQ-GAN** 등으로 발전하며, **구조적이고 해석 가능한 생성 모델의 새로운 기반**이 되었다.

---

**한계점 및 후속 발전 방향**
- 코드북 크기 및 차원 설정에 민감하며, **codebook collapse**와 같은 문제가 발생할 수 있음
- VQ-VAE-2는 **hierarchical latent + autoregressive decoder** 구조를 추가하여 더 복잡한 데이터 생성에 적합하게 확장됨
- 이후 VQ-GAN에서는 **GAN의 고품질 생성력과 VQ의 표현력**을 결합하여 고해상도 이미지 생성을 가능하게 함
