---
title:  "계량경제학 강의 4-2 (2) (한치록)"
excerpt: "추정값과 참값의 관계"

categories:
  - Econometrics
tags:
  - Blog
use_math: true
last_modified_at: 2020-12-07
---
 	
#### 비편향 추정량의 의미

* 예를 들어, 나에게 어떠한 자료가 주어지든 $\beta_1$이 0이라고 해보자. 즉 추정량이 $\tilde{\beta_1}=0$ 인 것이다.
	* 그렇다면, $\tilde{\beta_1}$은 편향된 추정량인가? 비편향된 추정량인가?
* 만일, $\beta_1 = 0$이면 $\tilde{\beta_1}$은 비편향이다.
* 그러나, 비편향 추정량은 아니다.
* 왜냐면, 비편향 추정량이란 '모수의 참값이 무엇이든' 비편향인 추정량이다.
	* 위 예에서는 $\beta_1$이 0이 아닐 경우 바로 편향이므로
* 오차평균 0의 가정하에서 최소제곱 추정량은 이런 강한 의미에서 비편향 추정량이다.

#### 오차평균0 가정이 위배된다면?

> $범죄율 = \beta_0 + \beta_1경찰수+u$

* 위 식을 보면, 경찰 수를 제외한 나머지 요인에 의해 범죄율이 증가하면 범죄를 줄이기 위하여 경찰의 수를 증가시킬 수 있다. 
* 수식을 보면,
	*  오차들의 평균이 0이 아니라, $X$값에 좌우 된다고 하면, 
	*  $E(uIX) = \delta_0 + \delta_1X$라고 해보자
	*  $E(\hat{\beta_1}) = \beta_1 + E\left[\frac{\sum_{i=1}^{n}{(x_i-\bar{x}u_i)}}{\sum_{i=1}^{n}{(x_i-\bar{x})^2}}\right] = \beta_1+\frac{\sum_{i=1}^{n}{(x_i-\bar{x})E(u_i)}}{\sum_{i=1}^{n}{(x_i-\bar{x})^2}}$
	*  $\beta_1 + \frac{\sum_{i=1}^{n}{(x_i-\bar{x})(\delta_0+\delta_1x_i)}}{\sum_{i=1}^{n}{(x_i-\bar{x})^2}} = \beta_1 + \delta_1$

### 4.5 최소제곱 추정량의 표집분산
* 설명변수 표본값 고정, 비특이성, 동분산, 오차 간 독립 가정하에서 최소제곱 기울기 추정값의 표집분산은
* $var(\hat{\beta_1}) = \frac{\sigma^2}{\sum_{i=1}^{n}{(x_i-\bar{x})^2}}$
* 위 식에 따르면, 기울기 추정값의 표본추출 반복시 분산은 
	* 오차항의 분산($\sigma^2$)이 작을 수록 작으며
	* 표본내 $X$값들이 다를 수록(분산이 클수록) 작다. 

### 4.6 분산과 효율성
* 표본추출 반복시행 시 어떤 추정량의 분산이 크다는 말은 표본 관측값이 바뀔 때 추정값도 크게 바뀔 수 있음을 의미한다.
* 이런 경우, 자료로부터 구한 추정값에 신빙성이 떨어질 가능성이 높다
* 반대로, 표집분산이 작다면, 표본을 바꿔서 추정값을 구해도 값이 크게 변하지 않음을 의미하고 참값과 비교적 가까움을 의미한다.
* 결국, 두 추정량이 모두 비편향이고, 한 추정량이 다른 추정량보다 분산이 작을 때, 우리는 분산이 더 작은 추정방법이 큰 추정방법보다 낫다고 하거나 더 효율적(efficient)이라고 한다. 


### 4.7 최소제곱 추정량은 선형추정량
> $\hat{\beta_1} = \frac{\sum_{i=1}^{n}{(x_i-\bar{x})y_i}}{SST_X} = \sum_{i=1}^{n}{(\frac{x_i-\bar{x}}{SST_X})y_i}$

* 위 식을 보면, $y_1, \cdots, y_n$의 선형함수다.
* 이 말은 결국, 최소제곱 기울기 추정량은 선형추정량이라는 의미
* 결국, 어떤 모형이 선형이라고 하면, 이는 그 방정식의 모수(파라미터)에 대해 선형이라는 뜻이고
* 어떤 추정량이 선형추정량이라고 하면, 이는 추정량이 $y_1, \cdots,y_n$에 대해 선형이라는 뜻이다.

### 4.8 최소제곱법의 효율성

* 표본 설명변수값 고정, 오차평균0, 동분산, 오차 간 독립의 가정하에 표본 추출이 반복시행될 때
* 어떤 선형 비편향 추정량도 최소제곱 추정량보다 더 작은 분산을 가질 수 없다
* 즉, 최소제곱 추정량이 가장 좋은 선형 비편향 추정량(BLUE: Best Linear Unbiased Estimator)이라는 것이며, 이걸 증명한 게 <b> 가우스 마코프 정리 </b>이다.
	* 가우스 마코프 정리를 위해서는 앞의 가정들, 특히 동분산 가정과 오차 간 독립 가정이 중요하다.

### 4.9 오차분산 추정량과 표준오차

* 최소제곱 추정량 $\hat{\beta_1}$의 표집분산은 앞에서 말한 여러가지 가정 하에 $\frac{\sigma^2}{\sum_{i=1}^{n}{(x_i - \bar{x})^2}}$이다.
* 여기서 $\sigma^2$을 $s^2$로 치환하면 $\hat{\beta_1}$의 표집분산의 추정값인 $\frac{s^2}{\sum_{i=1}^{n}{(x_i - \bar{x})^2}}$이 된다.
* 여기에 제곱근을 취하면 $\hat{\beta_1}$ 표본추출 반복시행시 표준편차인 $sd(\hat{\beta_1})$을 추정한 값이 되는데 이를 $\hat{\beta_1}$의 표준오차라하고 $se(\hat{\beta_1})$이라고 표기한다.
> $se(\hat{\beta_1}) = \frac{s}{SST_X}$
* 사실, 표준오차는 표준편차의 비편향 추정량은 아니지만, 이 점은 크게 중요치 않다.

### 4.10 최소제곱 추정량의 표집분포

* 오차항들이 모두 정규분포를 갖는다고 가정해보자.
	* 그런데, 앞서 우리는 이미 오차항들의 평균이 0이고, 오차항들의 분산이 $\sigma^2$로 동일하고, 오차항들이 서로 독립이라고 했다.
* 이 말을 간략하게 나타내면 $u_i \sim iidN(0, \sigma^2)$라고 하는데 여기서 $iid$는 독립적이고(independent) 동일한 분포를 가졌다 (identically distributed)는 뜻이다. 
	* 정규분포의 좋은 점은 정규 분포에 상수를 더하거나 곱해도 정규분포이고
	* 독립된 정규분포를 갖는 확률변수들을 서로 더한 것도 정규분포를 갖는 다는 사실이다. 
* 최소제곱 기울기 추정량은 $\hat{\beta_1} = \beta_1 + \frac{\sum_{i=1}^{n}{(x_i-\bar{x})u_i}}{SST_X}$이다.
	* $x_i$는 표본추출 반복시행시 불변이므로 정규분포를 갖는 $u_i$에 곱해지면 정규분포를 갖고,
	* $u_i$가 서로 독립이므로 $(x_i-\bar{x})u_i$도 모두 독립이며 이것들을 모두 더한 것도 결국 정규분포를 갖는다.
	* 또한, 이것을 표본추출 반복시행시 고정된 $SST_X$로 나눈 값도 정규분포를 가지며
	* 마지막으로 $\beta_1$이라는 상수를 더한 값도 정규분포를 가지므로 결국, $\hat{\beta_1}$은 정규분포를 갖는다. 

> $\hat{\beta_1} \sim N(\beta_1, var(\hat{\beta_1}))$

* 오차항들이 정규분포를 갖는다는 가정하에서 최소제곱 추정량도 정규분포를 갖는다는 게 매우 중요

#### 표준화

* 정규분포의 평균이 0이고 분산이 1이면 이를 표준정규분포라고 한다. 
* 무슨 분포이든 평균을 빼고, 표준편차로 나누면, 평균이 0이고 분산이 1이 될 수 있다. 
* 그러므로 $\frac{\hat{\beta_1}-\beta_1}{\sigma / \sqrt{SST_X}} \sim N(0,1)$ 이 된다.