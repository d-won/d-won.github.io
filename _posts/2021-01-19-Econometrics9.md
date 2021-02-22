---
title:  "계량경제학 강의 9 (한치록)"
excerpt: "다중회귀 추정량의 성질"

categories:
  - Econometrics
tags:
  - Blog
use_math: true
last_modified_at: 2021-02-08

---



## 9.1 모형의 구성항목들에 대한 가정



> ### 설명변수에 대한 가정

* 설명변수 표본값 고정
* 비특이성



> ### 오차항에 대한 가정

* 오차평균 0
* 오차 동분산
* 오차 간 독립
* 정규분포



## 9.2 OLS 추정량 평균

* 설명변수 표본값 고정 가정하에 비특이성 가정이 만족되면 주어진 표본에서 OLS 추정값은 유일하다
* 오차평균 0의 가정이 만족되면, OLS 추정량은 비편향성을 갖는다. (표본추출 무한반복 시행시, OLS 추정량 평균은 모수와 동일)

> $\hat{\beta_1} = \beta_1 + \frac{\sum_{i=1}^{n}{\hat{r_{i1}}u_i}}{\sum_{i=1}^n{\hat{r_{i1}}^2}}$

* 위 식에서 $\hat{r_{i1}}$은 $X_1$을 여타 독립변수들에 대해 회귀했을 때, 얻는 잔차다
* 그러므로, 표본추출 반복할 때 고정돼있으므로 평균을 구하면 $u_i = 0$이면 위에서 결국 모수와 동일하게 된다.



* 행렬을 통해 비편향성을 증명하면,
  * $\hat{\beta} = (X^TX)^{-1}X^TY, Y=X\beta+U$ 이므로
  * $\hat{\beta} = (X^TX)^{-1}X^T(X\beta+U) = (X^TX)^{-1}X^TX\beta + (X^TX)^{-1}X^TU = \beta + (X^TX)^{-1}X^TU$
  * 위 식에서, $(X^TX)^{-1}X^T$는 고정되어있으므로 평균을 취하면 밖으로 나오고, 결국 식은 아래와 같다.
  * $E[\hat{\beta}] = \beta + (X^TX)^{-1}X^TE[U]$
  * 위에서, 오차평균 0 가정에 의해 $E[U]=0$이므로 결국, $E[\hat{\beta}] = \beta$가 된다.


## 9.3 변수를 누락시키면 어떻게 될까?


* 연구자가, 임금에 관련된 회귀식을 설계한다고 할 때 경력과 학력에 대해서 모두 고려하지 못하고 1개 변수만 넣는다면 어떻게 될까?

> $Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + u$

* 위에서 $X_1$은 학력이고, $X_2$는 경력이라고 할 때, 학력만 넣었다고 가정해보자.
* 그리고, $Y$를 $X_1$에 대해서 회귀시킨다고 할 때, 그 OLS 추정량을 $\tilde \beta_1$라고 하자
  * $\tilde{\beta_1} = \frac{\sum_{i=1}^n{(x_{i1}-\bar{x_1})(y_i - \bar{y})}}{\sum_{i=1}^n{(x_{i1}-\bar{x_1})^2}}$, 여기에 $y_i = \beta_0 + \beta_1x_{i1} + \beta_2 x_{i2}+u_i$를 대입하면
  * $y_i - \bar{y} = \beta_1(x_{i1} - \bar{x_1}) + \beta_2(x_{i2} - \bar{x_2}) + (u_i - \bar{u})$ 이므로
  * $\tilde{\beta_1} = \beta_1 + \beta_2 \times \frac{\sum_{i=1}^n{(x_{i1}-\bar{x_1})(x_{i2}-\bar{x_2})}}{\sum_{i=1}^n{(x_{i1}-\bar{x_1})^2}} + \frac{\sum_{i=1}^n{(x_{i1}-\bar{x_1})u_i}}{\sum_{i=1}^n{(x_{i1}-\bar{x_1})^2}}$ 이고, 표본값 고정 하에 표본추출 반복시행하면
  * $E(\tilde{\beta_1}) = \beta_1 + \beta_2 \times \tilde{\delta_1}$이고, 여기에서  $\tilde{\delta_1} = \frac{\sum_{i=1}^n{(x_{i1}-\bar{x_1})(x_{i2} - \bar{x_2})}}{\sum_{i=1}^n{(x_{i1}-\bar{x_1})^2}}$ 이 된다.
    * 위에서 보면 결국, $\tilde{\delta_1}$은 $X_2$를 $X_1$에 회귀할 때 기울기의 최소제곱 추정량이다.
* 결국, 위 식의 전개를 보면 
  * $\beta_1$은 $X_2$를 고정시킨 채 $X_1$을 변화시킬때 $Y$가 받는 평균 영향을 나타내고
  * $\beta_2\tilde{\delta_1}$는 $X_1$과 $X_2$가 서로 관련된 정도($\tilde{\delta_1}$)에 $X_1$을 고정시킨 채 $X_2$ 를 변화시킬 때 $Y$가 받는 평균 영향을 곱한 것이다.
    * $\beta_2\tilde{\delta_1}$는 $X_1$이 $X_2$를 변화시킴으로써 $Y$에 간접적으로 미치는 영향이다.
  * 최종적으로 변수를 누락하면 직접효과($\beta_1$)에 간접효과($\tilde{\delta_1}\beta_2$)를 더한 총 효과가 나오게 된다.
* 다시 돌아가서 위 모형을 생각해보면
  * 임금을 학력에 대해서 회귀시키면, 추정값은 평균 $\beta_2\tilde{\delta_1}$만큼 벗어날 것이다. 
  * 그런데 학력과 경력은 음의 상관관계가 있을 것이고, 경력의 효과는 양일 것이므로 
  * 단순회귀로부터 나오는 결과는 우리가 보고자 하는 $\beta_1$보다 더 작은 값을 추정하리라 예상된다.
* 정리하면
  * $X_1$의 총 효과 = $X_1$의 직접 효과 + $X_2$를 경유한 간접 효과
  * 그리고 위에서 식은 평균적인 관계를 나타내는 것이었고 최소제곱 추정량들은 
  * $\tilde{\beta_1} = \hat{\beta_1} + \hat{\beta_2}\tilde{\delta_1}$ 이다. 여기에 평균을 취하면 위와 같은 식이 나오는 것 확인 가능하다.



* 행렬로 구해도 똑같은 정리가 나온다.
  * 2개변수를 갖고 있는 아래와 같은 정규방정식을 생각해보자.
  * $\begin{bmatrix} X_1^T \\ X_2^T \end{bmatrix} \begin{bmatrix} X_1\hat{\beta_1} + X_2\hat{\beta_2}\end{bmatrix} = \begin{bmatrix} X_1^T \\ X_2^T\end{bmatrix} Y$  여기에서 위에 행만 따로 추출하고, $X_1^TY$를 $X_1^TX_1\tilde{\beta_1}$로 대체하면,
  * $X_1^TX_1 \hat{\beta_1} + X_1^TX_2\hat{\beta_2} = X_1^TX_1\tilde{\beta_1}$가 된다. 이제 양변에 $(X_1^TX_1)^{-1}$를 곱하고 $(X_1^TX_1)^{-1}(X_1^TX_2)$를 $\tilde{D}$라 놓으면
    * $(X_1^TX_1)^{-1}(X_1^TX_2)$는 사실, $X_2$를 $X_1$으로 회귀한 것에 대한 계수임을 알 수 있다.
  * $\hat{\beta_1} + \tilde{D}\hat{\beta_2} = \tilde{\beta_1}$이 된다.



#### 변수를 누락시키거나 추가하여도 좋은 경우

* 위 식에서 보면 알겠지만, 아래 경우에 OLS 추정량은 여전히 비편향적이다
  * 사실 통제하고자 하는 변수가 종속변수에 별도 영향을 미치지 않는다면 (위 사례 $\beta_2 = 0$)
  * 혹은, 설명변수와 무관한 경우 ($\tilde{\delta_1} = 0$)
* 독립변수가 둘이라면 위와 같을 수 있지만 2개 보다 많다면 주의해야 한다. 3개인 경우를 생각해보자.
  * $X_1, X_2$가 통제될 때, $X_3$이 $Y$에 아무런 영향도 못 미친다면 여전히 OLS 추정량은 비편향이다.
  * 그러나, $\beta_3 \ne 0$이고, $X_3$이 $X_1$과 상관 없지만, $X_2$와 상관이 있다면,
    * $X_1$과 $X_2$가 상관이 없다면, $X_3$이 누락될 경우 $X_2$는 편향, $X_1$은 비편향이다.
    * 만약 상관이 있다면, $X_1, X_2$ 모두 편향된다. 
* 이야기를 조금 틀어서, 모형 계수 추정할 때 다른 변수들 추가시키면 어떻게 될까? (원래는 누락, 지금은 추가)
  * 모형의 설명변수들과 무관하거나 Y에 별도 영향을 미치지  않는 변수들은 포함시켜도 OLS 추정량은 여전히 비편향이다. 
  
  
## 9.4 OLS 추정량의 분산

* OLS의 비편향성을 위해서 가정했던 조건들에 '오차 동분산'과 '오차간 독립'을 가정하자

* $X_1$을 다른 변수로 회귀시킨 후 나온 잔차들을 $\hat{r_{i1}}$이라 하자. 

* 그러면, 이 가정 하에 나온 최소제곱 추정량 $\hat{\beta_1}$의 표본 추출 반복 시행시 분산은 아래와 같다.

  * $var(\hat{\beta_1}) = \frac{\sigma^2}{\sum_{i=1}^n{\hat{r_{i1}}^2}}$
    1. 앞에서 우리는, $\hat{\beta_1} = (\sum_{i=1}^n{\hat{r_{i1}}y_i}) / (\sum_{i=1}^n{\hat{r_{i1}}^2})$ 인걸 보았다
    2. 그런데, 모든 $i$에 대해 $\sum_{i=1}^n{\hat{r_{i1}}y_i} = \sum_{i=1}^n{\hat{r_{i1}}}(\beta_0 + \beta_1x_{i1} + \beta_2x_{i2} + \cdots +\beta_kx_{ik}+u_i) = \beta_1\sum_{i=1}^n{\hat{r_{i1}}x_{i1}} + \sum_{i=1}^n{\hat{r_{i1}}}u_i$ 이다.
       * 왜냐면, $r_{i1}$이 $X_1$에 대해 다른 변수들을 회귀시킨 것이므로 다른 변수들과 직교하여 0이 되기 때문
    3. $\sum_{i=1}^n{\hat{r_{i1}}x_{i1}} = \sum_{i=1}^n{\hat{r_{i1}}(\hat{x_{i1}} + \hat{r_{i1}})} = \sum_{i=1}^n{\hat{r_{i1}}^2}$
       * 왜냐면, $\hat{r_{i1}}$와 $\hat{x_{i1}}$는 서로 직교하기 때문 (예측한 결과와 예측 잔차는 직교)
    4. $\hat{\beta_1} = \beta_1 + \frac{\sum_{i=1}^n{\hat{r_{i1}}u_i}}{\sum_{i=1}^n{\hat{r_{i1}}^2}}$
    5. 증명의 나머지는 단순회귀의 분산과 같다. $\beta_1$은 고정값이므로 제외되고, 두번째 항에서 분자는 단순회귀때와 마찬가지로 $var(u_i) = \sigma^2$이므로 최종적으로 위 식이 된다.

  
## 9.5 가우스 마코프 정리

* 설명변수 표본값들이 표본추출 반복시행 시 변화하지 않고 특이성이 없다고 하자.
* 오차평균0, 동분산, 오차간 독립 가정 하에서, OLS 추정량보다 더 분산이 작은 선형 비편향 추정량은 없다. (BLUE)

## 9.6 설명변수의 추가 또는 누락과 추정량의 분산

* Y에 영향을 미치지 않으면서 $X_1$과 연관된 변수를 우변에 추가하면, $X_1$ 변수내의 정보가 삭감되어 $X_1$ 계수 추정량의 표집분산이 커지고 정확도가 떨어진다.
  * 반대로 말하면 그런 변수 없이 단순회귀를 할 경우가 더 분산이 작아진다.
* Y에 대한 별도의 설명력을 가지면서도 $X_1$가 무관한 변수를 통제하면 설명불가 요인들의 변동성(오차항)이 줄어들면서도 $X_1$내의 정보가 삭감되지 않아 다중회귀가 단순회귀 보다 더 효율적인 추정량을 제공한다.

* 현실적으로 $X_1$의 계수가 주 관심사일 때, 
  * 무관한 변수는 우변에 포함시켜 통제하는 것이 좋고
  * 연관된 변수는 당초 부터 연구 목적상 포함시켜야 되는 게 아니라면, 제외하는 게 좋다
    * 그러나, 설명변수들이 무관한 경우는 거의 없다. 
    * 다른 변수가 통제된 상태에서 $X_1$의 변화가 $Y$의 평균에 미치는 영향에 관심이 있따면 포함시키는 게 좋다.
* 가장 설명력이 높으면서 가장 작은 모형을 찾고 할 경우, 일반적인 모형에서 가장 유의하지 않는 변수를 차례로 제거해나가는 방법을 쓰기도 한다.



## 9.7 OLS 추정량의 분산의 추정



* 우리가 n개의 자료를 갖고 있는 경우, 잔차항의 개수는 당연히 n개일 것
* 이 잔차들은 $k+1$개의 정규방정식 만족해야 함 
  * $\sum_{i=1}^n{\hat{u_i}=0}, \sum_{i=1}^n{x_{ij}\hat{u_i}=0}$
  * 결국, $n$개의 값 중, $n-(k+1)$개 만이 자유롭고 나머지 $k+1$개는 고정되어 있으므로,
  * $s^2 = \frac{1}{n-k-1}\sum_{i=1}^n{\hat{u_i}^2} = \frac{SSR}{n-l-1}$
* 단순회귀와 마찬가지로 OLS 추정량의 분산 추정량에 제곱근을 취한 것은 OLS 추정량의 표준편차의 추정량으로 '표준오차'(standard error)라 한다.



## 9.8 OLS 추정량의 표집분포

* $\hat{\beta_2} \sim N(\beta_2, var(\hat{\beta_2})), var(\hat{\beta_2}) = \sigma^2 / \sum_{i=1}^n{\hat{r_{i2}}^2}$



## 9.9 신뢰구간

* 단순회귀모형의 경우 $(\hat{\beta_1} - \beta_1)/se(\hat{\beta_1})$이 $t_{n-2}$ 분포를 갖는 반면,
* 다중회귀모형의 경우 자유도는 $n-k-1$이 된다. 

>$\frac{\hat{\beta_j}-\beta_j}{se(\hat{\beta_j})} \sim t_{n-k-1}$

* 신뢰구간 = 추정값 ± 임계값 × 표준오차



* 그런데, 만약 계수 추정량들의 선형결합의 표준오차를 구하려면 어떻게 해야 할까?
  * $\beta_1 + \beta_2$의 표준오차를 구하려면 
  * $\theta = \beta_1 + \beta_2$로 가정하고
  * $Y = \beta_0 + \beta_1X_1 + (\theta-\beta_1)X_2 + \beta_3X_3 + u$
  * 결국, $Y = \beta_0 + \beta_1 (X_1 - X_2) + \theta X_2 + \beta_3 X_3+u$
  * 위 식대로 하면, $\theta$를 추정할 수 있고 표본오차도 추정할 수 있다. 
* 우리는 위와 같은 방식으로 특정한 값을 가정했을 때, $y$값의 신뢰구간을 구할 수 있다. 
  * $Y = \beta_0 + \beta_1X_1 + \beta_2X_2$라고 할 때, $X_1 =500, X_2 = 10$이라면
  * $\theta = \beta_0 + \beta_1500 + \beta_210$이 되고, $\beta_0$에 대한 식으로 정리하여 그 식을 대입하면
  * $Y = (\theta-\beta_1500-\beta_210) + \beta_1X_1 + \beta_2X_2$이므로,
  * $Y = \theta + \beta_1(X_1-500) + \beta_2(X_2-10)$이 된다. 
  * 여기에서 $\theta$에 대한 표준오차가 나오므로 신뢰구간 추정 가능



## 9.10 예측

아래와 같은 순서로 진행되는 예시를 보자

1. $Y = \beta_0 + \beta_1X_1 + \beta_2log(X_2)+\beta_3X_3+u$
2. $y^0 = \beta_0 + \beta_1 \cdot 3 + \beta_2log(20) + \beta_3 \cdot(-1) + u^0$
3. $\theta = \beta_0 + \beta_1 \cdot 3 + \beta_2log(20) + \beta_3 \cdot(-1)$ , 여기서 $\theta$는 $X_1=3, X_2 =20, X_3=-1$인 모든 개체들의 평균 $Y$라는 것을 기억하라
4. $\hat{y^0} = \hat{\theta} = \hat{\beta_0} + \hat{\beta_1} \cdot 3 + \hat{\beta_2l}og(20) + \hat{\beta_3} \cdot(-1)$

이 위에서 모수 추정방식대로

1. $\beta_0 = \theta -3\beta_1-log(20)\beta_2 + \beta_3$
2. $Y = \theta + \beta_1(X_1 - 3)+\beta_2[log(X_2) - log(20)] + \beta_3(X_3+1)+u$

이제 여기에서, 

1. $y^0 = \theta + u^0$
2. $\theta + u^0 -\hat{\theta} = y^0 - \hat{y^0}$
3. $var(\theta + u^0 -\theta) = var(u^0) + var(\hat{\theta}) -2cov(u^0, \hat{\theta})= \sigma^2+var(\hat{\theta})$ , 지금까지 식이 모두 정규분포를 따르므로
4. $\frac{y^0- \hat{y^0}}{\sqrt{\sigma^2+var(\hat{\theta})}}\sim N(0, 1) = \frac{y^0- \hat{y^0}}{se(y^0 - \hat{y^0})} = \frac{y^0- \hat{y^0}}{[s^2+se(\hat{\theta})^2]^{1/2}} \sim t_{n-k-1} $


결국, $\theta$의 신뢰구간과 $y^0$의 신뢰구간은 크게 다를 수 있다. 

(사실 $\theta$는 계수들의 선형결합의 신뢰구간이며, 특정값일 때 평균 y)

$y^0$의 예측구간은 $\theta$뿐만 아니라, $u^0$에 의해서도 영향을 받는다. 

그 중 $u^0$은 특정 개체에 고유한 것이며, 아무리 큰 표본이 있다라도 $u^0$에 대한 정보는 얻을 수 없다. 

그래서 $\theta$보다 $y^0$의 신뢰구간이 더 커질 수밖에 없다.