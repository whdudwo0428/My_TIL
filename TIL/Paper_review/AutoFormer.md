## Autoformer: Decomposition Transformers with Auto-Correlation for Long-Term Series Forecasting

#### 2025-08-13

### Problem Statement

* 기존 Transformer 계열 시계열 예측 모델은 긴 시계열 입력에 대해 **자원 소모가 크고**(O(L²) self-attention), 시계열의 **장기 주기성**과 **추세**를 효과적으로 분리·활용하지 못함.
* Multi-head attention이 시계열의 **패턴 반복 구조**를 잘 포착하지 못하고, 예측 시 길이가 길어질수록 누적 오차와 성능 저하가 발생.
* 특히 장기 예측에서는 **노이즈 제거**, **추세·계절 성분 분리**, **반복 패턴 추출**이 중요한데 기존 구조에서는 이를 명시적으로 처리하지 않음.

### Solution Approach

* 시계열을 **추세**와 **잔차**로 분해하는 **시계열 분해 모듈**을 Transformer 내부에 통합.
* Self-attention 대신, 시계열의 **시간 지연 상관**을 직접 모델링하는 **Auto-Correlation 메커니즘**을 제안해 주기성을 효율적으로 학습.
* 예측 과정에서 Auto-Correlation 기반 attention은 상관성이 높은 지연 시점을 식별하고 이를 반복적으로 복사·합성하여 미래를 예측.

### Methodology Details

1. **Series Decomposition Block**

   * 입력 시계열을 이동 평균 기반 필터로 **추세 성분**과 **잔차 성분**으로 분리.
   * 추세 성분은 장기 변화를, 잔차 성분은 주기적 패턴과 단기 변동을 반영.
   * 각 블록의 입력과 출력을 모두 분해·갱신하여 깊은 네트워크에서 누적되는 노이즈를 줄임.

2. **Auto-Correlation Mechanism**

   * 기존 self-attention에서 Q·K 내적 기반 유사도 대신, **주기적 지연과의 상관도**를 계산.
   * \*\*FFT(Fast Fourier Transform)\*\*를 사용하여 주파수 영역에서 상관 피크 위치를 탐색하고, 그 지연 시점의 값을 반복 복사해 예측.
   * 장기 패턴을 효율적으로 재사용하면서도 계산 복잡도를 줄임.

3. **Decoder with Progressive Prediction**

   * Decoder는 예측 결과를 한 번에 생성하는 대신, **추세**와 **잔차**를 각각 예측 후 합성.
   * Auto-Correlation은 잔차 패턴을 복사하고, 추세는 선형 확장 방식으로 처리.

4. **Complexity & Efficiency**

   * Auto-Correlation 연산은 FFT 기반으로 **O(L log L)** 복잡도를 가지며, 기존 self-attention(O(L²))보다 효율적.
   * 긴 시퀀스에서도 GPU 메모리 사용량을 크게 줄임.

### Recap

Autoformer는 장기 시계열 예측에서 발생하는 **장기 패턴 포착 문제**와 **자원 비효율성**을 해결하기 위해,

1. **Series decomposition**으로 추세와 계절 성분을 분리,
2. **Auto-Correlation mechanism**으로 반복 패턴을 직접 추출·복사하여 미래를 예측,
3. **FFT 기반 계산**으로 효율성을 높였다.

이 구조는 Transformer 기반 장기 예측 모델 중 **계절·주기성 데이터에 특히 강점**을 가지며, 여러 벤치마크에서 SOTA 성능을 달성했다.

**한계**

* 비주기적·불규칙 변동이 큰 데이터에서는 Auto-Correlation의 효과가 제한될 수 있음.
* 분해 과정에서 이동 평균 윈도우 크기 설정이 성능에 큰 영향을 미침.
