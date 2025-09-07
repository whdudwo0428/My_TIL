## Training Compute-Optimal Large Language Models

#### 2025-09-07

### Problem Statement

* *Scaling Laws for Neural Language Models* (Kaplan et al., 2020)은 모델 크기, 데이터 크기, 연산량이 성능에 미치는 영향을 파워 법칙으로 정량화했다.
* 그러나 제시된 **compute-optimal trade-off**에는 한계가 있었다.

  * 데이터셋을 한 번만 사용하는 **non-reuse 가정**에 기반했기 때문에, 실제 환경(데이터 재사용이 불가피한 상황)과 맞지 않았다.
  * 결과적으로 데이터 크기를 과대평가하고 모델 크기를 과소평가하는 경향이 있었다.
* 따라서, **현실적인 환경에서 주어진 연산량을 모델 크기와 데이터 크기에 어떻게 배분해야 하는가**라는 문제가 새롭게 제기되었다.

### Solution Approach

* DeepMind 연구진(Hoffmann et al., 2022)은 Kaplan scaling law를 수정하여 **Chinchilla scaling law**를 제안했다.
* 핵심 아이디어:

  * 데이터와 모델 크기를 균형 있게 확장해야 compute-optimal 성능에 도달할 수 있다.
  * 연산량이 고정되어 있을 때, Kaplan이 제안한 것보다 모델은 더 작고 데이터는 더 많은 쪽이 효율적이다.
* 대표적 결과:

  * **Chinchilla 모델** (70B 파라미터, 1.4T 토큰 학습)은 **Gopher 모델** (280B 파라미터, 300B 토큰 학습)보다 훨씬 적은 파라미터로 더 많은 데이터를 학습했음에도 성능이 우수했다.

### Methodology Details

* 다양한 크기의 Transformer 언어 모델을 학습하며 손실 곡선을 측정.
* Kaplan scaling law와 비교:

  * Kaplan: 연산량이 고정된 경우 모델 크기를 훨씬 크게 잡고 데이터는 적게 사용하는 것이 최적.
  * Chinchilla: 데이터와 모델 크기를 유사한 비중으로 확장하는 것이 더 효율적.
* 주요 발견:

  * 연산량이 4배 늘어나면, 모델 크기와 데이터 크기를 각각 2배씩 늘리는 것이 compute-optimal.
  * 모델 크기에 지나치게 치우친 확장은 효율성이 떨어진다.

### Recap

이 논문은 Kaplan scaling law의 한계를 보완하여 **Chinchilla scaling law**를 확립했다.
핵심 발견은 **compute-optimal 학습에서는 모델 크기보다 데이터 크기를 충분히 확보하는 것이 중요하다**는 것이다.
따라서 작은 모델이라도 충분히 많은 데이터를 학습하면, 더 큰 모델보다 높은 성능을 낼 수 있음을 실험적으로 증명했다.
