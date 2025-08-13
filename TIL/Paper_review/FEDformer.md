## FEDformer: Frequency Enhanced Decomposed Transformer for Long-term Series Forecasting

#### 2025-08-13

### Problem Statement

* 기존 **Transformer 기반 시계열 예측 모델** 들은 긴 시퀀스를 처리할 때 연산 복잡도와 메모리 사용량이 매우 크며, 복잡한 패턴을 효율적으로 모델링하기 어렵다.
* **Self-Attention** 이 시간 영역 (time domain) 에서만 작동하여, **주기적 (periodic)**·**계절적 (seasonal) 패턴** 을 효과적으로 추출하지 못하는 문제가 존재한다.
* 단순한 **데이터 차분 (differencing)** 이나 **이동평균 (moving average)** 기반의 추세 제거는 비선형 시계열에서 성능이 제한적이다.

### Solution Approach

* 시계열을 **추세 (trend)** 와 **잔차 (residual, seasonal)** 로 분해하는 **시계열 분해 (time-series decomposition)** 를 Transformer 구조에 통합하여 복잡성을 줄이고 예측 성능을 향상.
* 잔차 (계절 성분) 에 대해 **주파수 영역 (frequency domain)** 에서의 **Auto-Correlation** 기반 Attention을 적용, **장기 의존성 (long-term dependency)** 을 효율적으로 학습.
* 추세 성분은 단순하고 효율적인 **저차원 다항 회귀 기반 예측 모듈** 을 사용하여 계산량을 최소화.

### Methodology Details

1. **Time-series Decomposition**

   * 입력 시계열을 **추세 성분** 과 **잔차 성분** 으로 분리.
   * **추세 성분**: 저차원 **다항 회귀 (Polynomial Trend)** 로 단순 예측.
   * **잔차 성분**: Transformer 기반 모델에 입력하여 복잡한 **주기/계절 패턴** 학습.

2. **Frequency Enhanced Attention (Auto-Correlation Mechanism)**

   * 잔차 시계열을 **FFT (Fast Fourier Transform)** 로 주파수 영역으로 변환.
   * 주파수 영역에서 **자기상관 (Auto-Correlation)** 기반 **Top-k 지연 (lag)** 값을 선택하여 패턴 반복성을 효율적으로 학습.
   * 이렇게 하면 시간 영역에서의 **O(L²)** 연산을 줄이고, **장기 시계열 패턴** 을 효과적으로 포착.

3. **Encoder-Decoder 구조**

   * **Encoder**: 잔차 시계열의 **주기적 패턴** 을 Auto-Correlation 기반 Attention으로 학습.
   * **Decoder**: 예측 대상 구간의 시계열을 디코딩하면서, 예측 시점별 **주파수-시간 패턴** 을 복원.
   * 최종 출력: **추세 예측** + **잔차 예측** 의 합으로 최종 결과 생성.

4. **복잡도 감소**

   * Auto-Correlation 기반 Attention은 전체 길이의 모든 위치 쌍을 계산하지 않고, **주기성 높은 지연 위치** 만 선택하므로 **연산량** 과 **메모리 사용량** 이 크게 줄어듦.

### Recap

FEDformer는 시계열 데이터를 **추세** 와 **계절/주기 성분** 으로 분해하여 각각 다른 방식으로 처리하는 **Transformer 기반 예측 모델** 이다.
**추세** 는 단순 회귀로 빠르게 예측하고, **계절 성분** 은 **주파수 영역** 에서 **Auto-Correlation 기반 Attention** 으로 학습하여 **장기 의존성** 과 **주기성** 을 효율적으로 포착한다.
이를 통해 기존 Transformer의 **계산 복잡도** 를 줄이고, 긴 시계열 예측에서 높은 성능을 달성한다.

**한계점** 으로는 비주기적이고 불규칙한 변동이 강한 시계열에서는 **주파수 기반 방식** 의 효과가 떨어질 수 있으며, 계절성이 불분명한 데이터에서는 **Auto-Correlation 선택** 이 부정확해질 수 있다.
