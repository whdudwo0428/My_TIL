## Training Compute-Optimal Large Language Models

#### 2025-09-07

### Problem Statement

* \*\*Scaling Laws for Neural Language Models (Kaplan et al., 2020)\*\*은 모델 크기, 데이터 크기, 컴퓨트가 손실 감소에 미치는 영향을 파워 법칙으로 정량화했다.
* 그러나 그 논문에서 제시한 **compute-optimal trade-off** (주어진 연산량을 어떻게 모델 크기와 데이터 크기에 분배해야 하는가)에는 한계가 있었다.

  * Kaplan의 법칙은 데이터셋을 한 번만 사용하는 **non-reuse assumption**을 기반으로 했는데, 실제로는 데이터가 부족하여 \*\*중복 학습(data reuse)\*\*이 불가피하다.
  * 따라서, Kaplan 법칙을 그대로 적용하면 **데이터 크기를 과대평가**하고 **모델 크기를 과소평가**하는 문제가 생겼다.
* 새로운 질문: **주어진 연산량에서 모델 크기와 데이터 크기를 어떻게 설정해야 진정한 compute-optimal 학습이 가능한가?**

### Solution Approach

* DeepMind 연구진(Hoffmann et al., 2022)은 기존 Kaplan scaling law를 수정하여 **Chinchilla Scaling Laws**를 제안했다.
* 핵심 아이디어:

  * **데이터와 모델 크기의 균형을 재정립**한다.
  * 연산량이 고정되어 있을 때, 최적의 모델 크기는 Kaplan 법칙보다 작고, 대신 더 많은 데이터를 학습하는 것이 성능에 유리하다.
* 대표적인 결과:

  * Chinchilla(70B 파라미터, 1.4T 토큰)는 Gopher(280B 파라미터, 300B 토큰)보다 훨씬 적은 파라미터로 더 많은 데이터를 학습했음에도 불구하고, **성능이 뛰어남**을 보였다.

### Methodology Details

* 다양한 크기의 Transformer 언어 모델을 학습시키며 손실 곡선을 관찰.
* Kaplan scaling law와 비교:

  * Kaplan: 컴퓨트 최적화를 위해 데이터 수보다 모델 파라미터 수를 훨씬 크게 설정 → 데이터 효율성이 낮음.
  * Chinchilla: 데이터와 모델 크기를 비슷한 비중으로 늘려야 성능이 최적화됨.
* 주요 발견:

  * 주어진 FLOPs 안에서 **모델 크기와 데이터 크기가 같은 비중으로 증가해야 한다.**
  * 즉, 4배 더 많은 컴퓨트를 사용할 경우, **모델 크기와 데이터 크기를 각각 2배씩 늘리는 것이 최적**이다.
  * 모델 크기에 치우친 확장은 더 이상 compute-optimal이 아님을 증명.

### Recap

이 논문은 기존 Kaplan Scaling Laws를 개정하여 **Chinchilla Scaling Laws**를 확립했다.
핵심 주장은 **compute-optimal 학습에서는 모델 크기보다 데이터 크기를 충분히 확보하는 것이 중요하다**는 것이다.
그 결과, 작은 모델이라도 충분히 많은 데이터를 학습하면 초대형 모델보다 우수한 성능을 낼 수 있음이 실험적으로 증명되었다.

---

앞서 리뷰한 흐름을 정리하면:

1. **Scaling Laws for Neural Language Models** → 언어 모델의 성능이 파워 법칙을 따른다는 최초의 발견.
2. **Scaling Laws for Autoregressive Generative Models** → 해당 법칙이 언어 외에도 오토리그레시브 생성 모델 전반에 보편적으로 적용됨을 입증.
3. **Training Compute-Optimal LLMs (Chinchilla Laws)** → Kaplan 법칙의 한계를 수정하고, 실제 학습 환경에서 compute-optimal 분배 전략을 제시.
