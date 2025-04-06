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
- **Encoder**: 입력 \( x \)를 latent embedding \( z_e(x) \in \mathbb{R}^D \)로 인코딩
- **Quantization**: 다음과 같이 코드북 \( \{ e_1, e_2, \dots, e_K \} \subset \mathbb{R}^D \) 중 가장 가까운 벡터로 양자화

  \[
  z_q(x) = e_k \quad \text{where} \quad k = \arg\min_j \| z_e(x) - e_j \|_2
  \]

- **Decoder**: 양자화된 latent \( z_q(x) \)를 받아 출력 \( \hat{x} \)를 생성

#### 2. 손실 함수

총 손실은 다음 세 가지 항으로 구성된다:

- **재구성 손실** (reconstruction loss):  
  \[
  \mathcal{L}_{\text{recon}} = \| x - \hat{x} \|_2^2
  \]

- **코드북 업데이트 항** (codebook loss):  
  \[
  \mathcal{L}_{\text{vq}} = \| \text{sg}[z_e(x)] - e \|_2^2
  \]

- **커밋 손실** (commitment loss):  
  \[
  \mathcal{L}_{\text{commit}} = \beta \| z_e(x) - \text{sg}[e] \|_2^2
  \]

여기서 \( \text{sg}[\cdot] \)는 **stop-gradient** 연산자로, 해당 항목에서 gradient가 흐르지 않도록 차단하는 역할을 한다.

- **최종 손실 함수**:  
  \[
  \mathcal{L} = \mathcal{L}_{\text{recon}} + \mathcal{L}_{\text{vq}} + \mathcal{L}_{\text{commit}}
  \]

#### 3. 학습 방법
- 양자화는 미분이 불가능하므로, **Straight-Through Estimator**를 사용해 \( z_q(x) \)에 대한 gradient를 \( z_e(x) \)에 직접 전달한다.

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
