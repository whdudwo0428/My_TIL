# VisionAI: Automated Mosaic Processing Platform

## 프로젝트 개요
### 프로젝트 목표
비전과 딥러닝 기술을 활용하여 이미지를 자동으로 분석하고 특정 객체(혈흔, 얼굴, 성인 컨텐츠 등)를 탐지하여 모자이크 처리하는 기능을 제공하는 웹사이트 개발.

### 주요 기능
1. **혈흔 탐지 및 모자이크 처리**
2. **얼굴 탐지 및 모자이크 처리**
3. **성인 컨텐츠 탐지 및 모자이크 처리**
4. **사용자 인터페이스**: 각 기능을 선택하여 사용자 맞춤형 처리를 지원하는 웹페이지.

---

## 프로젝트 구조
### 기술 스택
#### 1. **프론트엔드**
- HTML, CSS, JavaScript (React.js 권장)
- 이미지 업로드 및 결과 표시 UI 개발

#### 2. **백엔드**
- Python (Flask or Django)
- REST API 개발
- 이미지 처리 및 모자이크 결과 반환

#### 3. **딥러닝 모델**
- PyTorch 또는 TensorFlow 사용
- 모델별 기능 구현:
  - 혈흔 탐지 모델: Mask R-CNN, U-Net
  - 얼굴 탐지 모델: YOLOv5, MTCNN, RetinaFace
  - 성인 컨텐츠 탐지: CLIP, DeepLab

#### 4. **데이터베이스**
- MongoDB 또는 PostgreSQL
- 사용자 업로드 이미지 및 처리 결과 저장

#### 5. **클라우드 및 배포**
- AWS (EC2, S3, Lambda) 또는 Google Cloud Platform (GCP)
- Docker 컨테이너화 및 배포

---

## 개발 계획
### 1. 데이터 준비
- **혈흔 탐지**: 의료, 범죄 관련 데이터셋 수집 및 라벨링
- **얼굴 탐지**: 공개된 얼굴 탐지 데이터셋 활용 (e.g., WIDER FACE)
- **성인 컨텐츠 탐지**: Open NSFW 데이터셋
- 대부분 오픈소스 준비되어 있을 것.

#### 데이터 라벨링 도구
- **Roboflow**
- LabelImg

### 2. 모델 개발 및 학습
#### 모델별 개발
1. **혈흔 탐지 모델**:
   - Mask R-CNN 또는 U-Net 기반의 세그멘테이션 모델
2. **얼굴 탐지 모델**:
   - YOLOv5 또는 MTCNN
3. **성인 컨텐츠 탐지**:
   - CLIP 기반 이미지 텍스트 매칭 또는 DeepLab

#### 학습 과정
- 전이 학습(Pre-trained 모델 활용)
- 학습 데이터 증강 (Augmentation)
- 평가 지표:
  - Precision, Recall, F1-Score
  - IoU (Intersection over Union)

### 3. 웹사이트 개발
#### 프론트엔드
- 사용자 업로드 인터페이스 및 처리 결과 표시 UI
- React.js 기반 SPA(Single Page Application) 구현

#### 백엔드
- Flask 또는 Django로 API 서버 구축
- 기능별 API:
  - `/process/blood`: 혈흔 탐지 및 모자이크 처리
  - `/process/face`: 얼굴 탐지 및 모자이크 처리
  - `/process/nsfw`: 성인 컨텐츠 탐지 및 모자이크 처리

### 4. 통합 및 배포
- 프론트엔드와 백엔드 통합
- Docker로 컨테이너화
- 클라우드 서비스(AWS/GCP)로 배포

---

## 공부해야 할 기술
### 1. **컴퓨터 비전**
- OpenCV: 이미지 전처리 및 모자이크 처리
- 딥러닝 모델 기반 객체 탐지 및 세그멘테이션

### 2. **딥러닝**
- PyTorch 또는 TensorFlow: 모델 개발 및 학습
- 전이 학습 및 Fine-tuning
- 데이터 증강 및 모델 평가 기법

### 3. **웹 개발**
- React.js: 사용자 인터페이스 개발
- Flask/Django: 백엔드 API 서버 개발
- REST API 설계 및 구현

### 4. **클라우드 및 배포**
- AWS (EC2, S3): 서버 및 스토리지 관리
- Docker: 애플리케이션 컨테이너화
- Git/GitHub: 협업 및 코드 관리

---

## 프로젝트 일정 / 수정 예정 초안
| 단계          | 기간             | 주요 작업                                 |
|---------------|------------------|------------------------------------------|
| **기획 및 설계** | 1주차            | 요구사항 분석, 기술 스택 및 구조 설계       |
| **데이터 준비** | 2~3주차          | 데이터 수집, 라벨링, 전처리               |
| **모델 학습**   | 4~6주차          | 모델 구현, 학습, 평가 및 튜닝              |
| **프론트엔드 개발** | 7~8주차          | React 기반 사용자 인터페이스 개발         |
| **백엔드 개발** | 7~8주차          | Flask/Django API 서버 개발               |
| **통합 및 테스트** | 9주차            | 프론트엔드와 백엔드 통합, 기능별 테스트     |
| **배포 및 발표** | 10주차           | 클라우드 배포 및 최종 발표                |

---

## 팀원 역할 분담
| 역할         | 팀원               | 주요 업무                                 |
|--------------|--------------------|------------------------------------------|
| **팀장**      | 본인               | 프로젝트 관리, 통합 설계, 모델 구현         |
| **데이터 엔지니어** | 팀원 1             | 데이터 수집, 라벨링, 전처리               |
| **모델 개발자**   | 팀원 2             | 모델 학습, 평가 및 튜닝                   |
| **프론트엔드 개발자** | 팀원 3             | React 기반 UI 개발                        |
| **백엔드 개발자**   | 팀원 4             | API 개발, 서버 관리                      |

---

## 레퍼런스 및 자료
- [OpenCV Documentation](https://docs.opencv.org/)
- [PyTorch Tutorials](https://pytorch.org/tutorials/)
- [TensorFlow Documentation](https://www.tensorflow.org/)
- [React Documentation](https://reactjs.org/docs/getting-started.html)
- [AWS Documentation](https://aws.amazon.com/documentation/)
- 비전관련 내용 처음 정리하기 좋은 영상 : https://www.youtube.com/watch?v=7tEYhOdg034
   - 이거 읽으면서 보면 편함 : https://github.com/whdudwo0428/My_TIL/tree/main/TIL
- CNN 공부자료 : https://www.youtube.com/watch?v=ZZKnBpd1lR4
- R-CNN 공부자료1 : https://www.youtube.com/watch?v=W0U2mf9pf8o
- R-CNN 공부자료2 : https://www.youtube.com/watch?v=FSZLcqEgq9Q
- U-Net 공부자료 : https://www.youtube.com/watch?v=wnuWqG18FVU
- YOLO 공부자료 : https://www.youtube.com/watch?v=RLNx_tOHGiY&t=6s
- 비전 개념 공부자료 : https://www.youtube.com/watch?v=9f2_8e3PtLI