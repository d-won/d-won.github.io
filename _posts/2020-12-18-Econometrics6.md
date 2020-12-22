---
title:  "계량경제학 강의 6 (한치록)"
excerpt: "최소제곱을 이용한 가설검정"

categories:
  - Econometrics
tags:
  - Blog
use_math: true
last_modified_at: 2020-12-18
---

## 6장 최소제곱을 이용한 가설 검정

* 가설은 항상 모수에 관한 것이다. 모수에 관한 가설을 검정하기 위해 우리는 최소제곱 추정량을 이용할 것이다.
* 주어진 귀무가설에 대해 우리는 일정한 통계량(검정통계량)을 사용한다. 
* 이때 귀무가설 하에서 이 통계량의 분포를 알아야 하는데, 이를 위해서는 우선 최소제곱 추정량이 어떤 표집분포를 갖는지 알 필요가 있다.
* 4.10절에서는 4.3절의 가정하에서 최소제곱 추정량의 분포를 구한 바 있다. 

## 6.1 가설들
*선형 회귀모형에서 사람들은 일반적으로 기울기에 관심을 갖는다. 
*$\beta_1$이 0이라는 것은 독립변수가 종속변수에 평균적으로 영향을 미치지 않음을 의미한다. (귀무가설)
* 경우에 따라서 $X$와 $Y$에 자연로그를 취한후 그 기울기가 1인지 검정해 볼 수 있는데, 이 때 1이면 $Y$가 단위 탄력적이고, 그 절대값이 1보다 작으면 비탄력적, 그리고 절대값이 1보다 크면 탄력적이다. 
* 이처럼 $\beta_1=1$ 이라는 가설도 수요공급분석에 흥미로운 귀무가설이다.

> $\frac{\hat{\beta_1} - \beta_1}{sd(\hat{\beta_1})} \sim N(0,1)$

* 위 식을 보면, 좌변이 여러 항으로 구성되어 있따.
	* $\hat{\beta_1}$은 우리가 표본으로 부터 계산 가능하고
	* $\beta_1$은 우리가 모르는 기울기의 참값이며,
	* 분모의 표준편차는 우리가 모르는 $\sigma^2$와 설명변수의 표본값인 $x_1, \cdots, x_n$으로 구성되어있다.
* 만약 여기서, $\beta_1 = 1$이라고 귀무가설을 세운다면,

> $\frac{\hat{\beta_1} - 1}{sd(\hat{\beta_1})} \sim N(0,1)$

* 위 식을 세운다고 해도 여전히 우리가 모르는 $\sigma$가 포함돼있다. 
* 결국, 위 식은 통계량이 아니다. 
* 이제 우리는 미지의 $\sigma$를 $s$로 치환하여 검정 통계량을 도출할 것이다.



