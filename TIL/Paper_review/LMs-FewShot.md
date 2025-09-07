## Language Models are Few-Shot Learners

#### 2025-09-07

### Problem Statement

* 기존 언어 모델들은 대규모 학습 이후에도 새로운 작업(task)에 맞추려면 **fine-tuning**이나 **task-specific architecture** 조정이 필요했다.
* 그러나 실제 응용에서는 모델을 다양한 작업에 빠르게 적용할 수 있는 \*\*범용성(generality)\*\*이 중요하다.
* 따라서, **대규모 언어 모델이 사전 학습만으로 얼마나 범용적 능력을 갖출 수 있는가?** 그리고 \*\*적은 예시(few-shot)로 새로운 작업을 수행할 수 있는가?\*\*라는 질문이 제기되었다.

### Solution Approach

* OpenAI 연구진(Brown et al., 2020)은 \*\*GPT-3 (175B 파라미터)\*\*를 개발하고, **in-context learning** 능력을 실험했다.
* 핵심 아이디어:

  * Fine-tuning 없이, 단순히 프롬프트(prompt)에 예시 몇 개를 제공하는 것만으로 모델이 새로운 작업을 수행할 수 있다는 점을 검증.
  * 즉, 모델이 **few-shot, one-shot, zero-shot learning**을 할 수 있음을 보였다.

### Methodology Details

* **모델 규모**: 175B 파라미터 Transformer (GPT-2의 확장).
* **실험 설정**:

  * **Zero-shot**: 단순히 task 설명만 주고 수행.
  * **One-shot**: 예시 하나 제공.
  * **Few-shot**: 예시 몇 개(보통 10\~100개) 제공.
* **평가 영역**: 번역, 질의응답, 산술, 상식 추론, 텍스트 생성 등 다양한 NLP 벤치마크.
* **결과**:

  * Few-shot setting에서 GPT-3는 기존 SOTA 모델과 경쟁할 정도의 성능 달성.
  * Zero-shot/one-shot에서도 놀라운 일반화 능력을 보임.
  * 그러나 일부 영역(추론, 수학적 계산, 상식 이해 등)에서는 여전히 한계가 명확히 드러남.
* **한계점 분석**:

  * 데이터셋 편향 → 사회적 편향과 윤리적 문제.
  * 장기적 추론이나 사실적 정합성 부족 → hallucination 현상.
  * 컴퓨트와 환경 비용 → 지나치게 큰 자원 소모.

### Recap

이 논문은 **GPT-3**를 통해 “대규모 언어 모델이 사전 학습만으로 범용적 능력을 획득한다”는 사실을 보여주었다.
핵심 발견은 **in-context learning**으로, 프롬프트에 예시를 몇 개만 주어도 모델이 새로운 작업을 수행할 수 있다는 점이다.
이는 기존의 fine-tuning 패러다임에서 **prompt-based 학습 패러다임**으로의 전환을 이끌었고, 이후 ChatGPT와 같은 대화형 모델 개발로 이어졌다.

---

지금까지 리뷰한 4편을 시간 순서로 연결하면 다음과 같은 맥락이 보입니다:

1. **Scaling Laws for Neural Language Models (Kaplan et al., 2020)**
   → 성능과 자원(파라미터, 데이터, 컴퓨트)의 관계가 파워 법칙을 따른다는 최초의 발견.

2. **Scaling Laws for Autoregressive Generative Models (Henighan et al., 2020)**
   → 이 법칙이 언어 모델에 국한되지 않고, 오토리그레시브 생성 모델 전반에 보편적으로 성립함을 입증.

3. **Language Models are Few-Shot Learners (Brown et al., 2020)**
   → 초거대 모델(GPT-3)이 등장하면서, 단순 scaling만으로도 새로운 학습 패러다임(in-context learning)이 가능해짐을 증명.

4. **Training Compute-Optimal Large Language Models (Hoffmann et al., 2022, Chinchilla)**
   → Kaplan 법칙의 한계를 수정하고, compute-optimal 분배 전략을 통해 효율적으로 성능을 끌어올리는 방법 제시.
