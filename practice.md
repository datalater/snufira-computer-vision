
TA 실습시간



---

## 용어

+ `ROI` : region of interest

---

## 0719 Object Classification

Visual Words : dense SIFT는 128차원의 벡터로 되어 있는데 이것을 하나의 숫자로 표현한 것


---

## 0712 (1) Clustering, Segmentation

### K-Means Clustering

step1) 랜덤하게 센터 2(K: 클러스터링 개수)개의 점 선택
step2) 각 중심점으로부터의 거리를 계산하고, 센터에 가장 가까운 점들에 label을 매긴다.
step3) 각 label에 해당하는 모든 점의 '**평균(K-Means)**'을 계산하여 평균에 해당하는 점을 센터로 바꾼다.
step4) step2와 step3을 반복하다가 센터가 움직이지 않으면 멈춘다.

### Watershed Algorithm (Segmentation)

+ 각 이미지의 픽셀 값을 높이로 생각
+ 높이가 높은 것은 경계선
+ 높이가 낮은 것은 이미지
+ 물을 점점 채워서 높이가 낮은 것은 날려버리고 높이가 높은 것만 남긴다


## 0712~0719 (2) Features

### Feature Extraction & Matching

- feature : 이미지 내 salient(가장 핵심적인) point
- feature를 뽑는다 : feature를 describe할 수 있는 벡터 값을 알아낸다.
- 그 중 128차원의 벡터를 뽑아내는 알고리즘을 SIFT라고 한다.
- SIFT는 feature를 뽑아내는 것과 뽑아낸 feature를 128차원의 벡터 값으로 변환하는 것을 한다.

### SIFT (key point & descriptor)

#### 1단계 :: 라플라시안 피라미드로 key point 찾기

+ 이미지에 라플라시안 피라미드를 적용해서 두드러지는 픽셀을 찾아낸다.
+ 그 픽셀이 바로 key point가 된다.
+ 오리지널 이미지의 key point는 찾았지만, 변환된 이미지에서 key point가 어디있는지 알려면 key point의 descriptor가 필요하다.

#### 2단계 :: key point의 descriptor 구현하기

+ key point 픽셀을 중심으로 16 by 16 범위에 있는 각 픽셀의 gradient 값을 구한다. (with sobel filtering)
+ 그러나 이대로 픽셀 관점의 값을 그대로 사용하지는 않는다.
+ 이미지 비교를 할 때 픽셀 관점은 patch 관점에 비해 비효율적이기 때문이다. 왜냐하면,
    + (1) 연산 복잡
    + (2) 좋은 표현 불가 (ex. 무늬)
+ 그래서 16 by 16 픽셀을 16개의 구간으로 크게 나눈다. (픽셀 관점 -> 패치 관점)
+ 한 개의 구간은 4 by 4 픽셀로 구성된다.
+ 한 개의 구간에 있는 4 by 4 픽셀의 gradient 값을 하나로 압축한다.
  + 압축할 때는 4 by 4 픽셀의 gradient값을 모두 더해서 8가지 방향을 가진 gradient, 즉 8차원 벡터로 바꾼다.
+ 16개의 구간에 대해 위 연산을 반복하면 8차원 벡터를 가진 16개의 구간을 일렬로 나열하면 128차원 벡터로 표현할 수 있다.
+ 따라서 key point의 descriptor가 128차원 벡터로 표현된다.

#### **Note:** 라플라시안 피라미드를 사용하면 주변 픽셀값을 비교할 수 있다

+ 이미지에 라플라시안 피라미드를 적용하면 주변 픽셀값들을 비교할 수 있다.
+ 라플라시안을 적용한 픽셀값은 minimum or maximum으로 나온다.
+ minimum or maximum 값을 가진 픽셀이 feature가 된다.
+ 따라서 모든 픽셀에 대해서 일일이 연산할 필요 없이 feature 픽셀만 쉽고 간단하게 뽑아낼 수 있다.

#### **Note:** 이미지 픽셀의 gradient 구하려면 sobel 필터를 적용하면 된다

+ 이미지에 soble filter를 적용하면 각 픽셀의 gradient값을 구할 수 있다.

---
