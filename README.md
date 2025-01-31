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
    - 논문 리뷰 로드맵 / [참고git](https://github.com/rafaelpadilla/Object-Detection-Metrics)
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
    - [M2Det 논문 review](https://arxiv.org/pdf/1811.04533) / [참고블로그](https://herbwood.tistory.com/23)
    - [YOLO v4 논문 review](https://arxiv.org/pdf/2004.10934v1) / [참고블로그](https://herbwood.tistory.com/24)
    - [EfficientDet 논문 review](https://arxiv.org/pdf/1911.09070) / [참고블로그](https://herbwood.tistory.com/25)
      
    - [DETR 논문 review2](https://arxiv.org/pdf/2005.12872) / [참고블로그](https://herbwood.tistory.com/26)
    -
    - 이미지를 광학문자로 인식 처리하는 방법 RNN도 트랜스포머 이런거?
