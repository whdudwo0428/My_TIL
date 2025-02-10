## **NLP => tranformer 공부 순서 **
- 단어 임베딩 (Word Embedding)
  - [Word2Vec (2013)]()
  - [GloVe (2014)]()
  - [FastText (2016)]()
- 순환신경망 RNN
  - [RNN (1986)]()
  - [LSTM (1997)]()
  - [GRU (2014)]()
  - [GLU (2016)]()
- 시퀀스 변환 (Sequence-to-Sequence)
  - [Seq2Seq (2014)]()
  - [Attention Mechanism (2015)]()
  - [Bahdanau Attention (2015)]()
  - [Luong Attention (2015)]()
- Transformer
  - [Transformer (2017)]()

이후 NlP순서
ELMo (2018) → 문맥에 따라 변하는 워드 임베딩
ULMFiT (2018) → 전이 학습(Transfer Learning) 적용
5️⃣ 사전 학습 모델 (Pretrained Language Models)
BERT (2019) → 양방향 학습(Bidirectional)
GPT-1 (2018) → 단방향(Left-to-Right) 학습
GPT-2 (2019) → 크기 확장, zero-shot 학습
6️⃣ 범용 NLP 모델 (Generalized NLP Models)
T5 (2019) → Text-to-Text 모델
GPT-3 (2020) → Few-shot 학습
7️⃣ 대화형 AI 및 최신 모델 (Conversational AI & Recent Advances)
ChatGPT (2022) → 대화형 모델
LLaMA (2023) → 효율적인 오픈소스 언어 모델


1. DETR (2020) - End-to-End Object Detection with Transformers
주요 기여 (Contribution):
최초로 Transformer 기반 Object Detection 모델을 제안.
CNN과 Region Proposal Network (RPN)을 제거하고, Self-Attention Mechanism을 활용한 객체 탐지 구조를 도입.
Post-processing (e.g., NMS) 없이 엔드투엔드 학습 가능.
한계점:
큰 데이터셋이 필요하고, 학습 속도가 느림.
작은 객체 탐지 성능이 낮음 → 후속 연구에서 개선됨.
➡ 추천 이유: CNN 기반 Object Detection을 넘어 Transformer 기반으로 넘어가는 패러다임 변화를 만든 핵심 논문.

2. YOLOv7 (2022) - Real-Time Object Detection의 새로운 기준
주요 기여 (Contribution):
최고 성능과 속도의 균형을 가진 YOLO 모델.
Dynamic Label Assignment 기법 도입 → 학습 안정성 향상.
기존 YOLO 모델보다 연산 효율성을 개선하고, 실시간 탐지 성능을 최적화.
한계점:
YOLOv8과 비교하면 일부 실험에서 성능이 낮음.
Transformer 기반 모델과 비교하면 여전히 한계가 있음.
➡ 추천 이유: CNN 기반 모델 중 가장 최신의 강력한 성능을 갖춘 실시간 Object Detection 모델.

3. DINO (2023) - DETR 기반 성능 개선 모델
주요 기여 (Contribution):
DETR의 가장 큰 문제인 느린 수렴 속도를 해결.
DeNoising Anchor Boxes 기법을 도입하여 학습 안정성을 강화.
기존 DETR 대비 mAP 성능 향상 + 학습 속도 개선.
한계점:
계산량이 많고, 경량 모델이 아님.
YOLO 계열보다는 inference 속도가 느릴 수 있음.
➡ 추천 이유: Transformer 기반 Object Detection 모델의 한계를 해결한 최신 연구.




### **의료 데이터 분석을 위한 Classification 프로젝트 학습 가이드**  

#### **1. 목표 설정 및 개요**
- **목표**: 의료 데이터를 활용한 이미지 분류(Classification) 모델 개발  
- **분야**: 질병 진단, 종양 탐지, 병리학적 영상 분석 등  
- **핵심 기술**: CNN, Transformer, Self-Supervised Learning, Medical Imaging Preprocessing  

---

## **📌 1단계: 기본 개념 익히기 (Classification, Medical Imaging 기초)**
### 📚 **필수 개념**
✅ **이미지 분류(Image Classification) 개념**
- Supervised Learning vs. Unsupervised Learning  
- Loss Function (Cross-Entropy Loss)  
- Evaluation Metrics: Accuracy, Precision, Recall, F1-Score, ROC-AUC  

✅ **의료 영상 분석 개론**
- X-ray, MRI, CT, Ultrasound 영상의 특징  
- DICOM 데이터 처리 방식  
- Noise Reduction & Image Enhancement Techniques (Histogram Equalization, CLAHE)  

### 🛠 **추천 학습 자료**
- 📄 논문: **"Deep Learning in Medical Image Analysis"**  
- 🎥 강의: **CS231n (CNN을 이해하는 필수 코스)**  
- 📘 책: *"Deep Learning for Medical Image Analysis"*

---

## **📌 2단계: CNN 기반 Classification 모델 이해 및 실습**
### 📚 **필수 개념**
✅ **CNN 구조 및 동작 방식**  
- Convolution Layer, Pooling Layer, Fully Connected Layer  
- Activation Functions (ReLU, Sigmoid, Softmax)  
- Batch Normalization, Dropout 등 Regularization 기법  

✅ **대표적인 CNN 모델 분석**
- **VGG (2014)**: 가장 기본적인 CNN 구조  
- **ResNet (2015)**: Skip Connection을 통한 Gradient Vanishing 해결  
- **EfficientNet (2019)**: Parameter 효율성을 높인 모델  

✅ **Medical Image Classification 적용 사례**
- Pneumonia Detection using Chest X-ray (CheXNet, 2017)  
- Diabetic Retinopathy Classification (EyePACS Dataset)  

### 🛠 **추천 실습**
✅ **구현 목표**
- TensorFlow / PyTorch 기반으로 CNN 분류 모델 학습  
- Pretrained Model (ResNet, EfficientNet) 활용 및 Fine-tuning  
- 데이터 증강(Augmentation) 적용  

✅ **예제 프로젝트**
- **Kaggle Chest X-ray Classification Dataset** (Pneumonia Detection)  
- **Retinal Fundus Image Classification** (Diabetic Retinopathy Detection)  

---

## **📌 3단계: Transformer 기반 최신 Classification 연구**
### 📚 **필수 개념**
✅ **Vision Transformer (ViT) 이해**
- Self-Attention Mechanism  
- Patch Embedding & Positional Encoding  
- Multi-Head Attention & MLP Head  

✅ **Swin Transformer (Hierarchical ViT)**
- CNN과 Transformer의 장점을 결합한 모델  
- Medical Image Analysis에서의 Swin Transformer 적용 사례  

✅ **Self-Supervised Learning (SSL) 기법**
- Contrastive Learning (SimCLR, MoCo)  
- Masked Image Modeling (MAE, iBOT)  

### 🛠 **추천 실습**
✅ **구현 목표**
- ViT 모델을 활용한 의료 데이터 분류  
- ResNet + Transformer Hybrid 모델 성능 비교  
- Contrastive Learning을 활용한 Medical Image Pretraining  

✅ **추천 프로젝트**
- **Medical Image Classification using ViT**  
- **Self-Supervised Learning for MRI Image Analysis**  

---

## **📌 4단계: 의료 데이터 분석 및 Model Optimization**
### 📚 **필수 개념**
✅ **Model Optimization & Deployment**
- Quantization & Pruning  
- Knowledge Distillation  
- Model Compression for Edge AI  

✅ **Explainable AI (XAI) in Medical Imaging**
- Grad-CAM, SHAP을 활용한 모델 설명 가능성 확보  
- 의료 현장에서 신뢰할 수 있는 AI 모델 구축  

✅ **Federated Learning in Medical AI**
- 의료 데이터 보안 & 프라이버시 보호를 위한 Federated Learning 기법  
- Google’s **Flower** 라이브러리를 활용한 FL 모델 구축  

### 🛠 **추천 실습**
✅ **구현 목표**
- Medical Image AI 모델을 Flask / FastAPI로 배포  
- Explainability 기법 적용 후 성능 분석  
- Federated Learning으로 분산 학습 실험  

✅ **추천 프로젝트**
- **Grad-CAM을 활용한 AI 모델의 의료적 신뢰성 검증**  
- **Edge AI를 활용한 Mobile 기반 의료 AI 시스템 구축**  

---

### **📌 최종 정리: 프로젝트를 위한 논문 및 연구 추천**
1. **CheXNet: Radiologist-Level Pneumonia Detection (2017)**
2. **Self-Supervised Learning for Medical Image Analysis (2020)**
3. **ViT & Swin Transformer in Medical Imaging (2021-2022)**

---
2단계: CNN 기반 3D Object Detection (VoxelNet & BEV Representation)
📚 필수 개념
✅ Voxel 기반 3D Object Detection

VoxelNet (2017): LiDAR Point Cloud를 Voxel Grid로 변환하여 CNN으로 학습
SECOND (Sparse Efficient Convolutional Detection, 2018): Sparse CNN을 활용해 VoxelNet의 연산량 감소
PointPillars (2019): 3D 데이터를 2D BEV 형태로 변환하여 빠른 탐지 수행
✅ BEV (Bird's Eye View) 기반 탐지

BEVFormer (2022): Transformer를 활용한 BEV Representation
CenterPoint (2021): Anchor-free 3D Object Detection 모델
✅ KITTI Dataset & OpenPCDet 활용법

KITTI 데이터셋 구조 분석
OpenPCDet (PyTorch 기반 3D Object Detection 라이브러리) 활용
🛠 추천 실습
✅ 구현 목표

VoxelNet / PointPillars 모델을 OpenPCDet으로 구현
BEV Representation 변환 실습
✅ 예제 프로젝트

KITTI 데이터셋 기반 Point Cloud 3D Detection
nuScenes 데이터셋을 활용한 자율주행 객체 탐지
📌 3단계: Transformer & Point-based 3D Object Detection
📚 필수 개념
✅ Point Cloud 직접 활용하는 모델

PointNet (2017): MLP 기반의 최초 Point Cloud Classification 모델
PointNet++ (2017): Multi-scale Sampling을 통한 개선
PV-RCNN (2020): Point-based & Voxel-based Hybrid Detection
✅ Transformer 기반 3D Object Detection

3DETR (2021): DETR의 Transformer 구조를 3D Point Cloud에 적용
Pointformer (2021): Self-Attention을 이용한 Point Cloud Feature Extraction
✅ Self-Supervised Learning & 3D Pretraining

Contrastive Learning (DepthContrast, PointContrast)
Masked Point Cloud Pretraining (Point-BERT, MaskedPointMLP)
🛠 추천 실습
✅ 구현 목표

PointNet++을 활용한 Point Cloud Classification
PV-RCNN과 3DETR 비교 실험
✅ 추천 프로젝트

Point Cloud 기반 Object Detection (Waymo Dataset 활용)
Transformer를 이용한 3D Object Detection 성능 비교
📌 4단계: 3D Object Detection 실전 응용 (Edge AI, Autonomous Driving)
📚 필수 개념
✅ Edge AI를 위한 경량화 기법

Quantization (TensorRT, ONNX 활용)
Model Pruning & Knowledge Distillation
✅ 자율주행 & 로보틱스 응용

Multi-Sensor Fusion (LiDAR + Camera 데이터 통합)
Real-time Processing (CUDA Optimization)
ROS (Robot Operating System) 활용
✅ Explainable AI (XAI) in 3D Detection

Grad-CAM for Point Cloud
Feature Visualization in 3D Neural Networks
🛠 추천 실습
✅ 구현 목표

LiDAR + Camera Sensor Fusion 모델 개발
Edge AI를 위한 3D Detection 모델 경량화
✅ 추천 프로젝트

Real-Time 3D Object Detection for Autonomous Vehicles
Lightweight 3D Detection Model for Embedded Systems

3D O-D추천 논문 & 연구
VoxelNet: End-to-End Learning for Point Cloud Based 3D Object Detection (2017)
PointPillars: Fast Encoders for Object Detection from Point Clouds (2019)
PV-RCNN: Point-Voxel Feature Set Abstraction for 3D Object Detection (2020)
3DETR: A Transformer-based End-to-End 3D Object Detection Model (2021)
BEVFormer: Learning Bird’s Eye View Representation via Transformer (2022)
