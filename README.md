## 2025-01-11

### 강화학습 이론과 알고리즘 공부
- 파이썬으로 간단한 GridWorld를 만들고 경로 최적화 문제 실습
- Q-Learning과 SARSA 구현
- ε-탐욕 정책, Q-테이블 학습, 업데이트 공식, 강화학습 내 하이퍼파라미터 전반 이해

---

## 2025-01-12

### 자율주행 센서 기술 및 로드맵 탐색
- 전날 내용 이어서 이것저것 탐색 (특히 Lidar, Camera 중심)
- 추천 논문 몇 개 간단히 요약해 읽어봄
- 아직 이해는 어렵지만, 프로젝트 전 최대한 사전지식 채우기 위한 로드맵 구성 시도

---

## 2025-01-13

### 포트폴리오 구성 및 Git 활용 연습
- TIL, Project 정리 등 포트폴리오 준비 구성
- Git 사용법 공부
- GELU, ADAS, 레이더 도플러효과, 허프변환 등 다양한 주제 서칭하고 정리
- 자율주행 관련 기술들을 A to Z 정리

---

## 2025-01-14

### SLAM & LiDAR 기반 인지 메커니즘 공부
- SLAM과 3D Mapping 개념 간단히 훑어봄
- 시각 정보 인지 메커니즘 공부 (눈의 구조, 시각 수용체, 스펙트럼별 인지 등)
- LiDAR의 원리 및 발전사 깊게 공부  
  - Solid-State LiDAR, ToF-FMCW 신호처리와 통신 원리
  - 수학적 이론, 응용 분야, 산업 트렌드까지 폭넓게 탐구

---

## 2025-01-15

### 자율주행 산업 및 Git 구조 공부
- 테슬라 FSD의 라이센싱 비즈니스 모델과 end-to-end 구조 탐색
- GNSS(GPS) 원리와 자율주행에서의 활용성 탐구
- Git을 너무 못 쓰는 것 같아서 시간 들여 학습
- 여러 자료를 봤는데 구체적으로 기억은 잘 안 나지만 통신/수학 관련 공부도 많이 했던 듯

---

## 2025-01-16

- None...

---

## 2025-01-17

### Project 1: DiabetesPrediction 기획
- Project1 구조 및 baseline 코드 작성
- 프로젝트 목적에 따라 다양한 ML 모델들 탐색

---

## 2025-01-18

### Project 1, 2 본격 시작
- [Project1.DiabetesPrediction](https://github.com/whdudwo0428/MyProjects/tree/main/DiabetesPrediction)  
  - 모델 경량화, 효율성 확보를 위한 방법론 탐색  
  - Logging 등 학습 기록 모듈 공부  
  - README 정리하며 Git tool 이해도 향상 시도

- Project2.ChessPiece Detection  
  - 모델 선별 및 구조 설계  
  - Git, Roboflow에서 코드/모델/데이터 불러오는 방법 익힘  
  - YOLO 구조 간단히 이해

---

## 2025-01-19

### Project 2 완료 및 성찰
- [Project2.ChessPiece Detection](https://github.com/whdudwo0428/MyProjects/tree/main/ChessPiece%20Detection) 완료  
  - Git이나 PyTorch 기반 프로젝트 구성을 익히는 게 목적이었지만, 알고리즘, 코드, 파일 구조 등은 깊이 이해하지 못한 채 따라간 느낌  
  - 그래서 잠시 프로젝트를 멈추고 detection 관련 공부를 충분히 한 뒤 Project3로 넘어가기로 결정

- FPN, UNet 등 segmentation 모델  
  - 초기 모델부터 발전 과정까지의 흐름과 논리를 중심으로 탐구

---

## 2025-01-20

### 팀 프로젝트 구상 및 모델 탐색
- 자동 모자이크 처리 프로그램 + 웹페이지 개발을 위한 모델 조사
  - 다양한 모델 서칭 (YOLO 버전별 차이 포함)
  - 데이터 전처리 방식, 데이터셋-모델-코드 간 구조 파악에 시간 투자
  - OpenCV 기반 blur 처리 알고리즘 공부 및 과거 baseline 코드 복습

---

## 2025-01-21

### Project 3 설계 및 논문 읽기 시작
- Project3.Detection_Soccer 구조 설계 및 모델 후보 리스트업
  - 다양한 Object Detection 모델 정리 및 비교
- 논문 리뷰 로드맵 설계  
  - 참고 Git: [deep_learning_object_detection](https://github.com/hoya012/deep_learning_object_detection)
- Paper Review : DETR (End-to-End Object Detection with Transformers)

---

## 2025-01-22

### Object Detection 성능 평가 Metric 탐색
- mAP를 포함한 다양한 평가 지표 탐구  
- 향후 다양한 Metric 추가 학습 예정

- Paper Review : DETR (End-to-End Object Detection with Transformers)
- Paper Review : R-CNN (Rich feature hierarchies for accurate object detection and semantic segmentation)

---

## 2025-01-23

### CNN 구조 및 객체 탐지 프레임워크 이해도 향상
- Paper Review : OverFeat (Integrated Recognition, Localization and Detection using Convolutional Networks)
- CNN 동작 원리 깊게 탐구 (Padding, Stride, Pooling, 각 Layer 내 연산 등)
- 지금까지 정리한 TIL 내용 다시 읽고 복습
- OverFeat 기반으로 Two-Stage Detector → One-Stage Detector로의 전환 개념 이해
- Paper Review : Fast R-CNN (Fast Region-based Convolutional Networks for Object Detection)

---

## 2025-01-24

- Paper Review : Faster R-CNN (Towards Real-Time Object Detection with Region Proposal Networks)
- Paper Review : OHEM (Training Region-based Object Detectors with Online Hard Example Mining)

---

## 2025-01-25

- Paper Review : YOLO v1 (You Only Look Once: Unified, Real-Time Object Detection)
- Paper Review : SSD (Single Shot MultiBox Detector)

---

## 2025-01-26

- Paper Review : R-FCN (Object Detection via Region-based Fully Convolutional Networks)
- Paper Review : YOLO v2 (YOLO9000: Better, Faster, Stronger)

---

## 2025-01-27 ~ 01.28

- Paper Review : FPN (Feature Pyramid Networks for Object Detection)
- FPN이 새로운 개념이라기보단 기존 모델을 잘 조합해 성능을 올린 구조라는 점에서, 오히려 내가 뭘 알고 모르고 있는지를 분명하게 알 수 있었음  
- 이 기회에 시간을 좀 더 써서 예전 모델들을 복습하고, 기본 개념들을 내 것으로 만드는 데 집중했음  
- CNN 내 다양한 Layer 원리 (fc, conv, Reorg, Residual Connection 등)와 구조적 개념 (Bottom-up, Top-down Pathway, Lateral Connection) 학습  
- K-means Clustering 공부하며 예전 논문 리뷰에서 다뤘던 수학 개념들 (지시 함수, 특이값 분해, 이중 합산 등) 복습  
- P.S. FPN 공부하며 다시 예전 논문들도 돌아가서 참고하게 되었고, 이제 슬슬 객체 탐지 모델 흐름이 어느 정도 들리는 느낌 받음

---

## 2025-01-29 ~ 01.30

- Paper Review : RetinaNet (Focal Loss for Dense Object Detection)
- Paper Review : Mask R-CNN (Mask R-CNN)

---

## 2025-01-31

- Paper Review : YOLO v3 (YOLOv3: An Incremental Improvement)
- Paper Review : RefineDet (Single-Shot Refinement Neural Network for Object Detection)
  - ARM과 ODM의 개별 역할은 명확했지만, ODM에서 각 스케일 정보를 어떻게 최종적으로 통합하는지는 애매했음  
  - Multi-scale Feature에서 가져온 prediction을 어떻게 결합하는지, Bounding Box Regression 과정이 명확하지 않아 직접 코드를 Scratch해서 파악 필요  
  - 논문 자체가 조금 불친절했지만, 지금까지의 base 모델 개념들이 도움이 되며 ‘이건 어디서 가져온 개념이네’, ‘이 구성은 문제 있었는데 어떻게 해결했더라?’ 같은 생각이 들면서 insight를 얻게 됨  
  - 특히 FPN 리뷰할 때처럼 객체탐지 모델에 대한 나만의 관점이 조금 생긴 느낌
- Paper Review : M2Det (A Single-Shot Object Detector based on Multi-Level Feature Pyramid Network)

---
```markdown
## 2025-02-01 ~ 02.02

- Paper Review : YOLO v4 (YOLOv4: Optimal Speed and Accuracy of Object Detection)  
  - YOLOv4는 새로운 개념과 기법이 너무 많이 나와서 처음 YOLOv1~3을 봤을 때보다 더 복잡하고 어려운 느낌이었음  
  - 특히 BoS, BoF, CSPDarknet53, PANet, CIoU, Mish activation, Mosaic augmentation 등 새로운 개념들을 접하며 처음 보는 단어와 구조가 너무 많아 막막했음  
  - 논문 하나를 이해하기 위해 다양한 네트워크 구성 요소와 성능 향상 요소들을 체계적으로 공부해야겠다고 느낌

- 논문 읽을 때 자주 나오는 영어 형용사, 동사, 고유명사들 정리

- 다양한 Data Augmentation 기법들의 수학적 원리 이해  
  - OpenCV 기반 코드 분석하며 실제 구현까지 확인  
  - RGB 채널 중심으로 image processing 개념 깊게 탐구  
  - 예전에 그냥 넘어갔던 channel 개념을 이제야 체계적으로 이해함

- 자연스럽게 생성 모델(Generative Model) 관련 흐름으로 연결됨  
  - 앞으로 object detection, segmentation 이후에 이쪽도 프로젝트 해보고 싶음

- Paper Review : VQ-VAE (Neural Discrete Representation Learning)  
  - Flow based model 구조, 역함수 접근과 loss 이해  
  - Encoder-Decoder 구조를 이전보다 훨씬 깊게 이해함  
  - AE, Scalar/Vector Quantization 등의 하위 개념부터 정리  
  - 아직도 discretization과 Scalar Quantization 차이가 명확히 납득되진 않음  
  - Residual VQ 포함

- Paper Review : Neural ODE (Neural Ordinary Differential Equations)  
  - ODE 기초부터 Neural 방식의 수치적 접근까지 학습  
  - 관련 코드까지 보며 구현 방식 이해  
  - 이전에 공부했던 Loss 구조도 같이 복습하게 되었고, 수학 공부를 꽤 많이 함  
  - ODE Solver 관련 내용도 정리

- Python에서 `__init__` 같은 파일 구조 관련 기술들 보긴 했는데... 졸려서 거의 흘려봄. 5번째 프로젝트쯤에 다시 제대로 보기로.

- Diffusion Model(DDPM)도 잠깐 봤지만 아직 완전히 모르겠음  
  - 나중에 GAN 개념 확실히 잡고 나서 다시 돌아와야 할 듯  
  - 선행 개념 정리:
    - (Continuous) Stochastic Process
    - Markov Process
    - SDE(확률 미분 방정식)
    - Noise Schedule / Variance Schedule
    - VAE, GAN 같은 기반 개념

---

## 2025-02-03

- 2월 1~2일 공부 내용 복습
- CNN 기본기 추가 학습 (앞으로도 지속적으로 다질 계획)
- 세미나 주제로 3D Object Detection 관련 논문들 서칭
  - 추천 논문 리스트 및 로드맵 정리
  - 3D Point Cloud, LiDAR, Voxel Grid, 3D Object Detection 등의 기초 개념들 정리
  - 무엇을 찾아보고 있는지를 항상 정리하는 습관을 들이기로 다짐

---

## 2025-02-04

- Paper Review : VoxelNet (End-to-End Learning for Point Cloud Based 3D Object Detection)  
  - 하루 종일 세미나 준비만 함  
  - Architecture, 아이디어, 주변 필요 지식들을 전반적으로 공부  
  - 3일부터 5일까지 밤 새서 준비함

---

## 2025-02-05

- Paper Review : VoxelNet (세미나 발표 진행)  
  - 세미나 준비 시간이 2일로 짧았지만, 내용 구성 자체는 만족스럽게 마무리  
  - 발표 시간이 갑자기 앞당겨져서 script를 준비 못 했는데도, 내가 이해하고 공부한 내용을 70% 정도는 설명할 수 있었던 것 같음  
  - 첫 세미나라 많이 떨렸지만, 주변에서 발표 잘했다는 말 들어서 기분 좋았고, 레벨업한 느낌도 있었음  
  - PPT 완성도는 낮았지만, 다음에는 더 잘 준비할 수 있을 것 같다는 자신감 생김  
  - 발표 중 부족했던 개념들 정리 → 2월 10일까지 하루에 하나씩 공부할 예정:
    - Receptive field, ~wise operations, Skip Connection, concat  
    - Aggregation methods, feature extraction techniques, Point Density variance imbalance  
  - Sparse 4D Tensor 설명할 때 데이터 차원 개념이 부족하다는 걸 느낌  
    → 자료구조, 알고리즘 이후 이 부분도 공부할 키워드 정리 (2월 8~9일 계획)

---

## 2025-02-06

- CNN 기본기 복습
- 해상도(resolution)에 대한 이론 전반 정리
- Receptive field, Dilated/Atrous Convolution, Segmentation 한 번에 정리  
- Paper Review : Dilated Convolution (Multi-Scale Context Aggregation by Dilated Convolutions)
- Skip Connection 개념 정리
- 미국 가기 전, 내가 지금까지 공부한 내용을 종합적으로 정리하고 체득하는 시간 필요하다고 느낌

---

## 2025-02-07

- 영단어 정리 (Vocabulary.md)
- Skip Connection → ResNet으로 이어서 정리
- Paper Review : ResNet (Deep Residual Learning for Image Recognition)
- Lab 서칭, CV, contact email 초안 피드백 받음

---

## 2025-02-08

- Detect-seg-blur 프로젝트용 적절한 데이터 탐색
- 연구실 contact email 초안 완성 후 교수님별로 튜닝

---

## 2025-02-09

- Contact Email 전송: 한양대 데이터사이언스 Casey Bennett 교수님
- Aggregation methods / Ensemble Learning 정리
  - Boosting, Bagging, Bootstrap
- Feature Extraction Techniques 정리
  - Vision: SIFT, HOG, LBP
  - NLP: TF-IDF, Word2Vec, GloVe
  - Speech: MFCC, Chroma Features, PCA
  - 향후 후각 특징 추출 관련도 추가 공부 예정

---

## 2025-02-10

- 연구실 서칭 및 석박사 통합 과정으로 진지하게 준비하기로 결심
- 미국에서 공부할 것들 정리
- Transformer 학습 로드맵 수립: LNP → Transformer → NLP/Vision 기반 확장
  - cosine similarity, SVD, KL Divergence, Bayes' theorem 개념 정리
  - Transformer 관련 블로그 리뷰하며 막히는 부분 체크
  - NLP 교재 진도 시작 (데이터 전처리, 언어 모델, BoW, TF-IDF 등)
- Project4. PDF → LDA 변환 진행

```
 
- **2월 11일~18일 : 미국견학**
  - [NPL 교재](https://wikidocs.net/21694)
    - Chapter 02. 데이터 전처리
      - Chapter 03. 언어모델 종류 / 확률 기반 모델
        - Chapter 04. 카운트 기반 모델
        - Chapter 05. 벡터 유사도
        - Chapter 06. 머신러닝 기본 복슴
        - Chapter 07. 딥러닝 기본 복습
        - Chapter 08. RNN base
        - Chapter 09. Word embedding
        - Chapter 10. NLP 실습 / 다양한 task별 구현 논리
    - 시카고 듀플대학 석사 연구실 컨택 => 영어공부 시작해보자... 목표 토플 80점
        - 초등영단어1 700
        - 초등영단어2 800
        - 중학 영단어 1000 : 1~600
          
         
- **2월 19일**
    - 남은 2월동안 영어단어만 공부!
    - 밀린 한국 일정들 처리하느라 바쁠 예정...
    - 중학 영단어 1000 : 600~1000
         
- **2월 20일**
    - 중학 영단어 1000 복습
    - 중등 수능필수영단어 1800 : 240개
         
- **2월 21일 ~ 2월 25일**
    - [영어어원 블로그](https://m.blog.naver.com/PostList.naver?blogId=eternity9us&categoryNo=29&logCode=0&tab=1) : 잘 안외워지는 단어는 여기서 확인, 심심할때마다 들려서 쭉 읽기
    - 중등 수능필수영단어 1800 : 매일 복습하고 진도 반복

- **2월 26일 ~ 3월 3일**
    - Word Master 고등 Basic: 매일 복습하고 진도 반복
    - 품사파생어도 다 같이 외우고, 모든 예문 자연스럽게 읽힐 때까지 끊어읽기 연습
 
- **3월 4일 ~ 3월 12일** : **논문준비, 5월 SCI 목표**
    - Word Master 고등 Basic : Day 1~25 반복
    - Mamba Preliminary!
        - HiPPO ~ Mamba까지 쉬운 수준에서 "이런 이런 기능을 갖기위해 모델을 이렇게 구성하고 대충 이런 논문이다" 같은 러프한 수준에서는 납득하고 넘어가겠는데, 구체적으로 아키텍쳐나 수식 하나하나를 뜯어보며 이해하려고 하는 순간 그 구조의 논리적 전개가 안됨. 아직 이걸 읽을 레벨이 아니란 느낌 생각보다 Mamba 모델을 대략적으로도 이해하는 것 자체가 꽤 오래 걸릴것같음... 기간 신경쓰지말고, 시간 충분히 두고 하위 개념 하나하나 익숙해지면서(비젼논문 처음 읽었던것처럼) step by step 으로 해보자...
        - rPPG, Self Attention, Transformer, Hippo, SSM, LSSL, S4, H4, Mamba, PhysMamba 까지 전체적인 논리와 관련개념, 세부적인 내용 등을 공부하고 정리함.
        - [HiPPO 논문](https://arxiv.org/pdf/2008.07669)  공부
        - [LSSL 논문](https://arxiv.org/pdf/2008.07669)  공부
        - [S4 + S4(D) 논문](https://arxiv.org/pdf/2111.00396)  공부
        - [H3 논문](https://arxiv.org/pdf/2212.14052) 공부
        - [Mamba 논문](https://arxiv.org/pdf/2312.00752) 간단하게 읽어봄 / [참고 블로그 1](https://kyujinpy.tistory.com/149)
        - [Mamba 참고 유튜브 1](https://www.youtube.com/watch?v=JjxBNBzDbNk) : 해당 유튜브를 바탕으로 노트정리!
    -  Adaptive Kernel, 동적 SSM filter 추가로 공부하기
    -  Mamba 공부
    
    
 - **3월 13일 ~ 3월 16일** 
    - Word Master 고등 Basic : 13~30 계속 반복

- **3월 17일 ~ 3월 27일** 
    - 수업시간 : Word Master 고등 Basic : 26~30 계속 반복
    - 근로시간 : English Grammar in USE : (18일 화요일 시작) / 동사 시제별로 암기해두기
    - [Mamba 논문](https://arxiv.org/pdf/2312.00752) review 세미나 (2025-03-27 2차 세미나까지 완료)
 
- **3월 28일 ~ 4월 3일**
    - 토익기출 VOCA 영단어 암기 : Day 1~10
    - [Mamba code 구현](https://github.com/state-spaces/mamba) 공부
    - rPPG 기본 공부
    - [Physmamba 1 논문](https://arxiv.org/pdf/2409.12031) review : Mamba-1 기반 PhysMamba
    - [Physmamba 2 논문](https://arxiv.org/pdf/2408.01077) review : Mamba-2 기반 PhysMamba

- **4월 4일**
    - 토익기출 VOCA 영단어 암기 : Day 1~5 복습
    - Transformer 공부 제대로 하기
    - [Bahdanau Attention 논문](https://arxiv.org/pdf/1409.0473) review
    - [Luong Attention 논문](https://arxiv.org/pdf/1508.04025) review

 - **4월 5일**
    - 토익기출 VOCA 영단어 암기 : Day 5 복습
    - [Attention Is All You Need 논문](https://arxiv.org/pdf/1706.03762) review
        - [Positional Encoding 참고 블로그](https://www.blossominkyung.com/deeplearning/transfomer-positional-encoding)
        - [Transformer Code 실습](https://github.com/ndb796/Deep-Learning-Paper-Review-and-Practice/blob/master/code_practices/Attention_is_All_You_Need_Tutorial_(German_English).ipynb)
    - Paper Review : [Simplified State Space Layers for Sequence Modeling](https://arxiv.org/pdf/2208.04933)
    - Titans preview !!!
      
 - **4월 6일**
    - 토익기출 VOCA 영단어 암기 : Day 6~& 복습
    - Paper Review : [Learning to (Learn at Test Time): RNNs with Expressive Hidden States](https://arxiv.org/pdf/2407.04620)
    - Paper Review : [Test-Time Training with Self-Supervision for Generalization under Distribution Shifts](https://arxiv.org/pdf/1909.13231)
        - 정독 : Test-Time Momory update 개념 확실하게! self-supervision + online adaptation 구조 파악
    - Paper Review : [Memorizing Transformers](https://arxiv.org/pdf/2203.08913)
        - 정독 : Titans의 memory 메커니즘이 기존 external memory 방식과 어떻게 다른지를 파악, recall/retrieval 구조 참고용
    - Paper Review : [Retentive Network: A Successor to Transformer for Large Language Models](https://arxiv.org/pdf/2307.08621)
        - 구조만 정리 요약위주 : attention-free memory retention 구조
    - **Paper Review** : [Transformers are SSMs: Generalized Models and Efficient Algorithms Through Structured State Space Duality](https://arxiv.org/pdf/2405.21060)
    - Paper Review : [MoE-Mamba: Efficient Selective State Space Models with Mixture of Experts](https://arxiv.org/pdf/2401.04081)
    - **Paper Review** : [Titans: Learning to Memorize at Test Time](https://arxiv.org/pdf/2501.00663)
    - Paper Review : [Using Fast Weights to Attend to the Recent Past](https://arxiv.org/pdf/1610.06258)
        - fast memory writing 개념만 요약


    - [Physmamba code 구현](https://github.com/ubicomplab/rPPG-Toolbox/blob/main/neural_methods/model/PhysMamba.py) 공부


-----
- [Physmamba 논문](https://arxiv.org/pdf/2409.12031) review
        - [Baseline code](https://github.com/ubicomplab/rPPG-Toolbox/blob/main/neural_methods/model/PhysMamba.py)
        - [Titans 논문](https://arxiv.org/pdf/2501.00663) review


  
#### **NLP => tranformer 공부 순서 **
- 단어 임베딩 (Word Embedding)
  - [Word2Vec (2013)](https://arxiv.org/pdf/1301.3781)
  - [GloVe (2014)](https://arxiv.org/pdf/1902.11004)
  - [FastText (2016)](https://arxiv.org/pdf/1607.04606)
- 순환신경망 RNN
  - [RNN (1986)](https://arxiv.org/pdf/2308.09728)
  - [LSTM (1997)](https://arxiv.org/pdf/2105.06756)
  - [GRU (2014)](https://arxiv.org/pdf/1406.1078)
  - [GLU (2016)]()
- 시퀀스 변환 (Sequence-to-Sequence)
  - [Seq2Seq (2014)](https://arxiv.org/pdf/1409.3215)
  - [Bahdanau Attention (2015)](https://arxiv.org/pdf/1409.0473)
  - [Luong Attention (2015)](https://arxiv.org/pdf/1508.04025)
- Transformer
  - [Transformer (2017)](https://arxiv.org/pdf/1706.03762)
  - 
3) 들어가려는 연구실 교수님 논문 review 세미나 준비

    - 11일 : [충북대 컴공 CBNU DL 세미나](https://sites.google.com/view/dl-keep-up/)
        - Deepseek LLM model
