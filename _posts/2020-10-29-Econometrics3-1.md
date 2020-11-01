---
title:  "계량경제학 강의3-2(한치록)"
excerpt: "단순 회귀모형의 추정"

categories:
  - Econometrics
tags:
  - Blog
use_math: true
last_modified_at: 2020-10-29
---
> ### 3.5 설명변수 표본값들이 모두 동일할 때

* 표본 내 $X$의 값이 모두 동일할 때 다음과 같은 문제가 발생한다.
	* 우리의 목적은 표본내 $X$ 관측값의 차이를 이용하여 $Y$ 관측값의 차이를 설명하는 것
	* $Y$ 값들은 관측치별로 상이한데, $X$값들은 모두 동일하다면?
	* 우리는 개체별로 동일한 것들로 개체별 상이한 것들을 설명하려 하는 것

> ### 3.6 맞춘값과 잔차

* 맞춘값(fitted values): 수평축으로부터 각 점에 이르는 수직방향 값은 주어진 $X$ 값에 대하여 $\hat{\beta_0} + \hat{\beta_1}X$를 구함으로써 얻어진다.
* 잔차(residual): 각각의 관측값인 $y_i$에서 그 맞춘값인 $\hat{y_i}$를 뺀 것
* 앞서 정의한 직교방정식에 의하면,
	* 잔차와 설명변수값을 곱해서 합한 것도 반드시 0이 되어야 한다.
	* $\sum_{i=1}^{n}{\hat{u_i}}=0$과 $\sum_{i=1}^{n}{x_i\hat{u_i}}=0$

* 표본내 17번 개체의 맞춘값은 설명변수의 값이 $x_17$인 모든 개체들의 평균 $Y$를 추정한 것이다.
	* $\hat{E(YIX=x_17)} = \hat{y_17} = \hat{\beta_0}+\hat{\beta_1}x_17$