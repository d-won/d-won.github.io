---
title:  "계량경제학 강의3-3(한치록)"
excerpt: "단순 회귀모형의 추정"

categories:
  - Econometrics
tags:
  - Blog
use_math: true
last_modified_at: 2020-11-02
---
> ### 3.7 종속변수가 로그일 때 계수 추정값의 해석

* 예: $\hat{log(Y)} = 0.245 + 0.07X$
* 좌변이 $log(Y)$면, $E[log(Y)IX]=\beta_0 +\beta_1X$ 일 때, $logE(YIX) = \beta_0 + \beta_1X$가 성립되지 않는다.
	* $E(log(Y)IX) \ne logE(YIX)$ 이기 때문
	* 그러므로 "$X$가 한 단위 증가할 때 $log(Y)$가 평균 약 0.07 증가하는 것으로 추정된다" 옳지만
	* "$X$가 한 단위 증가할 때 $Y$가 평균 약 7% 증가하는 것으로 추정된다"는 옳지 않다
* 다시 한번 말하지만 조건부 등식을 고려해봤을 때, '평균' oo% 증가한다는 말은 엄밀하게 옳지 않다
	* 수학적으로 보면,
	* $E(logYIX = x+\Delta x) - E(logYIX=x) = \beta_1\Delta x$
	* 결국, $log(Y)$의 평균과 $Y$의 평균에 로그를 씌운 것은 다르기 때문 
	* $E(logY) \ne logE(Y)$

> ### 3.8  제곱합

* SST(total sum of squares): 종속변수의 관측값이 표본평균으로부터 벗어난 편차를 제곱해서 합한 것
* SSE(explained sum of squares): 맞춘값들이 자신의 표본평균으로부터 변동한 양의 제곱합, 종속변수값 중 독립변수에 의해 설명된 부분에 얼마나 차이가 있는 지를 나타낸 것
* SSR(residual sum of squares): 잔차값들이 자신의 표본평균으로부터 벗어난 편차를 제곱해서 합한 것, 독립변수로 설명되지 않는 나머지 부분의 차이의 크기 측정

* $SST = SSE + SSR$
* $y_i - \bar{y} = \hat{y_i}-\bar{y}+\hat{u_i}$ 인데, 이걸 제곱해보면,
* $(y_i - \bar{y})^2 = (\hat(y_i)-\bar{y})^2 + \hat{u_i}^2+2(\hat{y_i}-\bar{y})\hat{u_i}$
* 위 식에서 좌변의 합은 SST, 우변 첫째 항의 합은 SSE, 나머지 제곱합이 SSR이 되어야 한다.
* 그런데, $\sum_{i=1}^{n}{(\hat{y_i}-\bar{y})\hat{u_i}}=\sum_{i=1}^{n}{\hat{y_i}\hat{u_i}}-\sum_{i=1}^{n}{\bar{y}\hat{u_i}}$이고
* 직교방정식에 의해 $\sum_{i=1}^{n}{\hat{u_i}}=0$이고, $\sum_{i=1}^{n}{\hat{y_i}\hat{u_i}}=0$이므로, 직교방정식이 성립했다면 위의 식은 성립한다.

> ### 3.9 R제곱

* $SST = SSE + SSR$의 식에서 양변을 $SST$로 나누면,
* $1=\frac{SSE}{SST}+\frac{SSR}{SST}$
* 여기에서 $SSE/SST$는 종속변수의 분산 중 $X$에 의해 설명된 부분의 비중을 나타내고 이 걸 결정계수(coefficient of determination)이라 한다.
* $R^2 = \frac{SSE}{SST} = 1-\frac{SSR}{SST}$