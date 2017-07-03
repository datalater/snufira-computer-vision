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



---

# Lecture 05: Edge detection

@@@프린트에 필기했음

---

# Lecture 09: Image Formation and Optics

## A Brief History of Images 카메라의 역사

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

## 핀홀 카메라

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

## 3D to 2D

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

# Lecture 10 : Image Formation and Optics II

## Projection Matrix 이미지 plane 상의 좌표와 실제 오브젝트의 좌표의 관계

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

## Camera with Lenses

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


**끝.**

---

# Lecture 02: Image Processing

## 1. Digital Image Processing

@@@ resume



---



---

# Lecture 01 - Introduction to Computer Vision

## 1. Introduction to Computer Vision

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
