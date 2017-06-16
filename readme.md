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

# I. 강의록

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
