---
title:  "계량경제학 강의 10 (한치록)"
excerpt: "다중회귀 모형에서 가설 검정"

categories:
  - Econometrics
tags:
  - Blog
use_math: true
last_modified_at: 2021-02-18


---



* 다중회귀모형에서는 우변에 변수가 여럿이므로, 가설이 좀 더 복잡할 수 있음
  * $\beta_1 + \beta_2 = 1$처럼 하나의 제약으로 되어있거나
  * $\beta_1= 0$ 그리고 $\beta_2 = \beta_3$처럼 여러 개 제약으로 이루어져 있을 수도 있다
* 9.1 절 모든 가정들이 성립한다고 가정한다
  * 정규분포 가정은 표본 크기가 크면 별 문제가 되지 않는다
  * 동분산성 가정과 오차 간 독립 가정이 위배되는 상황도 표본크기가 크면 큰 문제가 없다
  * 설명 변수 표본값들이 임의적으로 결정되도, 설명변수들과 오차가 서로 독립이라면 문제 없다
  * **다만, 확률적인 설명변수 표본값들이 오차와 상관되면 문제가 발생한다**



## 10.1 하나의 선형 제약으로 이루어진 가설의 t 검정



> $\frac{OLS 추정량들의 선형결합 - 상응하는 모수들의 선형결합}{추정된 표준편차} \sim t_{n-k-1}$



#### 수동 계산법

* $\frac{(\hat{\beta_1} + \hat{\beta_2}) - (\beta_1 + \beta_2)}{se(\hat{\beta_1} + \hat{\beta_2})} \sim N(0, 1)$
* 만약 여기서, 귀무가설이 $\beta_1 + \beta_2 = 1$이라면, 위의 식은 아래와 같이 된다.
* $\frac{(\hat{\beta_1} + \hat{\beta_2}) - 1}{se(\hat{\beta_1} + \hat{\beta_2})} \sim N(0, 1)$
* 우리가 위 값을 구하려면 $se(\hat{\beta_1} + \hat{\beta_2})$를 구해야 하는데, $var(\hat{\beta_1} + \hat{\beta_2})$를 구해야 하므로 조금 복잡하다



#### 반자동

* $\beta_1 + \beta_2  = 1$을 $\theta = \beta_1 + \beta_2 - 1$로 바꾸면,
* $Y = \beta_0 + \beta_1 X_1 + (\theta - \beta_1 + 1)X_2 +\beta_3X_3 + u$
  * $Y = \beta_0 + \beta_1(X_1 - X_2) + \theta X_2 + X_2 + \beta_3X_3 + u$
  * $Y- X_2 = \beta_0 + \beta_1(X_1-X_2) + \theta X_2 +\beta_3 X_3+ u$
  * 그러므로 우리는 위와 같은 식을 만들고 회귀분석을 하게 된다면 $\theta$에 대한 검정값이 나오게 된다.

## 10.2 잔차제곱합을 비교하여 검정하는 방법

* 해당 방법에서는 $\beta_1 + \beta_2 - 1 = 0$이라는 제약을 가하여 구한
* 잔차제곱합과 제약을 주지않고 계산한 잔차제곱합을 서로 비교하여
* 통계적 검정을 진행한다


* 우리가 제약되지 않은 잔차제곱합 (원래 식)을 $SSR_U$라 하고
* 제약되 잔차제곱합 (위 제약을 적용)을 $SSR_R$이라 할 때
* $SSR_R$은 $SSR_U$보다 작지 않다. 이유는 $SSR_U$는 모든 경우의 수 중 잔차를 최소화하여 구한 것이고 $SSR_R$은 제약이 있기 때문
* 해당 방식을 통해 검정하는 통계량은 아래와 같다
  * $F = \frac{SSR_R - SSR_U}{ms^2}$
  * 위 값은 F 통계량이며
  * F 통계량은 일정한 가정하 F 분포를 갖는다
    * F 분포는 서로 독립인 두 카이제곱 변수들의 비율이 갖는 분포이다. 
    * $ X_1 \sim \chi^2_{df1} $이고 $X_2 \sim X^2_{df2}$이며 서로 독립이면 $(X_1/df_1)/(X_2/df_2)$는 자유도가 $(df_1, df_2)$인 F 분포를 따른다
    * 카이제곱 변수들이 확률 1로 양의 실수값을 가지므로 F 분포를 갖는 변수들도 확률 1로 양의 실수값을 갖는다.
* 하나의 제약으로 이루어진 귀무가설에 대해 대립가설이 '≠' 형태로 되어있으면, t 검정/F 검정 모두 가능하다
  * 그래서, 두 방법은 전적으로 동일한 결과를 낳는다.
  * t 통계량을 제곱하면 그 값은 F 통계량과 정확히 일치하기 때문이다. 
  * t 분포인 어떤 확률변수를 제곱하면 그 분포는 F 분포가 된다. 

## 10.3 여러 선형제약으로 이루어진 가설 검정

* $\beta_1 = \beta_2 = 0$처럼 여러 제약이 있다고 가정하자. 
* 대립가설은 $\beta_1$과 $\beta_2$ 중 적어도 하나는 0이 아니라는 것이다. 
  * 이를 위해 각각의 t검정을 하고 조합하여 결론을 낼릴 수 있겠다고 생각할 수 있지만
  * 상호작용을 고려하지 않으므로 좋지 않다
  * F 검정을 그래서 배운 것
* $F = \frac{(SSR_R - SSR_U)/m}{SSR_U/(n-k-1)}$
  * 위 가정에서 $m=2$
* 다만, 해당 F검정을 하기 위해서는 library 활용 필요 (ex: car에서 lht)



#### 코드 진행

~~~R
### jc(2년제 대학) univ (4년제 대학) 영향 동일하다는 제약, F 검정

Twoyear <- read.csv('twoyear.csv')
n <- nrow(Twoyear)
m <- 1
u1 <- lm(lwage ~ jc + univ + exper, data = Twoyear)$resid
u0 <- lm(lwage ~ I(jc+univ) + exper, data = Twoyear)$resid
ssr1 <- sum(u1^2)
ssr0 <- sum(u0^2)
Fstat <- ((ssr0 - ssr1)/m)/(ssr1/(n-4))
Fstat
pval <- 1-pf(Fstat, m, n-4)
pval

[1] 0.1422441

~~~



~~~R
### jc, univ 영향과 두 학력과 exper 영향이 모두 동일하다는 가정 (b1 = b2 = b3)

libarary(car)

ols1 <- lm(lwage ~ jc + univ + exper, data=Twoyear)
lht(ols1, c("jc=univ", "univ=exper"))

Linear hypothesis test

Hypothesis:
jc - univ = 0
univ - exper = 0

Model 1: restricted model
Model 2: lwage ~ jc + univ + exper

  Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
1   6761 1437.0                                  
2   6759 1250.5  2    186.49 503.97 < 2.2e-16 ***
---
Signif. codes:  
0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
~~~


