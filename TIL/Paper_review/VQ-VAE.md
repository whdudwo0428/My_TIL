## VQ-VAE: Neural Discrete Representation Learning  
#### 2025-04-06 / [https://arxiv.org/abs/1711.00937](https://arxiv.org/abs/1711.00937)

### Problem Statement
- 기존의 VAE(Variational Autoencoder) 및 AE(Autoencoder) 계열 모델은 **잠재 공간(latent space)이 연속적**이기 때문에, discrete symbol 기반의 표현이 중요한 **음성, 텍스트, 구조적 데이터 표현에 한계**가 있음.
- 또, GAN은 고품질 샘플을 생성하지만 **잠재 공간에 대한 명확한 해석 불가능**, VAE는 해석 가능한 잠재 공간을 제공하지만 **샘플 품질이 낮은 문제**가 있음.
- 따라서 **discrete latent representation을 사용하면서도**, end-to-end 학습이 가능한 새로운 생성 모델이 요구됨.

### Solution Approach
- 본 논문에서는 **Vector Quantized Variational Autoencoder (VQ-VAE)**를 제안함.
- 연속적인 잠재 공간 대신, 사전 정의된 **코드북(codebook, 임베딩 테이블)**에서 가장 가까운 벡터로 양자화(quantization)하는 방식으로 **discrete latent representation**을 학습함.
- Autoencoder 구조를 기반으로 하되, latent vector를 continuous하게 사용하는 대신 **최근접 임베딩으로 대체**하는 구조.

### Methodology Details

#### 1. **Architecture**
- **Encoder**: 입력 데이터를 latent vector z(x)로 변환
- **Quantization**:
  
![image](https://github.com/user-attachments/assets/b29b2c48-81b2-4198-9909-61c43c33b3d3)

- **Decoder**:
- 
![image](https://github.com/user-attachments/assets/4a59ed7a-9d6f-4402-aba2-49189bcf3e40)

#### 2. **Codebook (Embedding space)**
- 사전 정의된 K개의 embedding vector 집합
- ![image](https://github.com/user-attachments/assets/938f92f6-b971-4d3d-a53d-ddaad87e39a5)

- 학습 중에 이 embedding vector들도 같이 업데이트됨

#### 3. **Loss Function**
- 총 손실 함수는 다음 세 항으로 구성됨:
![image](https://github.com/user-attachments/assets/ec87b198-2015-49b8-a9b1-08ca51c718c4)
  - 여기서 `sg`는 **stop-gradient** 연산자로, 역전파를 특정 부분에만 적용하게 함

- 최종 loss:
![image](https://github.com/user-attachments/assets/86823ea9-3902-4de3-9c2f-c9dc60188bf9)


#### 4. **Training Stability**
- gradient가 양자화 지점에서 끊기므로 **straight-through estimator**를 사용해 decoder로 gradient를 우회 전달함

#### 5. **Applications**
- **음성 신호**에서 discrete representation을 사용해 WaveNet 기반 decoder로 고품질 음성 합성 성공
- 이미지 및 텍스트 생성에도 적용 가능

### Recap
VQ-VAE는 **continuous latent vector 대신 discrete codebook 기반 latent representation**을 도입한 첫 Autoencoder 계열 모델로, **양자화(quantization) + end-to-end 학습**을 동시에 달성했다. Encoder는 입력을 잠재 벡터로 인코딩하고, 이를 가장 가까운 코드북 벡터로 대체한 뒤 Decoder로 복원한다. VAE의 장점인 잠재 공간 해석 가능성과 GAN의 장점인 고품질 생성을 결합할 수 있는 강력한 기반이 되며, 이후 VQ-VAE 2, VQ-GAN 등으로 발전하였다. 특히 discrete symbol이 중요한 음성, 언어, 구조적 데이터에서 탁월한 성능을 보였다.

---

**한계점 및 후속 발전 방향**
- 코드북 크기 및 벡터 차원 수 설정에 민감
- codebook collapse 현상 (일부 코드북만 선택되는 문제) 발생 가능
- 이후 VQ-VAE 2에서는 hierarchical structure와 autoregressive prior를 결합해 expressive power를 확장함
