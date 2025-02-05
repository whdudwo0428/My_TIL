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

- **2월 1일, 2일**    
    - [YOLO v4 논문 review](https://arxiv.org/pdf/2004.10934v1) / [참고블로그](https://herbwood.tistory.com/24)
        - YOLOv4에서는 개인적으로 새로운 개념과 다양한 기법들이 대거 도입된 느낌을 받아 처음 객체탐지 모델 논문을 읽었을 때 처럼 막막한 기분이 들었다. (한줄마다 새로운 개념과 단어들이 계속 나오는... 심지어 그때보다 더 복잡하다...) YOLOv3같은 기존 논문들까지는어느정도 특정 모듈의 개선을 중심으로 발전시켰던 분명 심플한 디자인의 모델이었던것 같은데 말입니다. 특히 Bos, BoF 같은 새로운 개념을 접하며 이전 네트워크 개선에 대한 공부 뿐만 아니라 성능 향상에 기여하는 다양한 요소와 기반지식들을 체계적으로 공부하고 넘어가야할 필요성을 느꼈다. Bos, BoF뿐만 아니라 CSPDarknet53, PANet, CIoU, Mish activation, Mosaic augmentation 등 더 복잡한 개념들을 접하며 너무 힘들었던 review였다...
    - 영단어(논문 읽을 때 영어 단어 때문에 좀 더딘게 느껴졌기에 관련분야 논문에서 많이 쓰이는 형용사와 동사, 공부하는 분야 관련 논문에 많이 언급되는 형용사, 동사, 고유명사들 정리)
    - 다양한 **Data Augmentation** 기법의 수학적 원리를 중점적으로 공부하고, OpenCV 코드를 분석하며 구현 방식까지 살펴봄 + RGB를 중심으로 image processing에 대한 개념을 쌓고 더 깊게 공부해 솔직히 대충 짚고 넘겼던 channel에 대한 개념을 제대로 이해 할 수 있었음
        - 자연스럽게 생성모델(Generative model)에 대한 정보를 접하게 되어 어떤게 있는지 찾아봄. object detection, segmentation 이후 관련 공부와 프로젝트 진행하고싶음 [생성모델 관련 논문 커리큘럼 추천](https://donghyun99.tistory.com/24)
    - **VQ-VAE**    [논문](https://arxiv.org/pdf/1711.00937)
        - Flow based model(Normalizing)과정과 특히 역함수 접근과 loss -> 3일에 flow matching까지 공부해보도록
        - 인코더-디코더 구조와 원리(FCN, U-net이나 객체탐지 공부할 땐 그냥 저수준부터 고수준까지 특징 추출하고 복원하는 것, 네트워크 구조 정도 수준으로 얕게 이해했었는데 이번에 제대로 공부함)
        - AE, Scalar/Vector Quantization 같은 하위 개념부터 차근차근 공부함 //그런데 솔직히 discretization랑 Scalar Quantization 차이 아직도 납득이 안됨...
        - Residual VQ
    - **Neural ODE** [논문](https://arxiv.org/pdf/1806.07366) / [참고 Youtube](https://www.youtube.com/watch?v=EhyrwwjVuWU&t=1268s)
        - ODE 기초부터 Neural의 수치적접근을 코드로 구현하는 과정까지 등 넓게 이해하려 함
        - 이거하면서 옛날에 공부했던 것들의 loss도 같이 보면서 수학공부 엄청함...
        - ODE solver 
    - [영단어](https://github.com/whdudwo0428/My_TIL/blob/main/Vocabulary.md)
      
    - __init__ 같은 코드 파일 구조부터 파이썬 기술 같은거 좀 봤는데 솔직히 졸면서 봤음 한 5번째 프로젝트 할때쯤 신경써보기 시작하면 될듯?
    - Diffusion(DDPM)도 공부했는데 솔직히 하나도 모르겠음 나중에 다시 공부해야함... 아래 선행 되어야할 개념들을 정리해두겠음 언젠간 GAN 공부한 이후 다시 도전
        - (Continuous) Stochastic Process((연속)확률 과정), Markov Process, 확률 미분 방정식(SDE)
        - Noise Schedule, Variance Schedule
        - VAE, GAN 같은 생성모델 기반개념 잡기

 
- **2월 3일**
    - [영단어](https://github.com/whdudwo0428/My_TIL/blob/main/Vocabulary.md)
    - 1일, 2일 공부 내용 복습
    - CNN 추가 공부 (계속해서 CNN 기본기가 굉장히 약함 앞으로도 지속적으로 공부할 수 있도록 준비)
    - 세미나 주제로 정할 3D object Detection에 관련된 논문 searching
        - [추천 논문](https://github.com/maudzung/Awesome-Autonomous-Driving-Papers) 및 학습 로드맵 정리
        - 3D point cloud / LiDAR / Voxel Grid / 3D object Detection / 

- **2월 4일**
    - [VoxelNet 논문](https://arxiv.org/abs/1711.06396) review 세미나 준비
    - 
  
- **2월 5일**
    - [VoxelNet 논문](https://arxiv.org/abs/1711.06396) review 세미나 준비 및 발표
        - Receptive field, ~wise 개념 공부특히 수학 공부를 정말 많이함. 지난 이틀간 [임커밋님의 유튜브채널](https://www.youtube.com/@%EC%9E%84%EC%BB%A4%EB%B0%8B/videos)을 정말 많이 보고 참고함.

- **2월 1일, 2일**    
    - [YOLO v4 논문 review](https://arxiv.org/pdf/2004.10934v1) / [참고블로그](https://herbwood.tistory.com/24)
        - YOLOv4에서는 개인적으로 새로운 개념과 다양한 기법들이 대거 도입된 느낌을 받아 처음 객체탐지 모델 논문을 읽었을 때 처럼 막막한 기분이 들었다. (한줄마다 새로운 개념과 단어들이 계속 나오는... 심지어 그때보다 더 복잡하다...) YOLOv3같은 기존 논문들까지는어느정도 특정 모듈의 개선을 중심으로 발전시켰던 분명 심플한 디자인의 모델이었던것 같은데 말입니다. 특히 Bos, BoF 같은 새로운 개념을 접하며 이전 네트워크 개선에 대한 공부 뿐만 아니라 성능 향상에 기여하는 다양한 요소와 기반지식들을 체계적으로 공부하고 넘어가야할 필요성을 느꼈다. Bos, BoF뿐만 아니라 CSPDarknet53, PANet, CIoU, Mish activation, Mosaic augmentation 등 더 복잡한 개념들을 접하며 너무 힘들었던 review였다...
    - 영단어(논문 읽을 때 영어 단어 때문에 좀 더딘게 느껴졌기에 관련분야 논문에서 많이 쓰이는 형용사와 동사, 공부하는 분야 관련 논문에 많이 언급되는 형용사, 동사, 고유명사들 정리)
    - 다양한 **Data Augmentation** 기법의 수학적 원리를 중점적으로 공부하고, OpenCV 코드를 분석하며 구현 방식까지 살펴봄 + RGB를 중심으로 image processing에 대한 개념을 쌓고 더 깊게 공부해 솔직히 대충 짚고 넘겼던 channel에 대한 개념을 제대로 이해 할 수 있었음
        - 자연스럽게 생성모델(Generative model)에 대한 정보를 접하게 되어 어떤게 있는지 찾아봄. object detection, segmentation 이후 관련 공부와 프로젝트 진행하고싶음 [생성모델 관련 논문 커리큘럼 추천](https://donghyun99.tistory.com/24)
    - **VQ-VAE**    [논문](https://arxiv.org/pdf/1711.00937)
        - Flow based model(Normalizing)과정과 특히 역함수 접근과 loss -> 3일에 flow matching까지 공부해보도록
        - 인코더-디코더 구조와 원리(FCN, U-net이나 객체탐지 공부할 땐 그냥 저수준부터 고수준까지 특징 추출하고 복원하는 것, 네트워크 구조 정도 수준으로 얕게 이해했었는데 이번에 제대로 공부함)
        - AE, Scalar/Vector Quantization 같은 하위 개념부터 차근차근 공부함 //그런데 솔직히 discretization랑 Scalar Quantization 차이 아직도 납득이 안됨...
        - Residual VQ
    - **Neural ODE** [논문](https://arxiv.org/pdf/1806.07366) / [참고 Youtube](https://www.youtube.com/watch?v=EhyrwwjVuWU&t=1268s)
        - ODE 기초부터 Neural의 수치적접근을 코드로 구현하는 과정까지 등 넓게 이해하려 함
        - 이거하면서 옛날에 공부했던 것들의 loss도 같이 보면서 수학공부 엄청함...
        - ODE solver 
    - [영단어](https://github.com/whdudwo0428/My_TIL/blob/main/Vocabulary.md)
    - __init__ 같은 코드 파일 구조부터 파이썬 기술 같은거 좀 봤는데 솔직히 졸면서 봤음 한 5번째 프로젝트 할때쯤 신경써보기 시작하면 될듯?
    - Diffusion(DDPM)도 공부했는데 솔직히 하나도 모르겠음 나중에 다시 공부해야함... 아래 선행 되어야할 개념들을 정리해두겠음 언젠간 GAN 공부한 이후 다시 도전
        - (Continuous) Stochastic Process((연속)확률 과정), Markov Process, 확률 미분 방정식(SDE)
        - Noise Schedule, Variance Schedule
        - VAE, GAN 같은 생성모델 기반개념 잡기

 
- **2월 3일**
    - [영단어](https://github.com/whdudwo0428/My_TIL/blob/main/Vocabulary.md)
    - 1일, 2일 공부 내용 복습
    - CNN 추가 공부 (계속해서 CNN 기본기가 굉장히 약함 앞으로도 지속적으로 공부할 수 있도록 준비)
    - 세미나 주제로 정할 3D object Detection에 관련된 논문 searching
        - [추천 논문](https://github.com/maudzung/Awesome-Autonomous-Driving-Papers) 및 학습 로드맵 정리
        - 3D point cloud / LiDAR / Voxel Grid / 3D object Detection 해당 카테고리에 기본 개념들에 대해 공부 (앞으로는 이것저것 찾아볼 때 어떤걸 찾아봤는지 정리하는 습관을 가져야겠음...)

- **2월 4일**
    - [VoxelNet 논문](https://arxiv.org/abs/1711.06396) review 세미나 준비
        - 정말 하루종일 세미나 준비만해서 Network의 architecture, idea 필요한 지식을 두루두루 공부했다... 3일~5일까지 밤새면서 공부하고 준비했다. ㅜㅜ 
  
- **2월 5일**
    - [VoxelNet 논문](https://arxiv.org/abs/1711.06396) review 세미나 준비 및 발표
        - 세미나 준비 기간이 2일정도로 제한되어있기에 거의 잠도 안자고 공부하고 ppt를 제작했다. 때문에 초안 수준 정도로 ppt로 완성도가 낮았지만 논문 내 핵심 idea나 내가 공부하면서 깊게 탐구했떤 그런 말하고싶던 내용 누락 없이 구성하는 정도에는 성공한 것 같다. 갑자기 발표 시간이 4시간 정도 앞당겨지는 바람에 script 준비를 하나도 못했지만 최대한 내용 이해를 목적으로 공부했던 터라 준비했던 내용을 70% 정도는 발표할 수 있었던 것 같았다. script 준비 없이 이 정도면 정말 잘한거라 칭찬 받아서 기분 좋다 ㅎㅎ. 첫 세미나라 너무 떨렸기에 발표 중에 절고 가슴이 뛰어서 너무 속상했다... 하지만 레벨업한게 느껴졌다는 주변 칭찬을 들어 꽤 만족스러웠던 첫 세미나였다. ppt만드는 능력만 높인다면 다음엔 더 잘 준비할 수 있을 것 같다. (학부 때 거의 발표를 맡고 ppt는 피드백하는 역할이었는데 후회된다...) 아래는 내가 세미나 도중 매끄럽게 설명하지 못하거나 질문 받았을 때 잘 모르겠는 개념들을 정리해놓았다. 6개의 keyword를 미국 가기 전 날인 2월 10일까지 하루에 하나씩 공부할 수 있도록!
        - **Receptive field**, **~wise operations**, **concat**, **Aggregation methods**, **feature extraction techniques**
        - 각 Layer나 block에서 Data의 구조(차원)에 대한 개념이 약한게 느껴졌다, resource가 정말 많이 투자됨 ㅠㅠ = 자료구조와 알고리즘에 이어 해당 내용을 공부할 수 있는 keyword를 찾아 공부하도록! (2월8일,9일에 공부계획)
    - [영단어](https://github.com/whdudwo0428/My_TIL/blob/main/Vocabulary.md) 고생했으니 집에서 쉬면서 계속 읽는 정도로!
    - Lab searching, CV 작성, email 준비
    
- **2월 6일**
    - [영단어](https://github.com/whdudwo0428/My_TIL/blob/main/Vocabulary.md) 고생했으니 집에서 쉬면서 계속 읽는 정도로!
    - 미국 가기 전 **내가 지금까지 공부한 내용들을 정리하고 체득하는 시간이 필요**할 거 같음 지금까지 **공부한 내용 복기**!
    - Lab searching, CV, contect-email 검사받을거 준비

- **2월 7일**
    - Lab searching, CV, contect-email 초안 검사받기!
  
- **2월 8일**






# 🔥 추천 논문 목록

### 1️⃣ **VoxelNet: End-to-End Learning for Point Cloud Based 3D Object Detection**
📌 **학회:** CVPR 2018  
📌 **주요 기여:**  
- 3D Point Cloud 데이터를 **Voxel 변환 후 CNN을 적용**하는 최초의 방법  
- 이후 **SECOND, PointPillars** 등의 연구가 이를 개선하여 발전  
 
📌 **추천 이유:**  
- **CNN과 다양한 Layer 구조** (Conv, FC, Residual Conn, Pooling, Padding, Stride 등) 개념을 활용 가능  
- **One-stage vs Two-stage Detector 차이**, Bounding Box Regression, Multi-scale Feature 개념과 연계  
- 기존 LiDAR Detection 방식 (**Point-based → Voxel-based**) 대비 CNN을 적극적으로 활용  
- 이후 연구들(**SECOND, PointPillars**)로 확장되며, 3D Object Detection의 핵심 기초 개념이 되는 논문  

🔗 **논문 링크:** [VoxelNet Paper](https://arxiv.org/abs/1711.06396)  
🔗 **GitHub 코드:** [VoxelNet Implementation](https://github.com/charlesq34/VoxelNet)  

---

### 2️⃣ **PV-RCNN: Point-Voxel Feature Set Abstraction for 3D Object Detection**
📌 **학회:** CVPR 2020  
📌 **주요 기여:**  
- **Point-based Feature**와 **Voxel-based Feature**를 결합하여 **3D Object Detection의 정확도를 향상**  
- **KITTI, Waymo 데이터셋**에서 우수한 성능 기록  
- 이후 연구(**PV-RCNN++, Voxel-RCNN**)에서 확장 및 활용  

📌 **추천 이유:**  
- LiDAR 신호 처리 (**ToF, FMCW, Solid-State LiDAR**), SLAM, 3D Mapping 등과 연관  
- **FPN, Residual Connection, Multi-scale Feature** 등의 개념을 활용  
- Waymo Open Dataset과 KITTI에서 **실전 자율주행과 연결성이 높음**  
- 최신 연구들이 이 논문을 기반으로 발전했으며, 이를 이해하면 후속 연구도 쉽게 접근 가능  

🔗 **논문 링크:** [PV-RCNN Paper](https://arxiv.org/abs/1912.13192)  
🔗 **GitHub 코드:** [PV-RCNN Implementation](https://github.com/open-mmlab/OpenPCDet)  

---

### 3️⃣ **PointRCNN: 3D Object Proposal Generation and Detection from Point Cloud**
📌 **학회:** CVPR 2019  
📌 **주요 기여:**  
- **PointNet++ 기반 Region Proposal 방식 적용**, LiDAR 점 구름에서 직접 3D 객체 감지  
- **Proposal Refinement**을 통해 Localization 정확도 증가  

📌 **추천 이유:**  
- CNN 기반 Object Detection (**YOLO, Faster R-CNN, R-FCN** 등), Bounding Box Regression, **Two-stage vs One-stage Detector 차이** 등을 공부한 경험과 연관  
- **Feature Pyramid Networks (FPN), Multi-scale Feature Extraction 개념 활용 가능**  
- 기존 VoxelNet과 달리 **Voxel 변환 없이 PointNet 기반 Feature Extraction 수행**  
- **Faster R-CNN 등의 Two-stage 구조와 연결**, 기존 Object Detection 개념을 활용하여 쉽게 접근 가능  

🔗 **논문 링크:** [PointRCNN Paper](https://arxiv.org/abs/1812.04244)  
🔗 **GitHub 코드:** [PointRCNN Implementation](https://github.com/sshaoshuai/PointRCNN)  

---

## 📌 **추천 논문 학습 로드맵**
### 🏆 **학습 순서**
1️⃣ **VoxelNet → PV-RCNN → PointRCNN** 순으로 읽기  
- **VoxelNet:** CNN과 3D Detection의 기본 개념 학습  
- **PV-RCNN:** VoxelNet을 발전시킨 모델로 이해가 쉬움  
- **PointRCNN:** Faster R-CNN 기반 Two-stage Detector 개념과 연결  

2️⃣ **논문 속 개념을 기존 공부한 내용과 연결**  
- **VoxelNet** → CNN 구조 (Pooling, Stride, Residual Connection 등) 활용  
- **PV-RCNN** → SLAM, LiDAR 기술, Multi-scale Feature 학습과 연결  
- **PointRCNN** → Two-stage Detector (Faster R-CNN 개념과 연계)  

3️⃣ **논문 구현 코드 분석 (GitHub 검색 및 baseline 코드 실행)**  
- PV-RCNN과 PointRCNN은 **PyTorch 기반 코드 제공**, GitHub에서 실행 및 분석 가능  
- VoxelNet도 TensorFlow/PyTorch 기반 코드가 많아 활용 가능  

---

## ✅ **우선순위**
1️⃣ **PV-RCNN** → **LiDAR, SLAM, CNN, Multi-scale Feature 등 네가 공부한 개념이 가장 많이 적용됨**  
2️⃣ **VoxelNet** → **CNN 기반 Feature Extraction을 공부했으니, Voxel 변환과 CNN 구조를 결합하는 개념이 익숙할 것**  
3️⃣ **PointRCNN** → **Faster R-CNN 기반의 Two-stage Detector이며, Bounding Box Regression을 익혔으니 이해하기 쉬움**  

---

## 🚀 **추가 참고 자료**
- **LiDAR 기반 3D Object Detection 개요:** [Awesome 3D Object Detection](https://github.com/kyoungseok-kim/Awesome-3D-Object-Detection)  
- **SLAM과 자율주행 관련 논문 정리:** [Awesome-SLAM](https://github.com/AtsushiSakai/Awesome-SLAM)  
- **딥러닝과 자율주행 기술 관련 서적:** [Deep Learning for Autonomous Driving](https://www.deeplearningbook.org/)  

---

## 🎯 **목표**
- 3D Object Detection의 최신 연구를 체계적으로 학습하고, **자율주행 및 LiDAR 기반 AI 연구와 연결**  
- GitHub 코드 분석을 통해 논문 구현을 직접 실행해보고, 연구 발전 방향을 탐색  

