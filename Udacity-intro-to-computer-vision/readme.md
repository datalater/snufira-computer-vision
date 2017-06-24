ⓒ JMC 2017

**SOURCE**  
\- [Udacity, Introduction to Computer Vision](https://classroom.udacity.com/courses/ud810)  
\- [Udacity, Introduction to Computer Vision (YouTube) ](https://www.youtube.com/playlist?list=PLAwxTw4SYaPnbDacyrK_kB_RUkuxQBlCm)  

**RESUME**  
\- `https://classroom.udacity.com/courses/ud810/lessons/3490398568/concepts/34996085680923`

---

## Introduction

### Computer Vision의 목표

+ 컴퓨터 비전의 목표는 "**이미지를 해석하는 컴퓨터 프로그램을 만드는 것**"이다.
+ 왜냐하면 모든 이미지는 스토리를 담고 있기 때문이다.

### Computer Vision의 원리

+ 이미지를 입력한 후 이미지가 갖고 있는 의미를 끌어낸다.
+ Image-in, Meaning-out

### Computer Vision을 알면 좋은 이유

+ `이미지`가 쓰이지 않는 곳은 없다.
+ 카메라로 찍는 사진이나 비디오 등은 어느 기술에서나 쓰이기 마련이다.
+ 따라서 모든 산업 분야에서 이미지 처리는 점점 핵심 기술로 부상하고 있다.
+ 특히 이미지에서 정보를 끌어내는 능력이 중요하다.


> **Note:** `이미지` : 실제 보이는 이미지(images) + 추상적 이미지(imagery, ex. 어떤 시를 보고 떠올리는 이미지)

### Computer Vision에 기반을 둔 기술 영역

+ Surveliance 감시/감독
+ Building 3D representations 3D 모델링
+ Motion capture assisted 모션 캡쳐 (움직임 포착)

### Computer Vision을 적용한 사례 (최소 5~10년 전에 이미 상용화)

1. OCR (문자 인식, Optical Character Recognition)
    + 이미지 속 숫자나 문자에서 의미를 이끌어낸다.
        + ATM에서 수표 금액 인식
        + 우체국에서 우편번호 인식
2. Face Detection (얼굴 인식)
    + 모든 디지털 카메라의 얼굴 인식 기본 기능
    + 사람이 눈을 감았을 때 Blink Detected 메시지 띄우기
    + 사람이 웃을 때 사진을 찍는 SONY의 스마일 셔터
    + 본인 인증 로그인

3. Object Recognition (사물 인식)
    + 실시간 영상에서 사물을 인식한다.
        + 마트에서 손님이 캐셔의 눈을 피해 물건을 쇼핑카트에 넣어두고 그냥 지나치는 것이 큰 문제였는데 사물 인식 기계 LaneHawk를 개발하여 해결함.
        + 스마트폰 카메라로 어떤 랜드마크에 초점을 맞추면 그것에 대한 정보를 알려주는 AR 앱
        + 당신이 보고 있는 사물에 대한 정보를 알려주는 Google Glass

4. Special Effects and 3D Modeling (특수 효과 및 3D 모델링)
    + motion capture (영화 '캐리비안의 해적'의 특수 효과)
    + Earth viewers (Microsoft's Virtual Earth)

5. Smart Cars (스마트카)
    + self-driving cars (자율주행 자동차)

6. Sports
    + 미식축구 first down line 판독 (Sportvision)
    + 축구 오프사이드 판독

7. Vision-based interaction and games (시각 기반 상호작용과 게임)
    + 닌텐도 Wii
    + Microsoft Kinect(depth sensor로 skeleton infromation을 추출하여 유저 인터페이스 대폭 향상)
    + 사람이 손을 흔들면 그에 대응하여 손을 흔들어주는 로봇

8. Security and Surveilance (안전과 감시)
    + 공공의 안전을 위한 모니터링
    + Simense의 항구 모니터링 (선박 충돌 방지, 사람 배회 방지)

9. Medical Imaging (의료 이미징)
    + 3D imaging, MRI, CT
    + Image guided surgery (의사가 환자의 뇌를 수술할 때 두개골 속 이미지를 환자의 두개골 위에 보여준다. 벽에 영화를 보여주는 빔프로젝터처럼.)

### RESUME : `https://classroom.udacity.com/courses/ud810/lessons/3490398568/concepts/34996085680923`


---
