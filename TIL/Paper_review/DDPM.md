## Denoising Diffusion Probabilistic Models (DDPM)

#### 2025-09-08

### Problem Statement

* 복잡한 데이터 분포(특히 고차원 이미지)를 정확하게 모델링하여 새로운 샘플을 생성하는 것은 기존 **GAN**이나 **VAE**의 한계 때문에 어려움이 많았다.
* **GAN**은 학습이 불안정하고 mode collapse 문제가 발생하기 쉽고, **VAE**는 생성 이미지가 흐리게 나오는 문제가 있었다.
* 따라서, 안정적으로 학습 가능하면서도 높은 품질의 샘플을 생성할 수 있는 새로운 생성 모델이 필요했다.

### Solution Approach

* 문제를 해결하기 위해 **확률적 확산 과정**(forward diffusion)과 **역확산 과정**(reverse diffusion)을 정의하고, 이를 통해 데이터를 점차적으로 잡음화(destroy)하고 다시 복원(denoise)하는 과정을 학습한다.
* 핵심 아이디어는 **Markov chain을 이용해 데이터에 점진적으로 Gaussian noise를 추가**하여 단순한 분포로 변환한 뒤, **신경망이 역과정을 학습**해서 원래 데이터를 복원하도록 하는 것이다.

### Methodology Details

* **Forward Process (Diffusion)**:

  * 원본 데이터 $x_0$에 점진적으로 Gaussian noise를 T 단계 동안 추가한다.
  * 최종적으로 $x_T$는 거의 pure Gaussian noise 분포에 도달한다.
  * 이 과정은 사전 정의된 **variance schedule**(예: 선형 증가 $\beta_t$)에 따라 진행된다.

* **Reverse Process (Denoising)**:

  * 학습된 신경망(보통 U-Net 구조)이 $x_t$에서 noise를 제거하여 $x_{t-1}$을 예측한다.
  * 실제로는 직접 $x_{t-1}$을 예측하지 않고, **추가된 noise $\epsilon*을 예측**하는 방식으로 학습한다.
  * 학습 목표는 네트워크가 “추가된 잡음”을 잘 복원하도록 하는 것이다.

* **Training Objective**:

  * Variational Inference 기반의 증분 KL divergence 최소화에서 유도된다.
  * 최종 손실 함수는 단순한 **MSE 기반 noise 예측**으로 정리된다:

    $$
    L = \mathbb{E}_{x_0, \epsilon, t}\left[ \| \epsilon - \epsilon_\theta(x_t, t) \|^2 \right]
    $$

* **Sampling**:

  * 학습이 끝난 후, 무작위 Gaussian noise에서 시작하여 신경망을 여러 step 동안 적용하면 고품질 이미지를 샘플링할 수 있다.
  * 이 때 “reverse diffusion”을 단계적으로 수행하여 노이즈 → 이미지로 생성된다.

### Recap

* DDPM은 데이터를 Gaussian noise로 점차 변환하는 **forward diffusion process**와 이를 역으로 되돌리는 **reverse denoising process**를 학습하는 생성 모델이다.
* 학습 목표는 각 단계에서 추가된 잡음을 정확히 예측하는 것(MSE 기반).
* 샘플링은 순수 노이즈에서 시작하여 학습된 역과정을 따라가며 점진적으로 denoise하는 방식.
* GAN 대비 안정적이며, VAE 대비 선명한 샘플을 제공하여 이후 **Stable Diffusion**, **Latent Diffusion** 등 다양한 변형 모델의 기초가 되었다.
