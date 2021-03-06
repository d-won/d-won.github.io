---
title:  "계량경제학 강의 8 (한치록)"
excerpt: "다중회귀분석"

categories:
  - Econometrics
tags:
  - Blog
use_math: true
last_modified_at: 2021-01-18
---



## 8.1 다중회귀 모형



* 우리가 단순하게 임금을 학력만 사용하여 회귀식으로 추정한다고 해보자 그럼 무슨 일이 생길까?
  * 당연하게도 임금에 많은 영향을 미치는 요소는 학력만 있는 게 아니다.
  * 예를 들어 경력도 매우 중요한 요소다. 
  * 우리가 만약 학력만으로 회귀식을 세운다면 경력의 영향은 오차항에 포함되고
  * 설명변수와 오차항 간의 상관관계가 있게 된다. 
* 더 엄밀히 말한다면, 경력으로 인한 임금 차이가 오차항에 포함되어
  * 오차 평균 0 가정이 위배되고, 
  * 평균 임금 차이가 학력으로 인한 것인지 여타 요소(경력) 때문인지 알수 없게 된다.

* 위 문제를 수식으로 표현하면 다음과 같다. (아래에서 설명변수 표본값 고정 가정하에 표본추출 반복하는 상황)
  * 임금 = $\beta_0 + \beta_1$학력 $+ u$
  * 학력이 16년인 사람들의 평균 임금과 학력이 12년인 사람들의 평균 임금 간 차이는 아래와 같이 분해된다. 
    * $E($ 임금 $\mid$ 학력 $=16) - E($ 임금 $\mid$ 학력 $=12) = \beta_1(16 - 12) + [E(u\mid$ 학력 $=16) - E(u\mid $ 학력 $=12)]$
    * 위에서 $\beta_1(16-12)$가 학력 차이 영향이며, 꺾은 괄호 안이 여타 요소 차이의 영향이다.
    * 오차 평균 0의 가정이 성립한다면 꺾은 괄호 안은 0이며, 따라서 $\beta_1(16-12)$이 학력 차이의 영향이다.
    * 그러나, 고졸자 경력이 더 높고, 경력이 높을수록 임금이 높다면 꺾은 괄호 안의 값이 음($-$)이 되고, 이 값의 정확한 크기를 모르는 한 $\beta_1(16-12)$가 계산되기 어렵다.



#### 다른 변수를 제어하여 오차평균 0 회복

* 우리는 단순회귀가 아닌, 다중회귀를 활용하여 다른 변수를 통제함으로써 해당 문제 해결 가능
* 위 식에서도 학력과 더불어 '경력'이 추가되면,
  * 원래는 경력과 학력이 상관을 가져서 고학력 집단이 경력이 낮고 그래서 오차항이 평균적으로 더 낮을 수 있었지만
  * 경력과 학력을 동시에 활용하면 '오차항'에서 이런 문제가 없거나 더 적어 보인다.
  * 물론, 경력 외에도 다른 제3의 요소가 임금에 중요할 수 있다. 하지만 '완벽한 쌍둥이' 집단을 비교하지 않는 한 이런 식의 문제는 모든 모형에 대해 제기할 수 있고, 우리는 어느 선에서 주어진 모형에 만족해야 한다.
  * 어디에서 멈출 것인가는 어떠한 용인을 통제하고 싶은 가에 따라 좌우된다.



## 8.2 모수의 해석

> $Y = \beta_0 + \beta_1X_1 + \cdots + \beta_kXk + u$

* 일반적인 모형을 위와 같다고 할 때, 모수 해석을 위해 $E(u \mid X_1, \cdots, X_n)=0$이라고 가정하자. 

* 그러면 아래와 같은 식을 얻는다

  

> $E(Y\mid X_1, \cdots, X_k) = \beta_0 +\beta_1X_1 + \cdots + \beta_kX_k$



* 위에서 다른 모든 값을 고정하고, $X_1$만 증가시키면 $E(Y\mid X_1, \cdots, X_k)$는 $\beta_1$만큼 증가한다. 
* 그러므로, $\beta_1$은 여타 설명변수들($X_2, \cdots, X_k$)가 고정된 채 $X_1$이 한 단위 증가할 때 $Y$가 평균적으로 증가하는 정도를 의미한다.
* 물론, 여타 변수들 고정시키고 한 변수만 변할 때 종속변수가 받는 영향이라는 해석이 항상 옳은 것은 아니다. 왜냐면 상호작용항과 제곱항의 부분이 있기 때문이다.



## 8.3 최소제곱법



* 우리가 독립변수들에 대해 행렬을 갖고 있다면, $x_{12}$ 는 1번 관측치의 $X_2$ 값이 된다.
* 이러한 상황에서

> $\sum_{i=1}^{n}{(y_i - b_0 -b_1x_{i1}-\cdots -b_kx_{ik})^2}$

* 다중회귀에서 최소제곱법은 위식을 최소화시키는 $b_0, b_1, \cdots, b_k$를 찾는 것이다.
* 이 최소제곱법을 보통최소제곱법(ordinary least squares, OLS)라고 한다. 
* 보통최소제곱법은 일반화된 최소제곱법(generalized least squares, GLS)의 특수한 형태다.
  * 계량 경제학에서 ordinary, 보통의 또는 통상적인 이라는 말이 붙는 통계량은 오차항에 이분산과 자기상관이 없을 때를 염두에 두고 고안한 통계량을 지칭할 때 쓴다.
  * 보통최소제곱법은 이분산과 자기상관이 없을 때 BLUE이고,
  * 통상적인 표준오차는 이분산과 자기상관이 없을 때 사용할 수 있는 표준오차이다.



* 주어진 자료에 대해 식 $ \sum_{i=1}^{n}{(y_i-b_0-b_1x_{i1}-\cdots b_kx_{ik})^2}$를 최소화시키는 OLS 추정량은 다음 조건을 만족시킨다
* $\sum_{i=1}^n{(y_i-\hat{\beta_0} - \hat{\beta_1}x_{i1}-\cdots-\hat{\beta_k}x_{ik}) = 0}$  ~ $\sum_{i=1}^n{x_{ik}(y_i-\hat{\beta_0} - \hat{\beta_1}x_{i1}-\cdots-\hat{\beta_k}x_{ik}) = 0}$
* 이전과 마찬가지로 이 $k+1$개의 등식을 직교방정식이라 한다.



#### 절편을 수학적으로 어떻게 이해할까



* 회귀모형에서 절편은 모집단 내 $X_1=0, \cdots, X_k=0$인 개인들의 평균 $Y$값이다.
* 수학적으로는 $\beta_1$이 $X_1$ 변수의 계수인 것처럼, $\beta_0$은 $X_0$ 변수의 계수라고 보아도 좋고, $\beta_0$은 그 값이 항상 1을 갖는 변수인 것이다.
* 조금 더 나아가서, $Y = \beta_0 + u$라는 절편으로만 이루어진 식을 생각해보자. 
  * 직교방정식에 의해 $\sum_{i=1}^n{(y_i - \hat{\beta_0})} =0 $을 만족하므로 결국, $\hat{\beta_0}  = \frac{1}{n}\sum_{i=1}^n{y_i}$로 
  * 절편만으로 이루어진 모형에서 절편의 OLS 추정량은 종속변수의 표본평균과 동일하다. 



#### 최소제곱 추정량의 계산방법에 관한 주석



* 우변에 절편 포함, 세 개의 계수를 갖는 모형을 생각해보자.



> $Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + u$



* 이런 경우, $\hat{\beta_1}$은 두 단계에 의해 구해진다.
  1. $X_1$을 제외한 나머지 변수들이 독립변수, $X_1$을 종속변수로 하는 회귀를 진행한다. 그리고 잔차를 구한다.
  2. $Y$를 종속변수, 위에서 구한 잔차항을 독립변수로 하되, 절편을 제외한 회귀를 진행한다. (절편이나, 다른 변수 포함해도 상관 없다)
* 증명하면,
  * 1단계 회귀로부터 나온 잔차항을 $\hat{r_{i1}}$이라 할 때, 증명할 것은 $\sum_{i=1}^n{\hat{r_{i1}}(y_i-\hat{\beta_1} \hat{x_{i1}})}=0$이다.
  * $\sum_{i=1}^n{\hat{r_{i1}}(y_i-\hat{\beta_1} \hat{x_{i1}})} = \sum_{i=1}^n{\hat{r_{i1}}( \hat{\beta_0} + \hat{\beta_1}x_{i1} + \hat{\beta_2}x_{i2} + \hat{u_1} - \hat{\beta_1}\hat{r_{i1}})}$ 은 $y_i$ 항을 풀어낸 것이고,
  * $\hat{\beta_1} \sum_{i=1}^n{\hat{r_{i1}}(x_{i1} - \hat{r_{i1}})} + \sum_{i=1}^n{\hat{r_{i1}}\hat{u_i}}$  는 두 직교방정식 $\sum_{i=1}^n{\hat{r_{i1}}}=0$ 및 $\sum_{i=1}^n{x_{i2}\hat{r_{i1}}}=0$에 의해 성립한다.
  * $\hat{\beta_1} \sum_{i=1}^n{\hat{r_{i1}}(\hat{\delta_0} + \hat{\delta_1}x_{i2})}+\sum_{i=1}^n{(x_{i1}-\hat{\delta_0} - \hat{\delta_1}x_{i2})\hat{u_i}}$ 여기서는 $x_{i1} = \hat{\delta_0} +\hat{\delta_1}x_{i2}+\hat{r_{i1}}$이기 때문에 변형된 결과다.
  * $\hat{\beta_1} \hat{\delta_0} \sum_{i=1}^n{\hat{r_{i1}}} + \hat{\beta_1}\hat{\delta_1}\sum_{i=1}^n{\hat{r_{i1}}x_{i2}} + \sum_{i=1}^n{x_{i1}\hat{u_i}} -\delta_0\sum_{i=1}^n{\hat{u_i}}- \hat{\delta_1}\sum_{i=1}^n{x_{i2}\hat{u_i}}$
  * 마지막으로, 위 식에서는 직교방정식에 의해 모든 항이 0이 되므로 증명은 끝난다.



* 결국, 이것이 $\beta_1$의 의미는.
  * 한 개 독립변수를 종속변수로 나머지 독립변수를 독립변수로 삼아 회귀의 잔차를 구함으로써, 여타 독립변수들과 무관한 $X_1$의 변화를 구하고
  * 종속변수 $Y$를 해당 잔차를 독립변수로 삼아 회귀를 진행함으로써, 여타 독립변수들을 고정한 상태에서 $X_1$의 값이 증가할 때  $Y$가 받는 영향을 추정하는 것이다.



## 8.4 OLS 추정량이 유일한 조건



* 독립변수들 사이에 완벽한 선형관계(선형종속)이 성립할 때, 우리는 특이성(singular)를 만나고, 이러한 특이성이 존재할 때 최소제곱 추정량은 유일하지 않다.
* 완벽한 선형관계가 존재하면 계량경제학 교과서에서는 완벽한 공선성(collinearity)이 존재한다고 한다.
  * 예를 들면, '성별'이 더미변수일 때, 여성이 1이고 남성이 0으로 메겨진다고 하자.
  * $wage = \beta_0 + \beta_1 female + \beta_2 male +u$
  * 위 식은 특이성이 존재한다. 왜냐면, 남성은 여성과 선형종속 관계이므로 사실상 1개의 변수만 있는 것과 다를 게 없기 때문이다.
* 결국, 특이성이 존재하면 하나 이상의 직교방정식이 쓸모 없게 되며, 그 결과 추정값은 유일하게 결정되지 않는 것이다. 
  * 미지수가 2개고 방정식도 2개면 풀 수 있지만, 미지수가 2개인데 방정식이 1개만 있으면 못 푸는 것과 동일



## 8.5 더미변수와 상호작용항



* female은 1 male은 0이라고 하면 이런 변수가 더미변수다.
* $log(wage) = \beta_0 + \delta_0 female + \beta_1 school + \beta_2 exper +u$
* 위 식이 의미하는 바는
  * '학력'과 '경력'이 동일할 때 남녀간에 평균 임금 차이를 나타내는 것
  * 결국, 남성과 여성은 $\delta_0$만큼 임금이 차이나게 됨
  * $\beta_1$은 '성별'과 '경력'이 동일할 때, 학력 1년의 차이가 로그 임금의 평균값에 미치는 영향이다. 
* 만약, $\delta_0 = -0.243$라면 '학력'과 '경력'이 동일한 남녀간에 임금 차이는 어느 정도일까?
  * 남성이라면 $e^{0.243} - 1 =0.275$로 결국, 27.5% 정도 높고
  * 여성이라면 $e^{-0.243}-1 = 0.215$로 결국, 21.5% 정도 낮다고 볼 수 있다.



* 이제 모형의 우변에 $female \times school$이라는 상호작용항을 추가해보자.
  * 그럼 모형은, 아래와 같다.
  * $log(wage) = \beta_0 + \beta_1 school +\beta_2exper + \delta_0female+\delta_1(female \times school) + u$
    * 위 모형에서 남성은 $female = 0$이므로, $log(wage) = \beta_0 + \beta_1 school + \beta_2 exper +u$가 되고
    * 여성은 $female = 1$이므로, $log(wage)= (\beta_0+\delta_0) + (\beta_1 + \delta_1)school +\beta_2exper+u$가 된다.
* 결국, 상호작용항은 '동일한 독립변수(학력)'의 효과가 더미변수(성별)에 의해 어떻게 다른지를 보여주는 것이다. 
  * 이것은 더미변수항 그 자체와는 다르다. 더미변수항은 다른 조건이 모두 동일할 시 더미변수(성별)의 차이를 보여주는 것
  * 예를 들어 위 모형에서 $\beta_1=3$이고, $\delta_1=1.5$였다면, 학력이라는 조건도 1학년 올라갈때마다 성별에 대한 차이가 있고(임금에 대해서), 사례대로라면 여성이 1학년 증가시 4.5 임금이 더 증가하는 것
* 마지막으로 다시 한번 우리가 더미변수에 대해 살펴보면,
  * 어떤 변수가 표본에서 취할 수 있는 값들의 모든 경우에 대해 더미 변수를 만든다면,
  * 절편이 존재할 때 불가피하게 완전한 공선성(특이성) 문제가 발생한다.
  * 이를 dummy variable trap 더미변수 함정이라 한다.



#### 집단별 회귀와 전체 회귀

* 아래 다섯가지 모델을 생각해보자. 
  1. $log(임금) = \beta_0 + \beta_1학력+u$  
  2. $log(임금) = \beta_0 +\beta_1학력 + \beta_2 여성 +u$
  3. $log(임금) = \beta_0 + \beta_1 학력 + \beta_2여성 + \beta_3(여성 \times 학력) + u$
  4. $log(임금) = \beta_0 + \beta_1학력 + u$ (남자만 선별)
  5. $log(임금) = \beta_0 + \beta_1학력+u$ (여자만 선별)
* 사실, 위의 모델에서 계수값은 다를 수 있으나 일단 동일한 기호를 사용했다.
  1. log(임금)에 대하여 학력으로 하나의 직선을 그린다.
  2. log(임금)에 대해 남성과 여성의 학력의 기울기는 동일하나 절편값이 다르다.
  3. 성별로 절편과 기울기 모두 상이하다. 남성은 절편과 기울기가 각각 ($\beta_0, \beta_1$)이고, 여성은 ($\beta_0+\beta_2$, $\beta_1+\beta_3$)이다.
     * 결국, 3번째 식에서 남성에 해당하는 부분이 4번식과 동일하고, 여성에 해당하는 부분이 5번식과 동일하게 된다.
* 표로 표현하면,

|        | 남성                              | 여성                                          |
| ------ | --------------------------------- | --------------------------------------------- |
| 절편   | 3번식 $\beta_0$ = 4번식 $\beta_0$ | 3번식 $(\beta_0 + \beta_1)$ = 4번식 $\beta_0$ |
| 기울기 | 3번식 $\beta_1$ = 4번식 $\beta_1$ | 3번식 $(\beta_1 + \beta_3)$ = 4번식 $\beta_1$ |

* 위 표를 기반으로 보면 모든 설명변수들과 더미변수의 상호작용항들이 포함된 모형의 계수추정값들은 집단별로 별도의 회귀를 통해 똑같이 구할 수 있다. 
  * 특이할 점은 1번 식의 계수들은 4,5번 식의 계수들의 선형결합으로 나타낼 수 있다는 것이다. 
* 추가로 다음 모델을 생각해보자. $log(임금) = \beta_0 + \beta_1학력 +\beta_2(학력 \times 여성) + u$
  * 위 모델은 합리화하기 어려운데,
  * 성별에서 학력차이가 갖고 오는 효과가 다르다면, 학력 = 0일때, 동일할 이유가 없기 때문 ($\beta_0$)
  * 그러므로, 교차항을 포함시키고자 하면, 반드시 서로 곱해지는 두 변수들을 별도의 변수들로도 포함시켜야 한다.
  * $log(임금) = \beta_0 + \beta_1학력 + \beta_2(학력 \times 여성) + \beta_3 여성 + u$



## 8.6 제곱항



* $Y = \beta_0 +\beta_1X_1 + \beta_2X_2^2 + \beta_3X_2 + u$라는 모형이 있다고 하자.
* 위 모델에서 $X_2$가 고정될 때, $X_1$이 $\Delta X_1$만큼 증가하면, $Y$의 평균은 대략 $(\beta_1 + 2\beta_2X_1)\Delta X_1$만큼 증가한다.
  * 특이한 점은 $X_1$ 값에 영향을 받는 것이고,
  * 위에서 증가량은 식에 대해서 $X_1$으로 미분을 해보면 나온다
  * $\beta_1 + 2\beta_2X_1$에서 만일, $\beta_1 > 0, \beta_2 < 0$이면 우리는 우상향하다가 우하향하는 지점을 해당 식에 대해 미분하여 $-\beta_1 / 2\beta_2 =0$이 되는 지점이라는 것을 알 수 있다. 이런 지점을 반환점(turning point)라 한다.
* 예를 들어 $흡연량 = \beta_0 + \beta_1log(income) + \beta_2log(cigprice) + \beta_3 educ + \beta_4age + \beta_5 age^2 + u$라고 할 때
  * 일단 위 식은 흡연량이 젊을 때는 많지만, 나이가 들 수록 줄어들 것이므로 일견 타당해 보인다.
  * $\beta_4 = 0.78, \beta_5 = -0.009$라면 몇 살일 때 흡연량이 줄어들까? 위에서 보았 $-\beta_1 / 2\beta_2 =0$가 되는 43세 정도다.

* 그런데 위의 자료에서 만약 자료가 43세까지 없었다면 어땠을까? 우리는 반환점이 있는 지 없는 지에 대해 가정만으로 말했을 뿐 실제 자료에서는 그랬는 지 확인하기 어려웠을 것이다.
* 이렇게 설명변수 표본값의 범위를 넘어서는 지점에 대해 추정결과를 사용한 예측을 하는 것을 '외삽(extrapolation)'이라고 한다.
  * 외삽은 마치 10대의 자료로부터 30대에 관해 예측하는 것과 같아 부적절할 수 있다. 
  * 정리하자면 자료의 존재 범위를 너머선 모형을 적용하는 것이다. 



## 8.7 맞춘값, 잔차, 제곱합, R제곱



* 맞춘값, 잔차, 제곱합, R제곱에 대한 정의는 단순 선형회귀와 동일하다.

  * 그러나, 만일 모형에 절편이 포함되어 있지 않다면? $SST \ne SSE + SSR$이며, $R$제곱을 모형에 의해 설명되는 종속변수 내 차이 비중으로 해석하기 어렵다. 
  * 모형에 절편이 없을 때 $R^2$를 새롭게 정의하는 방법이 존재한다. 해당 부분은 어렵지 않으나 추후 설명. 대부분의 패키지에서 절편이 없을 때 이렇게 산출값을 뽑아낸다.

* 중요한 것은 단순회귀와 달리, 다중회귀는 변수를 많이 넣을 수 있고 식에 따르면 변수를 넣을 수록 $R^2$은 상승한다는 것이다. 이를 방지하기 위해 고안한 식이 '조정된 결정계수'다.

  >$\bar{R^2} = 1 - \frac{SSR/(n-k-1)}{SST/(n-1)}$ 

  * 핵심 아이디어는 SST와 SSR을 각각 자유도로 나눠주는 것이다. 
  * 특히, SSR은 새로운 변수를 추가할 때마다 k가 증가하여 추가된 변수의 설명력이 커서 SSR이 충분히 감소하지 않으면 (n-k-1)의 감소 폭이 더 커서 오히려 SSR/(n-k-1)이 더 증가하게 된다. 
  * 사실 $SSR/(n-k-1)$은 오차항 분산의 추정값이 $s^2$이다. 결국, 오차항 분산이 줄어들어야만 $\bar{R^2}$이 증가하게 된다.



## 8. A 최소제곱 추정량의 행렬표현



* 행렬로 직교방정식을 간단히 표현하면,

  > $X^T(Y-X\hat{\beta}) = 0$
  >
  > $X^TX\hat{\beta} = X^TY$

* 위 식에서 우리가 회귀계수의 벡터인 $\hat{\beta}$에 대해 정리하면,

  > $(X^TX)^{-1}X^TX\hat{\beta} = (X^TX)^{-1}X^TY$
  >
  > $\hat{\beta} = (X^TX)^{-1}X^TY$



