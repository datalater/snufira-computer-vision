ⓒ JMC 2017

**SOURCE**  
\- 서울대학교 4차산업혁명 아카데미, 인공지능 에이전트 과정  
\- 컴퓨터 비전, 김건희 교수님

---

# II. 용어 정리

### 01 Introduction to Computer Vision

+ `edge` : 색이 급격히 변하는 부분 또는 경계

### 02 Topics covered

+ `depth` : 거리


---

## Lecture 22: Detection

### Object detection

p.7 parts model
- 중요한 part 간의 상대적인 거리가 존재한다.
- 사람 관련 detection에 꽤 많이 쓰임

p.10
- 이미지에서 object가 있을 만한 곳에 대한 patch를 찾아내는 것

p.14
- segmentation 후 segmentation의 수많은 조합 고려

p.18
- Non-max suppresion : 가장 높은 것 제외 나머지 버린다

p.19 context/reasoning
- 카메라 높이보다 어떠하면 공중에 떠 있는 것이다 -> 사람 아님

### Statistical Template Approach

p.26 R-CNN
- CNN에는 정사각형 input이 들어가는게 좋다
- 그래서 정사각형으로 이미지 워핑을 한다.
- R: Region

p.28
- tight한 decision boundary를 정하려면 positive example뿐만 아니라 negative example도 잘 구해야 한다.
  - ex. pedestrian 구별에서 사람 비스무리한 것을 negative로 넣어야지 너무 사람 아닌 것을 넣으면
  - tight한 decision boundary를 구하기 어렵다.


### Parts-based Models

p.32
- 자동차를 보면 part간에 geometric한 관계가 정해져 있다.


p.34
- tree : 임의의 노드 2개를 정했을 때 2개의 노드를 잇는 path가 한 개밖에 없는 경우


p.37 DPM
- 딥러닝 이전 최고의 알고리즘
- 전체 template, part에 대한 template, part간의 관계에 대한 template
- root filter : object 전체에 대한
- spatial costs : 상대적인 거리가 멀어질수록 값이 적어진다.


p.42
- 빨간색 네모 : object detection
- 파란색 네모 : part detection

**컴퓨터비전 끝.**

---

## Lecture 21: Classification

+ 제한된 환경에서는 classfication 잘 된다. (ImageNet)

### Image Classifiers

p.3
- image classification : 이미지를 하나의 D-dimension으로 나타내서 진행한다.
- 가장 간단한 image Classification : skin detection
  - skin이냐 skin이 아니냐
- skin detection: 이미지의 각 픽셀을 하나의 D-dimension의 벡터스페이스인 RGB color space에 맵핑한다.
  - RGB feature space에 skin이 모이게 된다.


p.4~ 분류기를 디자인하는 여러 가지 방법
- (1) K-Nearest neighbor
- Data modeling
  - (2) Generative : training data로부터 skin의 '**분포를 알아낸다**'.
    - ex. skin 데이터들이 특정 가우시안 분포를 따르는구나
    - 분류 방법 : 각 데이터가 label된 skin 데이터에 fitting될 likelihood를 구한다.
    - ex. Naive Bayesian
  - (3) Discriminative : training data로부터 skin을 구별하는 +,-의 '**decision boundary**'를 정한다.
    - 장점 : 직접 분류 가능
    - 단점 : unsupervised learning에서는 사용 불가
    - ex. SVM

> **Note:** Generative보다 Discriminative로 분류하는 것이 더 직접적이고 간단하다.

p.7 이미지를 D-dimension으로 나타내는 image features, 어떻게 하나
- 무엇을 분류하느냐에 따라 기준이 달라진다.
- beach : color or layout
- cloth fabric : texture
- mug : shape

> **Note:** 딥러닝 : data와 task에 따라 적절한 feature를 스스로 학습한다. ex. CNN에서 수많은 레이어의 거의 전부가 feature를 뽑아내는 레이어이고 분류 레이어는 마지막 하나이다.

p.9
- image representation: 이미지를 D-dimension의 벡터로 바꾼 것

p.11
- classifier : 함수
  - $f: R^{D} \rightarrow {-1, +1}$
  - positive : +1, negative : -1

p.14
- logistic regression을 k개로 확장한 것이 딥러닝 알고리즘 softmax이다.
- 괜찮은 classifiers
  - randomized forests : 사이즈도 작고 성능도 좋다.
  - boosted decision trees
  - SVM
- 쓰지마라
  - RBMs
- 하지만 결국 각 classifiers의 특징을 알고 적절한 task에 사용해야 한다.

### Exemplar-based Models

p.16
- K-nearest neighbor classfier를 생각하면 된다.

p.19
- K를 홀수로 해라 : 짝수면 동점일 때 또 나눠야 함
- KNN을 lazy learning이라 한다
  - training 시점에는 아무것도 안하다가
  - test example이 나오면 그제서야 nearest neighbor를 찾는다.
- KNN은 연구자의 feature extraction이 얼마나 좋은지 평가할 때 좋다.
- K가 커질수록 더 많은 label을 고려하므로 더 멀리 있는 training example까지 고려하므로 smooth하다.
- Bayes optimal error : classification으로 도달할 수 있는 최대의 오류


### Discriminative Models

p.21
- 얼굴인지 아닌지 분류하기


p.26
- False Positive : Negative인데 Positive로 False 했다.


p.27~ Discriminative, SVM
- positive와 negative를 나누는 평면을 찾는다.
- 평면 : decision boundary 역할
- feature space의 decision boundary
  + 2차원 : $ax+by+c=0$
  + 4차원 : $ax+by+cz+dw = 0$

p.30 error가 0인 decision boundary가 여러 개일 때 어떻게 정하나
- margin이 최대가 되는 line을 decision boundary로 정해야 한다.
- 요점 : decision boundary 정할 때 error를 사용하지 말고 margin을 사용해라.
- margin을 maximize해야 제대로 분류할 수 있다.


p.32 SVM
- SVM : margin을 최대로 하는 decision boundary를 정하는 알고리즘
- support vector : boundary에서 가장 가까운 데이터 샘플
  - positive support vector : positive쪽 support vector
  - negative support vector : negative쪽 support vector
- decision boundary를 정할 때는 positive support vector와 negative support vector만 있으면 된다.
- support vector가 decision boundary를 정한다.


p.36 Kernel Trick
- 두 가지 옵션
  - (1) feature의 차원을 그대로 두고 polynomial line
  - (2) feature의 차원을 높인 후 1차원 line
  - 수학적으로 (2)가 더 낫다


### Generative Models

p.39 Generative
- joint probability를 구한다.
- Generative vs. Discriminative
  - G : $P(x, y)$
    - Bayes Rule 이용
  - D : $P(y | x)$
    - feature가 들어왔을 때 -1인지 +1인지 정한다.

p.40 Bayes Classifier
- ex. 어떤 단어가 들어갔을 때 스팸 메일일 확률
- argmax :


p.42
- virtual counts : 확률값이 0이 되는 것을 막아주기 위해 작은 숫자(ex.2)를 더해준다.


p.43
- parameter : training data로부터 배우는 것
- hyper parameter : 연구자가 직접 값을 지정해야 함
- Imbalanced classifiers
  - 분류 label 각각의 개수가 다른 상태에서 learning하게 될 때
  - ex. 숫자1 - 천만 장, 숫자2 -3백만 장

p.44
- 가장 많이 쓰는 분류기 순서

**끝.**


---

## Lecture 20: Categorization

### Visual Recognition and Its Challenges

+ ...

### General Concepts of Categorization

+ Categorization을 해야 우리의 knowledge와 연결시켜서 이미지를 해석할 수 있다.
+ ex. 사람 뒤에 있는 산 속의 덩치 큰 물체 -> 곰 -> 위험하다
+ Categorization은 철학적 관점 3가지가 있는데 이미지에서도 같은 접근법을 사용한다.

### Image Categorization with Bag of Words



---

## Lecture 19: Features

### Why Keypoints (or Interest Points)

p.3 correspondence finding
- SIFT feature: 가장 많이 쓰이는 feature 중 하나


p.5
- Homography를 해보면 affine transformation으로 표현할 수 있다.
- descriptor : 노란색 네모 박스
- descriptor의 scale과 orientation을 어떻게 잡을 것인지 중요하다.
- descriptor : patch를 벡터로 표현한 것 $f_A, f_B$
- descriptor를 사용하는 이유 :
  - dimension을 줄이기 위해
  - 뷰 포인트, 일루미네이션(빛의 차이)의 변화에도 robust하게 만들기 위해 (raw pixel로 하면 위험하기 때문)

p.6
- repeatability : 같은 그림에 대한 서로 다른 이미지(크기나 회전의 변화)에서도 똑같은 feature가 반복적으로 뽑혀야 한다.


p.7 trade-offs
- repeatability를 너무 우선시하면 feature 자체가 적게 나온다.
  - feature가 적으면 매칭 불가
- distinctiveness를 너무 우선시하면 매칭이 잘 안된다.


p.9
- fixation points : 사람이 scene을 볼 때 continuous하게 보지 않는다. 이를 saccade(써캐드)라고 한다.
  - 사람은 시점이 있고 그거를 시점과 시점 사이를 움직이는 게 아니라
  - discrete하게 움직인다.

### Local Keypoint Detectors

+ unusual한 point를 찾아야 애매모호함을 피할 수 있다.

p.14 PCA
- 첫 번째로 variation이 가장 큰 point가 Principle Component(PC)가 된다.
- 두 번째로 첫 번째 PC와 직교(orthogonal)하는 point가 PC가 된다.
- PC끼리는 반드시 수직이어야 한다.


### Scale and Rotation

p.21
- 노란색 원 중에 뭐가 제일 좋은지 알려면 차이를 보면 된다.
- 스케일의 기본 아이디어 : 크기를 크게 바꿔가다가 정보 차이가 크면 그것이 best 스케일일 것으로 추정

p.22
- 라플라시안 필터를 사용한다.
- 라플라시안 필터의 response가 커지는 곳을 잡아라.
- 안과 밖의 차이가 커지면 respoonse가 커지기 때문이다.
- 라플라시안은 가우시안의 차이(DoG, Difference of Gaussian)로 사용한다.


### Local Descriptors

p.32 SIFT

**끝.**


---

## Lectuer 18: Segmentation

### Clustering-based Segmentation - Mean Shift

- Mean Shift 굉장히 많이 씀. 알고 있으면 좋음.

p.5
- non-parametric 대표 사례 : 히스토그램
  - 히스토그램
  - 단점1 : support(density가 0이 아닌 곳)를 알아야 함. 그런데 support를 정확히 알기 쉽지 않음
  - 단점2 : dimension이 올라가면 히스토그램 쓰기가 어려움. 고차원 데이터에서는 쓸 수가 없다.
  - 장점 : 간단하다. counting만 할 줄 알면 된다.
- x_i : 히스토그램의 센터


p.6 Mean Shift Algorithm
- mode: local maximum
- Maen Shift는 기본적으로 mode-seeking algorithm이다.
- mode를 찾은 이후에는 mode가 같은 값끼리 clustering 하면 된다.


p.7~
- region of interest로써 윈도우를 정한다.
- 가장 dense한 지점으로 이동한다.

p.14
- x: 현재 center
- x_i : center 주변의 점들
- m(x) : 각 x_i에 대한 weighted mean
  - 현재 센터와의 거리를 구해서
  - 센터에 가까운 점들은 weight를 크게 준다.


p.16 Attraction Basin
- 모든 데이터 포인트가 clustering 한다.


p.18
- 커널 : 가우시안 쓰면 된다.
- bandwidth 잘 선택해야 한다. window 원을 조그맣게 정하면 그 지점에서 clustering을 해버린다.
- h (kernel size)가 크면 원이 크게 잡히고 h가 작으면 원이 작게 잡힌다.
- h가 너무 작으면 그 데이터 지점 자체가 mode가 되어 수렴된다.
- h가 적당 값이면 점점 이동하면서 mode를 찾는다.
- h를 너무 크게 잡으면 mode의 개수가 극단적으로 적어진다.


### Bondary-based Segmentation - Watershed

- over segmentation 용도로 사용한다.
- 아주 많이 쓰이는 것은 아니므로 빠르게 넘어감
- minimum에서 물을 채워서 범람할 때 댐을 만든다. 이 댐이 watershed line이다.

p.25
- catchment basin : 물을 떨어뜨렸을 때 가장 아래로 모이는 minimum 지점
- watershed line : 물을 떨어뜨렸을 때 동일한 확률로 서로 다른 곳으로 갈라지는 부분

p.28
- 장점 : 빠르다
- 단점 :
  - gradient 이미지의 정확도에 따라 결과가 정해진다.


### Graph-based Segmentation - Ncuts

- 그래프를 만들어야 한다.

p.30
- 이미지의 각 포인트를 node로 정한다.
- 픽셀 페어의 similarity(픽셀 사이의 거리)를 구한다.
- weighted 그래프를 만든다.
- 이미지 크기: 200 * 200 = 40000
- 에지 : 40000 * 40000

p.31
- 가장 이상적인 sigma는 가운데 이미지의 sigma
- 가까운 픽셀일수록 1, 멀수록 0
- sigma를 크게 주면 가까운 픽셀만 non-zero이고 나머지는 몽땅 0이 된다.

p32~
- cut : 다른 클러스터의 weight를 최소화한다.
- low cost인 것을 cut한다.
- 비슷한 픽셀은 같은 segmentation에 있을 확률이 높다. 비슷한 픽셀은 weight가 크므로 잘릴 확률이 적다.
- mincut : minimum cut을 찾겠다
  - A, B : 그래프가 A와 B로 나눠지길 바란다.
  - A와 B라는 다른 클러스터에서 오는 노드들 사이의 weight가 최소가 되도록 cut하겠다.
  - 가까운 픽셀은 wieght가 크므로 가까운 픽셀 사이를 cut하면 cost가 커질 것이다.
  - 사각형 그림을 봤을 때 A와 B를 제외한 엷은 하늘색의 면적의 크기가 최소가 되도록 cut하겠다.

p34
- 문제점 : 가장 멀리 떨어져 있는 하나만 자르는 것이 cost가 제일 적다. 따라서 그것을 권장하게 된다.
- 해결책 : 세그먼트 사이즈를 normalize하면 위 문제점의 경우대로 했을 때 cost가 커지게 된다.
- Ncut : A와 B가 비슷할 때 가장 좋다.


p.35
- volume(A) : A 면적 + A 오른쪽 면적의 합
- association : rec


p.36
- 레일라이(rayleigh) quot를 미니마이즈 하는 것과 같다.
- 아이겐 밸류 :
  - 구글의 페이지랭크
- normalized cut의 목적함수가 무엇인지 아는 것은 중요하다


p.38
- cut이 이미지 boundary로 가기 때문에 artifact가 생긴다.


p.39
- 단점 :
  - 너무 느리다. K가 올라갈수록 계속 잘라줘야 함.
  - normalize를 강하게 주다보니 세그먼트가 너무 equal하게 됨.
- 시간이 오래 걸리고 이미지 바운더리 artifact가 생겨서 요즘은 잘 안 쓴다.
- 요즘은 다 딥러닝으로 한다.




---

## Lecture 17: Grouping and Clustering

### Gestalt grouping

p.11
+ 사람은 이 그림을 보면서 자동으로 그룹핑을 한다.
+ 그리고 개를 떠올린다.
+ 무형의 검은색으로부터 그룹핑을 해서 물체로 인식을 하는 것.
+ 딥러닝이 잘 되는 것도 이런 것을 흉내내서 잘 되는 것이다.


p.13 Gestalt Cues를 하는 이유
- 사람이 그룹핑을 하는 기본 원리를 알 수 있기 때문
- occlusion reasoning에 사용되므로


### Clustering: K-means/Agglomerative/Spectral

+ 클러스터링 알고리즘 수만 개
+ 많이 해봤겠지만 여전히 잘 안 됨

p.15 Clustering 알고리즘에 대한 간단한 소개
- 하나의 토큰으로부터 유사한 것을 그룹핑
- 챌린지
  - 무엇이 유사한 것인지 기준(of similarity)이 필요하다.
  - similarity를 정한 이후 목적 함수가 있어야 한다.


p.19 K-means 클러스터링
- (1) 클러스터 개수 K를 정한다.
- (2) 포인트 K개를 랜덤하게 선택한다.
- (3) 각 포인트는 클러스터 센터가 된다.
- (4) 센터에 가까운 포인트를 각 센터에 할당한다 (클러스터 멤버십 업데이트).
- (5) 같은 클러스터에 속한 포인트들의 평균(mean)을 구해서 클러스터 센터를 새롭게 업데이트한다.
- (6) (4)~(5)를 반복한다.


p.18
- p.19에 있는 내용이 곧 p.18의 수식과 같다.
- 수식을 minimize하는 c와 delta를 찾겠다.
- c = center
- j번째 데이터가 i번째 center에 대입했을 때 그 거리를 최소화하는 cluster center와 delta를 구하겠다.


p.21
- initialize가 중요하다.
  - 랜덤하게 K개를 선택하든지
  - residual을 최소화하는 K개를 선택하든지


p.23 distance measure
- x_i : distance
- City Block : 점을 움직여서 거리를 구한다. 점을 움직일 때 사각형 형태가 되므로 city block이라 한다.


p.26~ Agglomerative Clustering
- threshold를 통해 tree 값을 구할 수 있다.
- ex. 3개의 tree를 만들고 싶다면 threshold 값으로 0.8을 선택하면 된다.


p.32
- Good : hierarchy = dendrogram tree
- 총평 : hierarchy가 필요한 경우가 아니면 웬만하면 쓰지 마라.


p.33
- Spectral : frequeyncy 관련, 아이겐벡터, 아이겐밸류 관련
- 그래프로부터 데이터를 만들자


### Image segmentation

+ 클러스터링을 컴퓨터비전에서 배우는 이유는 segmentation 때문이다.

p.36 이미지 분할
- 여기서는 컬러로 분할했음


p.39
- 백그라운드가 균일하기 때문에 깔끔하게 나온 것
- 색깔이 섞여 있다면 이렇게 깔끔하게 나오지 않음
- 잘된 것만 보여준 것이고 실제로는 segmentation은 정말 잘 안됨.
- segmentation은 image classfication과 달리 사람의 수작업으로도 하기 힘듦. 일일이 클릭해야 함.
- segmentation은 조금만 오류가 나도 치명적으로 느껴지기에 상품으로도 만들기 어려움.


p.40 segmentation 하는 이유
- Super Pixels : 필요 이상으로 오버 segmentation 하는 것
  - 200만 개 픽셀을 2000개 픽셀로 줄여서 segmentation 할 수 있음


p.42 segmentation은 bottom-up과 top-down 방식이 있다
- bottom-up : 색깔이 비슷한 것끼리
- top-down : 같은 물체끼리
- 얼룩말의 경우 bottom-up으로는 불가능하고 top-down으로 해야 한다.
- 그런데 얼룩말인지 어떻게 알 것인가가 결국 어려운 문제

**끝.**


---

## Lecture 13: Stereo I (Lecture 16 다음 순서)

### Camera Model

+ 나중에 함

### Binocular Stereo

p.9
+ 인간의 눈 2개: 3차원을 이해하기 위해.

acclude

p.10~15
+ 이미지 한 장만으로는 알아낼 수 없음
+ 그래서 사람은 shading을 사용하여 입체감을 느낀다.
+ Texture를 통해 입체감을 느낀다.
+ Focus를 통해 느낀다.
  + 앞에 나무가 뒤의 건물을 acclude하고 있다. 나무가 가까이 있다는 걸 알 수 있다.
+ Motion으로 느낀다.


p.16
+ 두 이미지로부터 스테레오를 만든다.
+ depth를 알아내야 한다.
+ 스테레오에 관심 있는 이유 : 우리 눈이 2개이므로.
+ 무조건 눈이 많을수록 multi-view일수록 3차원을 인식하는데 도움이 된다.


p.18
+ 작은 망원경이라도 없는 것보다 낫다. 눈이 1개인 것보다 2개인 게 낫다.


p.20
+ 컨버징 포인트
+ C와 P가 사람 눈의 image plane에 어떻게 찍히는지 보자.
+ Left Eye : C는 P의 왼쪽에 있음
+ Right Eye : C는 P의 오른쪽에 있음
+ 그래서 3차원 정보를 인식할 수 있는 것이다.
+ 숫자로 계산하면 망막의 지점을 0부터 100까지 있다고 했을 때
+ 왼쪽 눈과 오른쪽 눈에 찍히는 C의 지점을 합치면 disparity > 0이 생긴다.


p.23
+ 여러 장의 사진을 찍어서 depth를 알아낸다.
+ depth를 색으로 나타냄
+ 하얀 색 : 가장 가까움
+ 그런데 이미지로 3D 정보를 알아내는 것은 어려움
  + correspondent point를 자동으로 찾는 것이 어렵기 때문.


### Other 3D Methods

p.2
+ 그래서 3D 정보를 알아낼 때 이미지가 아니라 Active Streo를 쓰는 것이 대세이다.


p.3 레이저 스캐닝
+ 설계도가 없는 문화재도 새로 만들 수 있도록 레이저스캐닝을 통해 3D 정보를 알아낸다.


p.6
+ 사람 눈에 보이지 않는 IR을 쏜다.
+ 동그라미 패턴을 쓴 이유 : correspondent를 빠르게 찾기 위해
+ 왜 빠르게 찾을 수 있는지는 특허라서 알 수 없음
+ structured light이 아닌 prime sense(?)

끝. (다음 시간 segmentation)

---

## Lecuter 16: Lukas-Kanade Tracking (루카스-카나데, 최초의 tracking algorithm)

### Optical Flow

Spatial Coherence
- 포인트만으로는 coherence를 알 수 없으니 area-based로 보자.


Temporal Persistence
- small motion과 비슷한 맥락


### Lucas-Kanade algorithm (Translation, 기본 아이디어)(수치해석, 루트파인딩 관련)

루트파인딩을 하는 이유
- optimization에 중요하므로.
  - 미분이 0이 되는 지점 찾기 => 결국에 루트 파인딩


Netown's method p.10
- Taylor expansion
  - x_0을 잡았을 때 x_0에 대응되는 곡선의 점이 아니라 근사한 라인의 점을 잡는다.
  - 1차 미분만 구하면 쓸 수 있다.


General Problem of Image Registration p.13


p.16
- template이 u와 v 지점에 있을 때


p.20 단점
- 시간이 지남에 따라 template은 변하는데도 불구하고 하나의 view-point에서 본 template만 가지고 tracking을 한다.
- Generalize : 그래서 template을 바꿔가면서 tracking 한다.
  - p : parameter도 구해야 한다.


### Lucas-Kanade algorithm (General)

p.22
- affine이라면 p가 6개가 된다.


p.23
- 마름모꼴로 표현하는 이유:


p.24
- p를 찾는 것이 곧 u와 v를 찾는 것이다.
- W(x;p)의 의미 : W(x) 함수는 parameter로 p를 가지고 있다.


p.26
- taylor expansion
- 역삼각형: gradient


p.27
- Jacobian : 편미분을 계속
- 딥러닝 : 계속 미분을 한다.


p.29
- 오타 : x-> W_x, y -> W_y
- 오타 : (1+d_{xy})y -> (1+d_{yy})y


p.

---

## Lecture 15: Optical Flow (비디오 관련된 것)

가장 중요한 슬라이드
- p.12 Equation
- p.16, 17, 18 Aperture Problem


Optical Flow
- **똑같은 픽셀이 어디로 움직였느냐**
- Motion Field를 통해 알아낼 수 있다.
- 이미지 상의 벡터
- 모든 픽셀에 대해서 벡터의 변화를 알아낸다.
- 그러면 segmentation이 편해진다.
- 자동차는 기본적으로 강체이다. 물렁물렁하지 않다.
- 자동차가 v의 속도로 가면 자동차에 속하는 모든 것도 v로 변화한다.
- 자동차는 강체이므로 자동차를 이루는 모든 픽셀은 v로 변화해야 하지만 관점에 따라서 다를 수 있다.


Optical Flow and Motion (p.3)
- 자동차의 실제 속도보다는 보이는 관점에서의 속도가 관심사이다.
- camera jitter : 영상의 흔들림을 없애준다. (feature의 correspondent를 찾아서 해결)


Tracking - Rigid Objects와 Non-rigid Objects
- 자동차 : Rigid
- 사람 : Non-rigid


Motion Field
- scene에서 각 포인트의 특정 속도


Optical Flow != Motion Field 항상 같지는 않다.
- 당구공이 가운데 축을 두고 회전한다
  - motion field 있음
  - optical flow 없음


Problem Def. Optical Flow (p.11)
- Optical Flow 어떻게 알아낼까?
- 각 포인트의 correspondent를 찾는다.
- 핵심 가정이 필요하다.
- 그런데 물체가 프레임 안을 벗어나버리면 트랙킹에 실패한다.


오타 p.12
- 파셜t -> dt
- E_{x} : E를 x로 평균을 냈다.
- E_{t} : brightness에 대한 변화
- 오타 : u와 v를 바꿔야 함 (일반적인 표기상)


p.13
- 옵티컬 플로우가 이해 안되면 이 그림을 봐라.
- E_{t}(3, 3) = 3 - 4 = -1


p.14
- discrete하게 gradient를 구한다.


p.19
- v: y축의 변화 속도
- x: x축의 변화 속도
- 오타 : u와 v를 바꿔야 함 (잘못되어 있음)


p.20 Area-based Method
- 패치를 잡고 패치가 어느 방향으로 바뀌는지 살펴본다.


p.23
- 되도록이면 texture가 다양한 방향을 가진 것으로 골라야 한다.



---

## Lecture 12: Homography and Image Warping

### Image Mosaicing 이미지 모자이싱

이미지 모자이싱
- 여러 장의 사진을 찍어서 겹치는 부분을 잘 처리해서 하나의 사진으로 만드는 것


베이직 프로세싱
- (2) interest points(feature)를 뽑는다.
- (3) 코너와 가장 가까운 correspondence를 찾는다.
- 잘못 찾아서 outlier를 찾으면 RANSAC으로 처리한다.


이미지 리프로젝션
- pp : project plane


p.14 호모그래피
- T 행렬의 요소인 unknown 9개를 찾는 것 (i=1이면 unknown 8개)


### Compute Homography

p.18
- correspondent를 구한 후 tx, ty만큼 이동시킨다.


p.19
- 평균을 내는 이유: correspondent가 실제로는 정확하지 않고 떨림이 있기 때문이다.
- 마치 line fitting과 비슷하다.


p.23 오타
- xt -> tx, yt -> ty


p.27
- correspondent 1개에 대한 식


### 2D Image Warping

p.29
- 오리지널 이미지에 행렬 T를 적용하는 것이 아니라
- T의 인버스를 구해서 오리지널 이미지의 픽셀을 카피한다.
- Forward 하지 말라는 이유 : (1,1)을 Transformation했을 때 정수의 값으로 떨어지지 않을 수도 있다.
- 실수로 나오면 나눠줘야 하는데 (splattig) 굉장히 복잡함.
- inverse warping이 더 간단하다. (interpolation을 먼저 하는 것이 더 간단하므로)


p.35 좌측 이미지를 우측 이미지로 만들었다.
- 어떻게?


p.37
- 우측 이미지에서 기둥처럼 보이는 것은 사람 다리임


p.39
- 이미지 랙티피케이션은 굉장히 많이 쓰인다.
- 항공 사진도 그렇다.
- 항공 사진을 찍을 때 몇 도 기울여졌는지 센서(오도매트릭)가 있으므로 그 정보를 활용하면
- 이미지 랙티피케이션을 할 수 있다.
- 실제로는 correspondent를 찾는 것이 어렵다.
- 찾기만 하면 Matlab의 코드 한 줄로 풀 수 있다.


**오늘 수업 끝.**






---

## Lecture 11: Image Alignment

### Image Alignment

Paper에 발표되는 vision의 결과물
- ex. 고흐 화풍으로 그림 바꾸기
- 거기 시간은 안 적혀 있는데 실제로는 200초 이상, 약 4~5분 걸린다.
- paper에서 나온 거를 기자들이 과장하는 면이 많다.
- 무언가 paper에서 발표되면 '누군가가 최초로 시도했구나' 정도로 이해해야 한다.
- 아직 해야 할 게 많다.


중요한 건 자기가 하고 싶은 일을 오타쿠처럼 하면서 좋은 사람들을 모아 변화를 만드는 것
- ex. 딥 마인드 하사비스 - 바둑 - 아자 황(몬테카를로 박사 학위) - 데이비드 (? RL 권위자, 친구였음)
- 그게 바로 innovation
- 그래서 여러 가지를 공부하고 찾아봐야 됨.
- 아, 한계가 뭐구나, 아 내가 생각한 것을 이런 기술로 해결할 수 있겠구나.
- 다른 사람들이 인정해주지 않아도, 비웃어도 해야 한다.
- 그리고 몇 년을 해야 한다.
- 알파고도 매우 오래 전부터 비전을 갖고 노력해서 만든 것

p.3
- 똑같은 이미지인데 rotation되어 있음
- 여기서 transformation은 rotation scale이다.
- 어떻게 찾을까?
- matching pair를 찾는다. 빨간점-빨간점 등
- 그러면 T를 구할 수 있다.


p.5
- image alignment를 하는 이유?
- 첫 번째 : recognition을 위해.


p.7 이미지 얼라인먼트 어프로치 2가지
- Pixel-based: 픽셀의 correspondent를 찾는다.
- Feature-based: 예를 들어 집의 가장 자리, 코너와 같은 특징을 찾는다. (일반적으로 많이 사용하는 방법)


p.8
- alignment : T를 찾는다.
- warping : 이미지를 바꾼다.


p.11
- global : 모든 픽셀에 대해서 동일한 T를 적용한다.


p.14
- shear : 찌그러트리기


p.14~15
- 매트릭스의 곱으로 나타낼 수 있다.
- 매트릭스의 곱에 집착하는 이유: 여러 가지 T가 있을 때 한꺼번에 적용하려면 T끼리 곱하면 바로 해결되기 때문.
- 결국 T는 언제나 하나의 매트릭스의 곱으로 표현할 수 있다.

p.20
- Affine : T를 Linear combination한 것


p.21
- 가장 일반적인 형태
- i는 1로 고정해도 상관없다. 어차피 w'로 나눠줄 것이기 때문.


### RANSAC

p.24
- 먼저 어떤 Transformation을 구할지 정한다.
- Coordinates에 대한 Correspondent를 찾는다.
- Outlier : 잘못된 correspondence
- 첫번째 창문과 세번째 창문을 같은 correspondence로 오해할 수 있음.
- outlier는 parameter estimation에 치명적인 오류를 낳는다.


p.25~26
- p.25에 아웃라이어 하나 추가했더니 선이 바보가 됨.


p.27 RANSAC 랜삭
- 목표 : outlier의 임팩트를 피할 수 있는 parameter estimation을 생각해보자.
- 인튜이션 : outlier가 추가되면 라인을 support(일치)할 수 있는 점이 적다.
- 이 알고리즘은 outlier와 inlier의 비율에 따라 성공 여부가 정해진다.


p.39
- 선을 랜덤으로 선택하고 인라이어를 세본다.
- 아웃라이어 : 빨간색 2개
- 인라이어 : 파란색 5개

**끝.**

---

## Lecture 05: Edge detection

@@@프린트에 필기했음

---

## Lecture 09: Image Formation and Optics

### A Brief History of Images 카메라의 역사

2가지 반사
- 물체 고유에 대한 반사 material 반사
- 물체가 움직일 때마다 작용하는 반사 glossive 반사


물체마다 반사의 비율이 다르다
- ex. 금속 : glossive 반사 비율이 높음


최초의 네거티브 이미지
- 카메라 옵스큐라에 실버 솔트를 둔다.
- 실버 솔트는 빛이 많이 들어오는 부분은 검은색이 되고 그렇지 않은 부분은 하얀색이 된다.


1826 빛에 서서히 변하는 물질 발견
- 8시간 동안 빛에 노출
- 사진은 결국 빛에 반응하는 물질을 어떻게 만드느냐가 핵심


1837 드게로
- 드게로 타입 : 은판사진법
- 사진판에 화학적 성분을 섞음


1841 윌리엄 헨리 폭스 털봇
- 필름판의 시초
- 필름판은 기본적으로 네거티브함


1861 세계 최초의 컬러 사진
- 맥스웰 공식을 만든 맥스웰
- tartan ribbon : 스코틀랜드 체크 무늬가 있는 리본


1868 대중적인 컬러 이미지를 처음 만듦


1878 르랜드 스탠포드
- 자기 아들 이름을 따서 학교 만듦: Stanford University의 전신
- 말이 달릴 때 네 다리가 동시에 공중에 뜨는 경우가 있는지 궁금해서 고속 카메라의 시초를 만듦
- 말이 달릴 때 일정한 간격으로 셔터 누름


1925 라이카
- 우리가 알고 있는 처음 카메라를 만든 라이카 회사
- 필름 포맷도 처음 만듦


1948 폴라로이드 즉석 카메라
- 폴라로이드 최초


1973 아주 혁명적인 CCD
- 덕분에 디지털 카메라를 만들 수 있음
- 빛이 들어오는 양에 따라 전압을 다르게 하여 전류를 보내줌
- CCD : 빛을 전기 신호로 바꾸는 광학 센서
- 노벨 물리학상 수상


이미징이 굉장히 중요하다.
- 생물을 관찰하는 방법
- (1) 죽여서 본다.
- (2) 살아 있는 물체에 대한 이미징


---

### 핀홀 카메라

p.21
- 빛을 측정할 수 있는 필름이 있다고 해보자.
- 기본적으로 모든 물체는 전 방향으로 반사한다.
- obeject의 온갖 포인트가 전 방향으로 반사되므로 필름에 reasonable하게 표현할 수 없다.
- 1대1 맵핑이 되지 않으므로.


p.22~23
- object에서는 전 방향으로 반사되지만 이것이 특정 barrier(=ray)를 지나면 특정 포인트만 필름에 입사된다.
- 필름 카메라는 이런 식으로 image plane을 만든다.


p.25 핀홀 카메라의 equation
- 삼각형이 유사하면 비율이 똑같다.
- 그 원리에 따라 핀홀 카메라의 equation을 끌어낼 수 있다.


p.26 Magnification
- plane을 눈 앞에 두고 (smaller z) 내가 움직이면 아주 크게 움직인다.
- plane을 멀리 두고 (bigger z) 내가 움직이면 아주 작게 움직인다.


p.27 핀홀의 크기는 어떻게 정할까
- 핀홀을 작게 주면 > 대다수의 빛을 막음 > 1 to 1 관계 명확 > sharp한 이미지, but 흐릿한 이미지
- 핀홀을 크게 주면 > 빛을 더 많이 통과 시킴 > 1 to 1 관계 불명확 > blur(주변에 대한 average)한 이미지


p.28
- 0.35mm 아주 명확
- 더 줄이면 또 불명확 : 왜? diffraction 때문!
- diffraction : 빛의 파동의 특성 때문에 아주 작은 구멍에서는 빛이 휘어가게 됨


---

### 3D to 2D

p.30
- 사진을 찍기 어려운 이유 : 실제 물체는 3D인데 2D로 나타내야 하므로
- 2D 사진을 3D로 복원하는 것도 어려움
- 선은 보존되지만 각도나 길이는 보존되지 않기 때문


p.32 Fronto-Parallel Planes
- Fronto-Parallel Plane : ex. 벽
- 비율과 길이가 보존된다.


p.33
- 소실점: 현실의 포인트가 이미지 plane에 맵핑될 때 z값을 무한히 늘리면 소실점이 된다.


p.34
- 공간에 있는 각 direction은 모두 자신만의 소실점을 가지고 있다.


p.36
- ground plane은 camera center의 horizon과 만난다.
- 카메라보다 높은 포인트는 horizon 위에 찍힌다.


p.37
- (1) camera center보다 pole이 아래에 있다.
- (3) pole의 밑둥이 내 눈보다 위에 있으므로 pole은 공중에 떠있는 것이다.


p.44
- 구가 타원으로 보이는 이유


p.46
- Da Vinci는 Perspective distortion을 고려해서 그림을 그렸다.

---

## Lecture 10 : Image Formation and Optics II

### Projection Matrix 이미지 plane 상의 좌표와 실제 오브젝트의 좌표의 관계

p.4~5
- linear 하지 않다 : 하나의 매트릭스 multiplication으로 표현할 수가 없다.
- homogeneous coordinates :
  - 1을 붙여서 표현을 하고 시작한다.
  - 매트릭스 multiplication을 한다.
  - 다시 원래 좌표로 돌리려면 맨 마지막 값을 1로 바꿔야 한다.
  - 결국 마지막 값으로 나머지 좌표 값을 나눠주면 된다.
- Perspective projection Matrix
- 3-D point : 세상에 있는 물체에 대한 포인트
- 2-D point : 이미지 plane의 포인트


p.6~7
- perspective projection에 따르면 심시티 이미지에서 가까운 것이 멀리 있는 것보다 더 커야 한다.
- 그런데 그렇지 않다.
- 심시티 이미지가 실제로 언제 가능할까? 인공위성에서 지구를 보듯 아주 먼 곳에서 볼 때.
- 인공위성의 관점에서 보면 서울대학교의 모든 건물들의 거리 차이가 아주 작기 때문이다.
- 이러한 현상은 z가 delta z보다 클 때 발생한다.
- 즉 이러한 현상에서는 perspective 효과가 거의 무시된다.


p.10
- Geometric Computer Vision
- 로봇 공학
- 세상에 있는 3D 포인트를 이미지 plane에 맵핑하는 방법


---

### Camera with Lenses

p.12
- 이상적인 렌즈의 역할 : object의 포인트에서 반사되는 모든 빛을 필름에서 하나의 포인트로 모아주는 것
- 핀홀에서는 카메라 센터 밖의 빛은 막아주고 카메라 센터를 통과하는 빛만 허락했지만
- 렌즈는 카메라 센터와 밖의 모든 빛을 하나로 모아준다.


p.19
- Aperture,어파쳐, 조리개
- 어파쳐 : 렌즈의 다이어미터로써 빛의 exposure를 조절한다.
- F-number : focal length에 대한 비율, 조리개를 여는 비율


p.21
- 인포커스 아웃포커스
- 물리적으로 일어날 수밖에 없는 현상
- Depth of Field : 포커스가 맞는 거리
- depth of field는 apature로 조절한다.
- 조리개를 크게 열면 허용되는 반사각이 커지므로 blur circle이 커지고 아웃포커스가 흐릿해진다.
- 조리개를 줄여주면 허용되는 반사각이 작아지므로 아웃 포커스였던 이미지도 sharp하게 나온다.


p.24~25 광각
- Field of View
- VR에서 가장 critical한 개념이기도 하다.
- field of view를 줄이면 각도가 더 좁은 지점을 catch한다.


p.26
- field of view와 거리와의 관계
- 멀리 가서 field of view를 줄이든지 가까이가서 field of view를 늘리든지 물체의 비슷한 영역이 사진으로 나온다.
- 단, 가까이 가서 광각으로 찍으면 perspective distortion이 커진다.


p.28
- 영화 테크닉 Dolly zoom 달리 줌

### Lens Flaws 렌즈 오류

p.32
- 빛이 굴절한다.
- 파장이 다르면 다른 focal plane이 도달한다.


p.34 비그네팅
- 사진의 가장 자리일수록 어둡다.
- 왜냐하면 렌즈를 통과한 후 CCD의 바깥 쪽에 모이는 빛은 손실되기 때문이다.


p.35
- calibration이 필요하다.


p.36
- 렌즈의 비균일성 때문에 reflection이나 scattering이 일어난다.
- 비싼 렌즈에서는 어느 정도 해결된다.


p.37
- 빛을 전기 신호로 바꿔준다.


p.39
- CCD는 sensor array이기 때문에.


p.41
- 밤에 찍은 사진은 노이즈가 많다.
- 이건 trade-off인데 노이즈를 줄이려고 하면 밤 사진이 매우 어둡게 나온다.


p.42
- 디지털 카메라로 사진을 찍으면 artifact가 생기기 마련이다.
- 그런데 이것 역시 trade-off로 압축하지 않으면 파일 사이즈가 너무 커지기 때문이다.
- white balance : 조명의 영향 때문에 흰 색이 어쩔 수 없이 노르스름하게 나온다. 보정 가능하다.



**끝.**

---

## Lecture 02: Image Processing

### 1. Digital Image Processing

@@@ resume



---



---

## Lecture 01 - Introduction to Computer Vision

### 1. Introduction to Computer Vision

### Computer vision이란 무엇인가 (1)

+ Teach machines to do what we can do with vision
+ 사람이 시각으로 할 수 있는 것을 기계에게 가르쳐 주는 것

### Human Vision은 무엇을 할 수 있는가

+ 사람, 사물 인식하기
+ 장애물을 뚫고 지나가기
+ 분위기 감지 및 이해하기
+ 사진이나 그림을 보고 스토리 상상하기

### Human Vision이 완벽하지 않은 이유는 무엇인가

+ 착시를 겪는다.
+ 디테일을 무시한다.
+ 세상에 대한 묘사가 애매하다(Ambiguous description of the world).
+ 정확성이 부족하다.
+ 전부 기억하지 못한다(Limited memory)

> **Note:** 착시는 눈의 문제가 아니라 머리의 문제이다.

### 착시가 발생하는 이유 ::: Checker Shadow Illusion - E. H. Adelson

+ 사람의 눈은 시신경에 edge를 detect할 수 있는 부분이 제일 먼저 붙어 있다.
+ 따라서 사람의 눈은 차이에 민감하지만, 정확도는 떨어진다.

> **Note:** `edge` : 색이 급격히 변하는 부분 또는 경계

### Computer Vision에 대한 다양한 정의

+ 기계에게 사람의 시각으로 할 수 있는 일들을 가르쳐 주는 것 Teach machines to do what we can do with vision
+ 시각적 현상을 지능적으로 해석하는 것 Intelligent interpretation of imagery
+ 우리 뇌에서 시각을 담당하는 부분을 인공적으로 만드는 것 Building an artificial **Visual Cortex**
+ 사람처럼 빛을 측정해서 세상을 관찰하는 것이 아니라 거꾸로 이미지를 보고 세상을 이해하는 것(?) Inverse optics

> **Note:** Visual Cortex : 우리 뇌에서 시각을 담당하는 부분, 시각 피질, 시신경으로부터 자극을 전달 받는 대뇌 피질의 부분

### Computer Vision의 수준별 작업

#### Low-level

+ 이미지 >> 이미지
+ e.g. image processing, edge-detection, optical flow computation
+ e.g. 흔들림 보정(deblurring)

#### Mid-level

+ 이미지 >> 특징 Features
+ e.g. boundary detection, segmentation, structure from motion

#### High-level

+ 이미지 >> 의미 Semantics
+ e.g. object recognition, scene understanding
+ e.g. Image classification, Object detection, Image captioning


> **Note:** Image captioning : 이미지 캡셔닝이란, 이미지에 대한 설명을 작성하는 것이다.

### Computer Vision vs. Image Processing

#### Image Processing (IP)

+ input과 output이 이미지이며, 이미지의 transformation에 대해 연구한다.
+ 이미지 압축, 이미지 복원, 이미지 개선

#### Computer Vision

+ 이미지 프로세싱 기술을 적극 활용한다.
+ output이 이미지에 대한 묘사 또는 해석이다.
+ 이미지를 갖고 고차원 지능 (high-level intelligence) 활동을 한다.

### Computer Vision이란 무엇인가? (2)

+ An inverse processing of the forward process of image formation and graphics
+ 이미지가 생성되는 과정을 거꾸로 거슬러 올라가는 과정

**끝.**

## 2. Topics covered

### 이미지 프로세싱에서 다루는 개념

+ 푸리에 변환 Fourier Transform
+ 샘플링 Sampling
+ 컨볼루션 Convolution

+ 이미지 개선 Image enhancement
+ 특징 발견 Feature detection

### 음영처리로 3D 이미지 얻기

+ 음영처리로 형태 얻기 Shape from Shading
+ 입체적인 광도 측정 Photometric Stereo

> **Note:** 원제: 3D from Shading

### 이미지 워핑 및 포토 모자이크

+ 각도나 시점이 다른 이미지 뒤섞기

> **Note:** 원제: Image Warping and Photo Mosaics

### 광학 흐름

+ 사물의 각 포인트가 다음 frame에서 어떻게 움직이는가
+ ex. 두 개의 포인트 동시 이동하면 같은 물체라고 추측 가능

> **Note:** 원제: Optical flow

### 트랙킹

+ 이미지의 이동을 추적하고 예측하기
+ ex. 자율주행자동차는 사람이나 자동차의 움직임을 추적하고 예측해야 함

> **Note:** 원제: Tracking

### 이미지 기하학

+ 한 물체를 여러 각도에서 사진을 찍어서 물체의 3차원 모형 알아내기

> **Note:** 원제: Image Geometry

### 두 눈으로 보는 입체

+ 이미지 속에 있는 물체의 거리(depth)를 알아내기

> **Note:** 원제: Binocular Stereo

### 얼굴 인식

+ 이미지에서 얼굴 인식하기
+ Principle Components Analysis (PCA, 주성분 분석)이 전통적인 방법이나 요새는 딥러닝을 이용하는 것이 대세

> **Note:** 원제: Face Recognition

### 이미지 분류

> **Note:** 원제: Image Classification using Classifiers

### 딥러닝

+ CV(Computer Vision)에서 딥러닝의 효용성은 매우 큼

**끝.**

---
