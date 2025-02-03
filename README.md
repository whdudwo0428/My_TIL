## Today I Learned
- 1월 23일 작성시작
- 1월 11일 이후 공부한 내용들만 포함
- 좋은 TIL 저장소 예시
    - [예시1](https://github.com/Highjune/TIL)

---
- **1월 11일**
    - 강화학습 이론과 알고리즘 공부
        - 파이썬으로 간단한 GridWolrd를 만들고 경로최적화 문제 실습
              - Q-Learning과 SARSA 구현,ε-탐욕 정책, Q-테이블 학습, 업데이트 공식, 강화학습 내 파이퍼파라미터 등 이해.
          
- **1월 12일**
    - 10일 내용 이어서 이것 저것 많이 읽어봄 특히 Lidar, Camera 등 기술 탐구
    - 추천 논문 간단히 요약한 내용 읽어봄, 사실 무슨 내용인지 잘 모르겠어서 프로젝트 시작 전 최대한 관련 사전지식을 채우기 위한 로드맵을 구성
      
- **1월 13일**
    - TIL, Projecet 등 포트폴리오 준비구성, Git 사용 익숙해지도록 공부 
    - GELU, ADAS, 레이더 도플러효과, 허프변환 등 정말 다양한 범주로 이것저것 서칭하고 정리
    - 자율주행에 대한 기술들을 A to Z 정리 : [TIL_0110](https://github.com/whdudwo0428/My_TIL/blob/main/TIL_0110.md)
    
- **1월 14일**
    - SLAM과 3D Mapping 개념 간단히 훑어봄.
    - 시각정보 인지 메커니즘 공부 : 눈의 구조, 세포와 시각수용체, 스펙트럼 별 인지 등
    - LiDAR의 원리와 발전에 대한 깊은 공부
        - Solid-State LiDAR, ToF-FMCW의 통신 및 신호처리 그와 관련된 수학적 내용, 응용분야와 산업트렌드 등 광범위하고 깊게 공부
      
- **1월 15일**
    - 테슬라 FSD 라이센싱 비즈니스 모델과 end to end에 대해 간단히 이해해봄
    - 위성항법 GNSS(GPS) 원리와 자율주행에서의 활용성 탐구
    - Git을 너무 못쓰는 것 같아 살짝 시간투자, 포트폴리오와 논문구조 양식 등 살펴봄
    - 분명 이거 말고도 뭐 많이 읽고 통신이랑 수학공부 꽤 했던것같은데 기억이 안남
      
- **1월 16일**
    - None...
      
- **1월 17일**
    - Projecet1.DiabetesPrediction 구조 및 baseline code 작성
        - 프로젝트 목적에 따른 다양한 모델 공부
          
- **1월 18일**
    - [Projecet1.DiabetesPrediction](https://github.com/whdudwo0428/MyProjects/tree/main/DiabetesPrediction)
        - 모델 간소화, 효율성 확보 방법론 공부
        - Loggin과 같은 학습로그 모듈 공부
        - README를 정리하는 과정에서 Git tool 이해도 높이려고 노력했음
    - Projecet2.ChessPiece Detection 모델 선별 및 구조도 작성
        - Git, Roboflow 등에서 코드, 모델, 데이터를 불러오고 데이터를 모델에 맞게 전처리하는 과정을 익힘
        - YOLO 구조에 대해 간단히 이해
      
- **1월 19일**
    - [Projecet2.ChessPiece Detection](https://github.com/whdudwo0428/MyProjects/tree/main/ChessPiece%20Detection) 완성
        - 애초 본 프로젝트 목적도 Git이나 Pytorch사이트에서 끌어오고 이런 방법을 익히는 목적이었지만 알고리즘이나 코드, 파일구조 등 제대로 된 이해없이 그저 따라가는 느낌이 들었음. 잠시 프로젝트 진행을 멈추고 Detection공부를 마친 후 Project3를 진행하자 생각.
    - FPN, UNET 등 Segmentation 모델 알고리즘을 초기모델에서부터의 발전 과정과 논리를 중심으로 공부
    
- **1월 20일**
    - 자체적으로 구상중인 팀프로젝트_자동 모자이크 처리 프로그램과 웹페이지 제작을 위해 어떤 모델이 최적화일지 공부
        - 해당 문제에 적합한 다양한 모델을 서칭하며 읽어보고 특히 YOLO version별 차이와 그에 따른 데이터 전처리, 데이터셋-모델-실행코드 간 파일구조에 시간투자
        - 모자이크 과정에서 필요한 OpenCV blur처리 알고리즘에 대해 예전 실습했던 baseline코드와 함께 공부
      
- **1월 21일**
    - Project3.Detection_Soccer 구조도 작성 및 모델 선별
        - 데이터셋 선별 후 모델 선별과정에서 다양한 Object Detection 모델들 리스트업
    - 논문 리뷰 로드맵 / [참고git](https://github.com/hoya012/deep_learning_object_detection)
    - [DETR 논문 review1](https://arxiv.org/pdf/2005.12872) / [참고블로그](https://herbwood.tistory.com/26)
    
- **1월 22일**
    - Object Detection의 mAP를 포함한 성능 평가 Metric 탐구 : 추후 다양한 Metric 공부 계획
    - [DETR 논문 review2](https://arxiv.org/pdf/2005.12872) / [참고블로그](https://herbwood.tistory.com/26)
    - [R-CNN 논문 review](https://arxiv.org/pdf/1311.2524) / [참고블로그](https://herbwood.tistory.com/5)
      
- **1월 23일**
    - [OverFeat 논문 review](https://arxiv.org/pdf/1312.6229) / [참고블로그](https://herbwood.tistory.com/7)
        - 기존에 조금씩 햇갈리던 기본 CNN 동작 원리를 기존보다 깊게 탐구 (Padding, Strid, Pooling, 각 Layer 내 원리)
        - Git에 지금까지의 TIL작성하며 어떤 내용을 공부했나 다시 정리하고 읽어봄
        - OverFeat의 개념을 바탕으로  Two stage detector -> One stage detector 핵심 차이를 공부
    - [Fast R-CNN 논문 review](https://arxiv.org/pdf/1504.08083) / [참고블로그](https://herbwood.tistory.com/8)

- **1월 24일**
    - [Faster R-CNN 논문 review](https://arxiv.org/pdf/1506.01497) / [참고블로그](https://herbwood.tistory.com/10)
    - [OHEM 논문 review](https://arxiv.org/pdf/1604.03540) / [참고블로그](https://herbwood.tistory.com/12)
      
- **1월 25일**
    - [YOLO v1 논문 review](https://arxiv.org/pdf/1506.02640) / [참고블로그](https://herbwood.tistory.com/13)
    - [SSD 논문 review](https://arxiv.org/pdf/1512.02325) / [참고블로그](https://herbwood.tistory.com/15)
      
- **1월 26일**
    - [R-FCN 논문 review](https://arxiv.org/pdf/1605.06409) / [참고블로그](https://herbwood.tistory.com/16)
    - [YOLO v2 논문 review](https://arxiv.org/pdf/1612.08242) / [참고블로그](https://herbwood.tistory.com/17)
      
- **1월 27,28일**
    - [FPN 논문 review](https://arxiv.org/pdf/1612.03144) / [참고블로그](https://herbwood.tistory.com/18)
        - FPN 자체가 새로운 개념보단 이전 모델들을 잘 조합해 성능을 높인거다보니 다른 논문을 공부할 때에 비해 내가 어떤걸 모르고 아는지를 좀 더 명확히 할 수 있었음. 해서 시간투자를 좀 해서 기존 모델들을 복습하고, 아래 내용을 처럼 기본이 되는 내용들을 더 익숙해지는데 집중함
        - CNN 내 다양한 Layer들(fc,coonv,Reorg, ResidualConn 등)의 원리부터 Bottom-up, Top-down Pathway, Lateral Connetion 구조 등 다양한 구조적 개념
        - K-means Clustering 을 공부하며 이전 논문을 리뷰하며 공부했던 수학개념들을 다시 복습(주로 Loss내 공식에서 찾아봤던 지시함수, 특이값분해, 이중합산 같은 선형대수적 내용)
        - PS) FPN을 리뷰하며 이전 논문들도 다시 돌아가서 찾는 경우가 많았고 이제 뭐가 뭔지 좀 알아듣는 느낌
      
- **1월 29,30일**
    - [RetinaNet 논문 review](https://arxiv.org/pdf/1708.02002) / [참고블로그](https://herbwood.tistory.com/19)
    - [Mask R-CNN 논문 review](https://arxiv.org/pdf/1703.06870) / [참고블로그](https://herbwood.tistory.com/20?category=856250)
 

- **1월 31일**
    - [YOLO v3 논문 review](https://arxiv.org/pdf/1804.02767) / [참고블로그](https://herbwood.tistory.com/21)
    - [RefineDet 논문 review](https://arxiv.org/pdf/1711.06897) / [참고블로그](https://herbwood.tistory.com/22)
        - RefineDet 논문을 읽으면서 ARM과 ODM의 개별적인 역할은 명확하게 설명되었지만, ODM에서 각 스케일에 나온 정보를 어떻게 최종적으로 통합하는지(multi-scale feature에서 나온 여러 prediction을 어떻게 최종적으로 통합하는지/Multi-scale Feature에서 가져오는 정보의 조합 방식, Bounding Box Regression 과정 등) 명확하지 않아 직접 코드를 Scratch하여 이해하는 과정이 필요했음.
논문이 조금 불친절했던 것도 있지만, review하며 무의식적으로 지금까지 base model들과 개념들을 최대한 깊게 읽고 공부했던 내용들을 바탕으로 '아 이 개념은 어느 모델/기술에서 Scratch해왔구나', '이 부분 이런 네트워크로 구성하면 어떤 문제가 생겼던거 같은데 어케 해결했지'와 같은 고민을 하며 읽게되었다. 뭔가 이 해당 논문을 읽으며 저번 FPN논문을 리뷰할때처럼 객체탐지 모델에 대한 어느정도 insight가 생긴 느낌을 받았다.
    - [M2Det 논문 review](https://arxiv.org/pdf/1811.04533) / [참고블로그](https://herbwood.tistory.com/23)

2월 1일, 2일은 이것 저것 손 닿는대로 싹다 찾고 읽고 이해하고하느라 게시한 내용 말고 다양한 내용을 공부했는데 다 적긴 힘듬...
특히 수학 공부를 정말 많이함. 지난 이틀간 [임커밋님의 유튜브채널](https://www.youtube.com/@%EC%9E%84%EC%BB%A4%EB%B0%8B/videos)을 정말 많이 보고 참고함.
- **2월 1일**    
    - [YOLO v4 논문 review](https://arxiv.org/pdf/2004.10934v1) / [참고블로그](https://herbwood.tistory.com/24)
        - YOLOv4에서는 개인적으로 새로운 개념과 다양한 기법들이 대거 도입된 느낌을 받아 처음 객체탐지 모델 논문을 읽었을 때 처럼 막막한 기분이 들었다. (한줄마다 새로운 개념과 단어들이 계속 나오는... 심지어 그때보다 더 복잡하다...) YOLOv3같은 기존 논문들까지는어느정도 특정 모듈의 개선을 중심으로 발전시켰던 분명 심플한 디자인의 모델이었던것 같은데 말입니다. 특히 Bos, BoF 같은 새로운 개념을 접하며 이전 네트워크 개선에 대한 공부 뿐만 아니라 성능 향상에 기여하는 다양한 요소와 기반지식들을 체계적으로 공부하고 넘어가야할 필요성을 느꼈다. Bos, BoF뿐만 아니라 CSPDarknet53, PANet, CIoU, Mish activation, Mosaic augmentation 등 더 복잡한 개념들을 접하며 너무 힘들었던 review였다...
    - [영단어](https://github.com/whdudwo0428/My_TIL/blob/main/Vocabulary.md) (논문 읽을 때 영어 단어 때문에 좀 더딘게 느껴졌기에 관련분야 논문에서 많이 쓰이는 형용사와 동사, 공부하는 분야 관련 논문에 많이 언급되는 형용사, 동사, 고유명사들 정리)
    - 다양한 **Data Augmentation** 기법의 수학적 원리를 중점적으로 공부하고, OpenCV 코드를 분석하며 구현 방식까지 살펴봄 + RGP-D를 중심으로 image processing에 대한 개념을 쌓고 더 깊게 공부해 솔직히 대충 짚고 넘겼던 channel에 대한 개념을 제대로 이해 할 수 있었음
        - 자연스럽게 생성모델(Generative model)에 대한 정보를 접하게 되어 어떤게 있는지 찾아봄. object detection, segmentation 이후 관련 공부와 프로젝트 진행하고싶음 [생성모델 관련 논문 커리큘럼 추천](https://donghyun99.tistory.com/24)
    - **VQ-VAE**    (논문)[https://arxiv.org/pdf/1711.00937]
        - Flow based model(Normalizing)과정과 특히 역함수 접근과 loss -> 3일에 flow matchin까지 공부해보도록
        - 인코더-디코더 구조와 원리(FCN, U-net이나 객체탐지 공부할 땐 그냥 저수준부터 고수준까지 특징 추출하고 복원하는 것, 네트워크 구조 정도 수준으로 얕게 이해했었는데 이번에 제대로 공부함)
        - AE, Scalar/Vector Quantization 같은 하위 개념부터 차근차근 공부함 //그런데 솔직히 discretization랑 Scalar Quantization 차이 아직도 납득이 안됨...


- **2월 2일**
    - [영단어](https://github.com/whdudwo0428/My_TIL/blob/main/Vocabulary.md)
    - [Neural ODE 논문 review](https://arxiv.org/pdf/1806.07366) / [참고 Youtube](https://www.youtube.com/watch?v=EhyrwwjVuWU&t=1268s)
        - ODE 기초부터 Neural의 수치적접근을 코드로 구현하는 과정까지 등 넓게 이해하려 함
        - 이거하면서 옛날에 공부했던 것들의 loss도 같이 보면서 수학공부 엄청함...

    - __init__ 같은 코드 파일 구조부터 파이썬 기술 같은거 좀 봤는데 솔직히 졸면서 봤음 한 5번째 프로젝트 할때쯤 신경써보기 시작하면 될듯?

    - Diffusion(DDPM)도 공부했는데 솔직히 하나도 모르겠음 나중에 다시 공부해야함... 아래 선행 되어야할 개념들을 정리해두겠음 언젠간 GAN 공부한 이후 다시 도전
        - (Continuous) Stochastic Process((연속)확률 과정), Markov Process, 확률 미분 방정식(SDE)
        - Noise Schedule, Variance Schedule
        - VAE, GAN 같은 생성모델 기반개념 잡기

 
- **2월 3일**
    - [영단어](https://github.com/whdudwo0428/My_TIL/blob/main/Vocabulary.md)
    - 1일, 2일 공부 내용 복습
    - CNN 마지막으로 아직도 깔끔하게 정리 안된 내용들 공부(stride같은거)
    - 4일~ 계획짜기

      
- **2월 4일**
    - ㅁㄴㅇㄹ

      
- **2월 5일**
    - ㅁㄴㅇㄹ

- **2월 6일**
    - ㅁㄴㅇㄹ
 
- **2월 7일**
    - ㅁㄴㅇㄹ
