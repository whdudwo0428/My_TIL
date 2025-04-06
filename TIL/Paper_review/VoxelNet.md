## VoxelNet: End-to-End Learning for Point Cloud Based 3D Object Detection  
#### 2025-02-04 ~ 02-05 / [https://arxiv.org/abs/1711.06396](https://arxiv.org/abs/1711.06396)

### Problem Statement
- 기존 3D 객체 탐지 방식은 LiDAR의 **point cloud를 voxel이나 bird’s-eye view로 변환한 뒤 hand-crafted feature를 사용**하거나, 2D 이미지 feature에 의존하는 방식이 많음.
- Point cloud는 불규칙하고 밀도가 낮기 때문에 **end-to-end 학습이 어렵고**, 대부분의 방법은 **feature extraction과 detection이 분리**된 파이프라인을 사용함.
- 따라서 **raw 3D point cloud로부터 직접 feature를 추출하고**, 이를 통해 **end-to-end로 3D 객체 탐지까지 수행하는 구조**가 요구됨.

### Solution Approach
- VoxelNet은 point cloud를 **voxel로 분할**한 뒤, 각 voxel 안의 point set에 대해 **PointNet 기반의 feature extractor**를 적용하고, 이를 **3D CNN으로 연결**해 전체 공간의 feature map을 구성함.
- 그 후 **Region Proposal Network**(RPN)을 이용해 **3D 객체 탐지 결과를 출력하는 end-to-end 구조**를 제안한다.

### Methodology Details

#### 1. **Voxelization**
- Point cloud를 3D voxel grid로 균일하게 나눔
- 각 voxel에는 최대 \( T \)개의 point를 포함 (예: 35)
- 빈 voxel은 무시하고, point가 존재하는 voxel만 처리

#### 2. **Voxel Feature Encoding (VFE) Layer**
- 각 voxel 안의 point 집합을 처리하기 위해 PointNet 유사 구조 적용
- 각 point P = (x, y, z, r)에 대해 상대 좌표, centroid 등을 포함한 feature 구성
- 두 개의 VFE Layer 구성:
  - MLP → Aggregation (element-wise max) → Concatenation → 다음 레이어
- 최종적으로 **voxel 단위의 feature vector 생성**

#### 3. **3D Convolutional Middle Layers**
- 3D 공간의 모든 voxel feature를 4D tensor로 쌓아 input volume 구성
- 여기에 3D CNN을 적용하여 전체 공간에서의 **spatial context**를 학습

#### 4. **Region Proposal Network (RPN)**
- 마지막에는 2D BEV(Bird’s Eye View) feature map으로 변환 후
- Faster R-CNN 스타일의 RPN을 통해 3D bounding box를 예측
- Output: center, dimensions, orientation, objectness 등

#### 5. **End-to-End 학습**
- 모든 파이프라인이 하나의 네트워크로 연결되어 있어 **end-to-end로 학습 가능**
- Anchor-based detection + classification loss + regression loss 사용

### Recap
VoxelNet은 raw point cloud를 직접 받아 **voxel 단위로 분할하고**, 각 voxel 내 point 집합에 대해 VFE module을 통해 feature를 추출한 뒤, 이를 3D CNN에 입력하여 공간적 패턴을 학습한다. 이후 RPN을 통해 최종적인 3D bounding box를 예측하는 구조로, **point-level → voxel-level → region-level 추론을 모두 end-to-end로 통합**한 최초의 3D 탐지기 중 하나다. 기존의 hand-crafted feature 의존성을 제거하면서도 높은 정확도를 기록했고, 이후 SECOND, PointPillars, CenterPoint 등 다양한 후속 모델의 기반이 되었다.

---

**한계점 및 후속 발전 방향**
- Voxelization 단계에서 **point precision이 손실**되고, **sparse voxel 처리 효율이 낮음**
- 이후 **Sparse 3D CNN**, **Point-wise 연산**, **pillar 구조(PointPillars)**, **center-based anchor-free 방식(CenterPoint)** 등이 제안되어 성능과 속도 모두 개선됨
- VoxelNet은 학문적으로 중요한 기여였지만, 산업적 deployment에는 최적화되지 않음 (속도, 메모리 측면)

**느낀 점**
세미나 준비 기간이 2일정도로 제한되어있기에 거의 잠도 안자고 공부하고 ppt를 제작했다. 때문에 초안 수준 정도로 ppt로 완성도가 낮았지만 논문 내 핵심 idea나 내가 공부하면서 깊게 탐구했떤 그런 말하고싶던 내용 누락 없이 구성하는 정도에는 성공한 것 같다. 갑자기 발표 시간이 4시간 정도 앞당겨지는 바람에 script 준비를 하나도 못했지만 최대한 내용 이해를 목적으로 공부했던 터라 준비했던 내용을 70% 정도는 발표할 수 있었던 것 같았다. script 준비 없이 이 정도면 정말 잘한거라 칭찬 받아서 기분 좋다 ㅎㅎ. 첫 세미나라 너무 떨렸기에 발표 중에 절고 가슴이 뛰어서 너무 속상했다... 하지만 레벨업한게 느껴졌다는 주변 칭찬을 들어 꽤 만족스러웠던 첫 세미나였다. ppt만드는 능력만 높인다면 다음엔 더 잘 준비할 수 있을 것 같다. (학부 때 거의 발표를 맡고 ppt는 피드백하는 역할이었는데 후회된다...) 아래는 내가 세미나 도중 매끄럽게 설명하지 못하거나 질문 받았을 때 잘 모르겠는 개념들을 정리해놓았다. 6개의 keyword를 미국 가기 전 날인 2월 10일까지 하루에 하나씩 공부할 수 있도록!
Receptive field, ~wise operations, Skip Connection, concat, Aggregation methods, feature extraction techniques, Point Density variance imbalance
논문 내 Sparse 4D Tensor를 설명하며 각 Layer나 block에서 Data의 구조(차원)에 대한 개념이 약한게 느껴졌다, resource가 정말 많이 투자됨 ㅠㅠ = 자료구조와 알고리즘에 이어 해당 내용을 공부할 수 있는 keyword를 찾아 공부하도록!
