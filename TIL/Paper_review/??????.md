## FFT-Mamba-guided Lung Parenchyma Segmentation and Radiomics Representation for COPD Staging Diagnosis  
#### 2025-04-11

### Problem Statement  
- 만성 폐쇄성 폐질환 (Chronic Obstructive Pulmonary Disease, COPD)은 폐 기능 저하로 인해 호흡이 점진적으로 어려워지는 질병이다. 기존의 폐기능 검사 (Pulmonary Function Test, PFT)는 정확도가 제한적이며 환자의 협조가 필수적이어서, 정확하면서 비침습적인 COPD 진단과 병기(stage) 구분이 가능한 자동화된 기술이 요구된다.

### Solution Approach  
- 논문은 **FFT-Mamba** 기반 딥러닝 기법을 이용해 CT 영상에서 폐 실질(lung parenchyma)을 정밀하게 분할(segmentation)하고, 분할된 영역에서 라디오믹스(radiomics) 특징을 추출하여 COPD 병기 진단의 정확성을 높인다.

### Methodology Details  
- **FFT-Mamba를 활용한 폐 실질 분할**  
  - 폐 실질 영역의 정밀한 분할을 위해 Fourier 변환 기반의 주파수 도메인 특징과 최근의 구조화 상태 공간 모델인 Mamba를 결합한 하이브리드 세그멘테이션 기법을 사용하였다.
  - FFT (Fast Fourier Transform)를 통해 영상의 주파수 영역 특징을 추출한 후, 이를 Mamba의 구조적 상태 공간(Structured State Space) 모델을 통해 시공간적 정보를 효과적으로 처리하도록 설계하였다.
  
- **라디오믹스 특징 추출 (Radiomics Representation)**  
  - 분할된 폐 실질 영역에서 폐 조직의 구조적 및 기능적 상태를 반영하는 라디오믹스 특징을 정량적으로 추출하였다.  
  - 텍스처(texture), 형태(shape), 강도(intensity)와 관련된 특징들이 포함되며, 이는 COPD의 병기 판별에 필수적이다.
  
- **기계학습 기반의 COPD 병기 진단**  
  - 추출된 라디오믹스 특징을 기계학습 분류기(classifier)에 입력하여, 글로벌 COPD 병기 가이드라인인 GOLD (Global Initiative for Chronic Obstructive Lung Disease) 기준에 따라 환자의 병기를 자동으로 구분하였다.
  - 다양한 기계학습 모델을 비교 평가하여 최적의 분류 성능을 보이는 모델을 선정하였다.

### Recap  
본 논문은 COPD의 자동 진단 및 병기 판정을 위해 **FFT-Mamba**를 활용하여 폐 실질을 정밀하게 분할하고, 추출된 라디오믹스 특징으로부터 기계학습을 통해 COPD 병기를 정확히 예측하는 방식을 제안하였다. 이는 기존의 침습적이고 제한적인 폐기능 검사법을 보완할 수 있는 효과적인 자동화 진단 기술로 평가될 수 있다.

### 한계점 및 개선 가능성  
- 아직 실험 데이터의 규모가 상대적으로 작아 추가적인 대규모 임상 검증이 필요하다.
- 다른 호흡기 질환과의 차별성을 검증할 필요가 있다.
- 실제 임상 환경에서의 활용 가능성을 평가하기 위한 추가 연구가 요구된다.
