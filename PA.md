# FFT-Mamba2 기반의 rPPG 모델 설계

## 📌 1. 개요 및 목적

본 모델은 **FFT**를 활용한 주파수 도메인 특징 추출과 **Mamba2**를 기반으로 한 상태 공간 모델링을 결합하여, 기존 모델 대비 정확하고 효율적인 rPPG 신호 추정 및 심박수(HR) 예측을 목표로 한다.

본 연구는 아래 논문의 핵심 구조를 바탕으로 한다:

- (가) 논문: FFT-Mamba를 통한 Lung Parenchyma segmentation 및 Radiomics 특징 추출 (FFT 도메인, Hi-Mamba 구조)
- (나) 논문: PhysMamba를 통한 원격 생체 신호 측정 및 상태 공간 이중성(State Space Duality) 적용

---

## 📌 2. 모델 전체 아키텍처

**입력 데이터:** `(T, C, H, W)` 얼굴 영상
- `T`: 시간 프레임
- `C`: 채널(RGB)
- `H, W`: 높이, 너비

### 전체 흐름

```
입력 영상 (T, C, H, W)
│
├── [A] 전처리 (영상 안정화, 피부영역 추출, 조명 정규화)
│
├── [B] RoI 선정 및 공간 어텐션 기반 가중 평균화
│     ├── 시공간 스트림(Time-stream: Mamba2 기반, VSS_B 구조)
│     └── 주파수 스트림(Frequency-stream: FFT 기반, FFT_B 구조)
│
├── [C] Cross-Mamba 게이팅 상호작용
│
├── [D] Persistent Memory (Titans 기반)
│
└── [E] 최종 rPPG 신호 예측 및 심박수 추정
```

---

## 📌 3. 세부 구성

### ▶️ [A] 영상 전처리
- **얼굴 정합(Face Alignment)**: MediaPipe Anchor 기반 Affine 변환
- **피부 영역 추출**: DNN 기반 피부 마스크 적용
- **조명/피부색 보정**: YUV 변환 (CHROM 방식) 및 CLAHE 적용

### ▶️ [B] 이중 스트림 모듈 (Dual-stream)

#### ⏩ RoI 공간 가중화
- Attention-weighted pooling:
```
Input(T,C,H,W) → Conv → Sigmoid → Spatial Attention(T,1,H,W) → Weighted Pooling(T,C,1,1)
```

#### ⏩ 시공간 스트림 (Time-stream)
- 구성:
```
Weighted Input(T,C,1,1) → Conv(Temporal Embedding) → LayerNorm → Mamba2 (SSD)
```
- 특징: 상태 공간 이중성(SSD) 및 Temporal Difference Mamba

#### ⏩ 주파수 스트림 (Frequency-stream)
- 구성:
```
Weighted Input(T,C,1,1) → FFT(Temporal) → 1D-Conv → Mamba2
```
- 특징: 주파수대역 제한(0.7~4Hz)으로 HR 신호 집중 학습

### ▶️ [C] Cross-Mamba 게이팅
- 구조:
```
Gate = sigmoid(W₁·Time-stream + W₂·Freq-stream)
Output = Gate × Time-stream + (1−Gate) × Freq-stream
```
- 특징: 간소화된 효율적 결합

### ▶️ [D] Persistent Memory
- Titans 논문의 개인화 및 자기지도 학습 메모리 적용
- 개인별 메모리를 Mamba2 Hidden State에 Plug & Play 통합
- Test-time Adaptation 가능

### ▶️ [E] 최종 rPPG 신호 및 HR 추정
- Output → 1D Conv + Linear Projection → rPPG 신호 생성
- 심박수 추정: Peak Detection 또는 FFT 기반 분석

---

## 📌 4. 최종 모듈 정리

| 모듈                | 역할                     | 출처 논문              | 차별화 요소                              |
|-------------------|------------------------|---------------------|-----------------------------------|
| [A] 전처리          | 노이즈 제거, 안정화           | PhysMamba(나)         | 피부 세그먼트, 영상 정합 강화                 |
| [B] Dual Stream   | 시공간/주파수 정보 동시 학습   | FFT-Mamba(가), PhysMamba(나) | Weighted Pooling, Temporal diff. Mamba2 |
| [C] Cross-Mamba   | 스트림 간 결합               | FFT-Mamba(가)         | Gated Fusion 단순화                    |
| [D] Persistent Memory | 개인화 / 자기지도학습        | Titans               | Plug & Play 메모리 통합                 |
| [E] 최종 신호 추정    | rPPG 생성 및 HR 추정        | PhysMamba(나)         | 1D Conv + Linear Projection        |

---

## ✨ 기대효과

- FFT와 Mamba2의 상호보완으로 정밀한 rPPG 예측
- Titans 메모리 모듈을 통한 개인 맞춤화 및 자기지도 최적화
- 의료 및 헬스케어 분야 적용성 강화

