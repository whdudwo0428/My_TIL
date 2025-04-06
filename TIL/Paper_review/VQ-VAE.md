## VQ-VAE: Neural Discrete Representation Learning  
#### 2025-04-06 / [https://arxiv.org/abs/1711.00937](https://arxiv.org/abs/1711.00937)

### Problem Statement
- Variational Autoencoder(VAE)나 일반 Autoencoder는 잠재 공간(latent space)을 **연속적 공간(continuous space)**으로 정의하기 때문에, **텍스트, 음성, 구조적 데이터**와 같이 **이산적(discrete) 표현이 본질적인 데이터의 특성**을 효과적으로 포착하지 못함.
- GAN은 고해상도 생성을 가능하게 하지만 **잠재 표현 해석 가능성은 부족**하고, VAE는 해석이 가능하지만 **생성 샘플의 품질이 낮은 단점**이 있음.
- 따라서 **이산적인 latent representation을 가지면서도**, **end-to-end 학습이 가능한 생성 모델**이 요구된다.

### Solution Approach
- 본 논문은 **Vector Quantized Variational Autoencoder (VQ-VAE)**를 제안한다.
- 핵심 아이디어는 연속적인 latent vector를 사전 정의된 이산적인 **코드북(codebook)** 내의 벡터 중 하나로 **양자화(quantization)**하는 방식이다.
- Encoder는 연속값을 출력하지만, 이 값은 가장 가까운 코드북 벡터로 치환되어 Decoder로 전달된다.
- VAE의 latent space를 **discrete set으로 바꾸면서도 backpropagation을 유지할 수 있는 트릭**을 도입해 end-to-end 학습을 가능하게 했다.

### Methodology Details

#### 1. 모델 구성
- **Encoder**  
  입력 \( x \)를 latent embedding \( z_e(x) \in \mathbb{R}^D \)로 변환

- **Quantization**  
  코드북 \( e = \{ e_1, e_2, \dots, e_K \} \subset \mathbb{R}^D \) 중  
  \( z_e(x) \)와 가장 가까운 벡터 \( e_k \)를 선택

  \[
  z_q(x) = e_k \quad \text{where} \quad k = \arg\min_j \| z_e(x) - e_j \|_2
  \]

- **Decoder**  
  양자화된 latent \( z_q(x) \)로부터 복원값 \( \hat{x} \)를 생성

#### 2. 손실 함수 구성

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

- 여기서 `sg`는 stop-gradient 연산으로, 해당 항목에서 gradient가 흐르지 않도록 차단하는 역할을 한다.

- **최종 손실 함수**:  
  \[
  \mathcal{L} = \mathcal{L}_{\text{recon}} + \mathcal{L}_{\text{vq}} + \mathcal{L}_{\text{commit}}
  \]

#### 3. 학습 기법
- **Straight-Through Estimator**  
  양자화 과정은 비미분 가능하므로, backpropagation 시 \( z_q(x) \)에 대한 gradient를 \( z_e(x) \)로 직접 전달한다.

#### 4. 활용
- VQ-VAE는 discrete latent code를 학습할 수 있어, **WaveNet decoder**와 결합해 음성 합성에도 활용되었고,
- 이미지 압축, 텍스트 생성 등 **압축성과 구조적 표현력이 중요한 문제들**에 효과적으로 적용될 수 있다.

### Recap
VQ-VAE는 **continuous latent space를 discrete한 벡터 집합(codebook)으로 양자화**하여 표현하는 autoencoder 구조이다. Encoder는 연속적인 임베딩을 생성하고, Decoder는 이 임베딩을 코드북 벡터로 대체한 값을 기반으로 출력을 재구성한다. 학습은 stop-gradient 및 straight-through estimator 기법을 통해 양자화의 비미분 가능성을 극복하며 수행된다. 이 구조는 이후 VQ-VAE 2, VQ-GAN 등으로 확장되며, **discrete latent modeling의 대표적인 프레임워크**로 자리잡았다.

---

**한계점 및 후속 발전 방향**
- 코드북 크기나 embedding 차원 수는 성능에 큰 영향을 미치며, 잘못 설정 시 **codebook collapse** 문제가 발생할 수 있음.
- VQ-VAE-2는 이 구조를 **hierarchical latent + autoregressive decoder**로 확장하여 성능을 대폭 향상시킴.
- 이후에는 VQ-GAN을 통해 코드북 구조와 GAN 생성을 결합한 고품질 생성 모델로 발전함.
