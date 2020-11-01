---
title:  "kaggle MoA 대회 (2) - Label Smoothing"
excerpt: "개념 공부"

categories:
  - AI
tags:
  - Blog
use_math: true
last_modified_at: 2020-11-01
---
>## Label Smoothing

* Label Smoothing을 하니 0.1860 → 0.1845로 상승
* 예전 대회에서 Label Smoothing을 했지만, 별로 상승되지 않았기에 제대로 알아보기 위해 검색

	* 출처 자료 1: <https://si-analytics.tistory.com/21>
	* 출처 자료 2: <https://ratsgo.github.io/insight-notes/docs/interpretable/smoothing>

> ### What is Label Smoothing?

$$
y_{k}^{LS} = y_k(1-\alpha) + \alpha/K 
$$

* Szegedy 논문에서 소개 2016년
* 기본적으로 One Hot encoding된 Hard Label을 Soft Label로 바꾸는 것(0과 1사이의 값)
* $K$개의 클래스에 대해 Smoothing Parameter $\alpha$ 적용
	* y2_hard_label = [0, 0, 1, 0, 0]
	* y2_soft_label = [0.02, 0.02, 0.92, 0.02, 0.02]

> ### Label Smoothing 장점

* 예측 시 정답 예측을 위한 최대 Logit이 지나치게 커지는 것 방지 (overfitting 방지)
* 정답 예측과 오답 예측 사이에 '동일한 거리'에 있으면서 멀게 만드는 효과
	* Label Smoothing을 하면 오답 범주도 위와 같이 uniform 한 확률값을 부여 받기 때문

> ### Label Smoothing이 잘 통하지 않을 때
* Knowledge distillation에 부적합하고, 그 이유는 정보 손실
* 잘 이해가 안 가므로 나중에 다시 확인 필요