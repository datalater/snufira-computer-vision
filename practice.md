
TA 실습시간

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


## 0712 (2) Features

### Feature Extraction & Matching

- feature : 이미지 내 salient(가장 핵심적인) point
- feature를 뽑는다 : feature를 describe할 수 있는 벡터 값을 알아낸다.
- 그 중 128차원의 벡터를 뽑아내는 알고리즘을 SIFT라고 한다.
- SIFT는 feature를 뽑아내는 것과 뽑아낸 feature를 128차원의 벡터 값으로 변환하는 것을 한다.



---
