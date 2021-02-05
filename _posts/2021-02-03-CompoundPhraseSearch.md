---
title:  "조합 구절 검색"
excerpt: "힙알마(검색)"

categories:
  - etc
tags:
  - Blog
use_math: true
last_modified_at: 2021-02-03
---


## 4.6 **Search Methods for Merchandising**

- relatively generic search methods는 eCommerce에서는 아래와 같은 이유로 잘 통하지 않음
  1. Structured Entity: 각각의 상품별로 특성에 대한 데이터들 보유
  2. 상품 다양성: 검색하려는 구절과 관련해서 엄청나게 다양한 상품들이 연관될 수 있다 (빨간 구두 ↔ 드레스, 구두, 시계)
  3. 복합어와 다의어
     - Pink Rose라는 브랜드가 있을 경우, Pink Sweater는 해당 브랜드 제품에 매칭될 수도 있고
     - 반대로 Pink rose sweater는 Pink Rose의 스웨터 제품을 찾는 것이지만, Pink 또는 Rose 색상의 제품들을 찾을 수도 있다.
- 그래서 일반적 text가 아닌, 조금 더 구조화된 데이터에 적합한 '검색기법'이 필요 (해당 기법들은 Macy가 선도적으로 개발한 기술들)

### 4.6.1 조합 구절 검색

Pink rose sweater라는 복합어를 아래와 같이 구분해보자

> brand: [pink rose] , type: [sweater]

위와 같은 구분을 통해서 상품을 검색할 수 있다면 모호한 부분이 많이 사라지게 되고, 우리는 이런 기법을 차 판매사이트나, 부동산 사이트에서는 유용하게 활용 가능

But, 상품이 다양한 Commerce에서는 free text query가 더 적합하며 이를 위해 'query generation algorithm'이라는 기법이 존재

1. 구절 분리
2. 구절을 분리한 Partition 생성 
3. Partition 내 구절들과 데이터 scheme(?) 일치 확인
4. 모든 일치된 결과 결합하여 최종 결과 생성

'조합 구절 검색' 방법의 문제점은 Partition 개수가 구절이 많을 수록 지수적으로 증가한다는 데 있다.

- 그래서 현실에서는 일치 확인 구문의 복잡성을 줄이기 위하여 특정한 영역에서 특정 문구를 제외하기도 한다.
- 해당 기법은 semantic search 와 연결될 수 있고,
- semantic relationship을 semantic search만큼 파악하진 못하지만, 조합 구절의 일치 여부는 잘 파악할 수 있다.


### 4.6.2 일정 수준의 정확도 감소

조합 접근 방법의 가장 큰 문제점은 엄격하게 일치하는 것을 찾기 때문에 검색 실패 시 텅빈 결과 화면을 보여줄 수 있다는 것이다. 
(오타가 포함될 경우도 해당 문제 발생 가능)

검색 실패로 텅빈 창이 뜨는 것은 소비자 경험에 매우 안 좋은 영향

일정 수준의 정확도를 포기하는 대신, 이런 상황 방지를 위하여 우리는 몇가지 추가적인 조치 적용 가능하다.

- 특정 기본 조합에 무조건 매칭되게 만드는 방법
- 적어도 하나의 구절은 매칭되게 만드는 방법
- 표준화, 어간 추출, 구문 교정
- 특정 하위 구절 제외 후 재검색

### 4.6.3 Nested Entities and Dynamic Grouping

검색의 문제는 사실 디스플레이 공간의 효율적 활용의 문제

소비자에게 검색의도와 맞는 관련 상품들을 보여주는 것도 중요하지만,  한정된 공간안에서 상품 구색을 어떻게 보여주느냐도 매우 중요한 문제

예를 들면, 

동일한 드레스를 중심으로 색깔과 크기만 다르게 하여 보여주는 것보다

검색한 드레스와 관련이 있지만 다른 스타일의 드레스들을 보여주는 것이 더 합리적일 것이다.

그러나, 지금까지 검색 모델은 
상품간  hierarchical relationship을 기반으로 하고 있고 
이런 배경으로 인해 비효율적으로 디스플레이 공간을 보여주게 된다.

해당 사항 개선을 위해,
hierarchical structure를 제품 컬렉션이나, 다양한 제품들에 대응시켜야 한다.

1. Product variant(상품 구색?)을 별도의 문서로 모델링하여 검색 결과가 해당 Product variant에 매칭되게 하는 것 
▶️ 중복된 비효율적 Display 보여주는 현상 발생

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/639db487-4e3f-420f-8b95-9d61687baa7c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/639db487-4e3f-420f-8b95-9d61687baa7c/Untitled.png)

2. Product level document modeling은 위와 같이 중복 문제를 해결
▶️ 아래와 같은 2개 variant를 합칠 경우 문제 발생 
(구색에 존재하지 않는 비정상적 결과 도출)

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/45c88a2f-5df1-4d48-a29b-d244b57b96f6/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/45c88a2f-5df1-4d48-a29b-d244b57b96f6/Untitled.png)

3. 제품을 제품 컬렉션으로 통합시키는 방법
    - 고객이 어떤 의도로 어떤 검색 단어를 넣느냐에 따라 
    가변적으로 검색 결과를 보여줘야 함 (Dinnerware vs Cup)
    - 분석을 위해 heuristic merchandising rule 적용가능
    - 검색 단어(query)가 제품 컬렉션과 일치할 경우 개개 제품을 컬렉션으로 대체 가능

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fe26e18d-a4e9-462e-8e99-cb6da350be86/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fe26e18d-a4e9-462e-8e99-cb6da350be86/Untitled.png)

## 4.7 Relevance Tuning

앞서, 우리는 검색과 관련된 다양한 기법과 관련하여 fine tunning 하는 법과 평가 하는 법(Recall, Precision)을 보았고, 해당 지표들을 최적화하기 위한 relevance tuning 방법들을 알아볼 것이다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6372055d-e47d-4100-8dbd-c26a36a85e7f/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6372055d-e47d-4100-8dbd-c26a36a85e7f/Untitled.png)

Recall은 단일 검색/ 복수 검색 결과의 품질을 평가하는 데 활용 가능한 relevance metric

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/240499a6-c545-4eb6-8bf4-e360f16d9ac0/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/240499a6-c545-4eb6-8bf4-e360f16d9ac0/Untitled.png)

- Q는 가능한 query들, q는 query
- R(q)는 q(query)를 통해 전환된 평균 수익
- m(q)는 검색 결과 품질 평가 지표

모든  query를 활용하는 것이 아니라, 과거 데이터 기반 가장 많은 수익을 창출하는 query를 선택하고 해당 query 기반 최적화 가능

1. 서비스 성과에 제일 많은 기여를 하는 query set 결정을 위한 서비스 데이터 분석, 해당 query set을 benchmark query라고 함
2. 전체적인 검색 서비스 성과 측정을 위해 benchmark query에 대한 relevance metrics 계산 (위 Recall)
3. benchmark query에 대한 검색 결과들을 일일히 수동으로 분석하고 relevance metric을 향상시키기 위한 알고리즘 tuning 진행
4. 신규 평가 환경 설정을 실제 유저 표본으로 테스트하고, 적용 

위 작업은 지속적으로 반복되어야 함.

이를 위해 매우 많은 자원 투입을 필요로 하므로 bottleneck이 될 가능성이 높음. 해당 bottleneck 개선을 위해 아래 2가지를 해야 함

1. scoring 공식에 맞는 자동 tuning
2. 검색 서비스와 유저의 상호작용 분석 기반, 검색 품질 자동 평가

### 4.7.1 Learning to Rank

가장 우선적 목표는 query와 context들에 rank를 매기는 일이며, 해당 문제는 '분류', '회귀' 문제로 볼 수 있으며, rank에 대한 정확한 예측이 필요. 예측 후 query와 context를 rank에 따라 정렬. 

이런 문제를 'Learning to Rank'라고 표현함

해당 문제에 대해서는 학계에서부터 산업계까지 엄청나게 많은 분석이 진행되었고 관련하여 많은 연구 논문부터 산업 보고서, test data set이 존재하고 엄청나게 많은 model들이 존재함.

(Learning to Rank 관련 다양한 알고리즘 목록은 [Liu, 2009] 확인 가능)

본격적으로 Learning to Rank 모델을 살펴보면,

- Q 개 sample을 보유한 training set이 존재하고
- $q$는 검색 query, $m_q$는 검색 결과
- 그래서 1개 sample당 검색 query와 검색 결과가 쌍으로 존재
- 그리고 해당 검색 품질에 대한 relevance grade는 categorical 변수로 존재 (1-완벽, 2-우수, 3-평균)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8d469ed7-de78-46b5-a465-9bf0173c9e18/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8d469ed7-de78-46b5-a465-9bf0173c9e18/Untitled.png)

우리는 위와 같은 데이터를 기존 검색 데이터를 가져오고, 전문가 판단에 의해 grade를 메길 수 있다. 그리고, 다른 '지도학습' 문제들과 마찬가지로 feature engineering 과정이 포함된다.
우리는 위와 같은 데이터를 기존 검색 데이터를 가져오고, 전문가 판단에 의해 grade를 메길 수 있다. 그리고, 다른 '지도학습' 문제들과 마찬가지로 feature engineering 과정이 포함된다.

Document Features 

- 기본적인 document 통계치
- 제품 타입, 가격 카테고리

Query Features

- 기본적인 query 통계치
- query 빈도, CTR 등

Document-Query Features

- Document와 Query 모두를 기반으로 하는 feature

다음으로 해야 할 것은 Loss Function에 대한 정의

1. Pointwise : 각각의 document에 대해서 독립적으로 예측을 진행한 후, 산출된 loss를 모두 sum하여 전체 loss를 구하는 방식. But, 해당 방법은 rank를 고려하려는 우리의 목적과 다르게 질적, 정량적 예측치만을 산출
2. Pairwise: pair로 document를 선정하여 해당 pair끼리 순서가 반전되는 것을 최소화하는 방식. ranking을 구한다는 본래 목적에 적합하므로 pointwise보다 성능이 좋음
3. Listwise: 전체 document list를 넣고, 최적의 rank를 찾는 것. 

참고사이트

1. [https://yamalab.tistory.com/119](https://yamalab.tistory.com/119)
2. [https://renuevo.github.io/data-science/learning-to-rank/](https://renuevo.github.io/data-science/learning-to-rank/)
3. [https://checkwhoiam.tistory.com/24](https://checkwhoiam.tistory.com/24)

이제 학습 데이터와, loss function을 정했다면 model을 정할 차례인데

야후와 마이크로소프트의 경험에 따르면, decision tree, neural net 그리고 앙상블 모델을 많이 활용

우리는 McRank 알고리즘에 대해 살펴볼 예정 

- McRank는 GBDT model을 활용하고 k개의 카테고리에 대한 classfication 진행
- GBDT이므로 loss function smoothing 진행 (label smoothing?)

### 4.7.2 Learning to Rank from Implicit Feedback

전문가가 grade를 부여하는 것은 매우 많은 자원을 투입해야 하는 일이므로 해당 문제를 효율적으로 해결하기 위해서는 시스템이 유저와 상호작용을 기반으로 한 결과를 활용하여 자동으로 relevance grade를 부여하는 것이 필요 (예: 아무도 클릭하지 않은 결과는 당연히 검색결과 품질이 안 좋은 것)

우리가 살펴볼 모델에서는 2개의 relevance feedback rule을 고려

1. 만약 유저가 검색 결과 중 특정 document를 클릭한다면, 해당 document는 다른 document에 비해 relevance가 높음
2. eye tracking 연구를 통한 실증적 근거를 기반으로 보았을 때, 유저는 일반적으로 검색 결과 중에서 최소한 최상단의 2개까지는 보고 행동한다. 그러므로, 유저가 최상단의 첫번째 document를 클릭했다면, 두 번째 보다 적합도가 높다는 것이다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0951f85c-4dbd-4677-aa27-843c84657e2e/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0951f85c-4dbd-4677-aa27-843c84657e2e/Untitled.png)

유저는 보통 1번만 검색하는 것이 아니라, 2번 3번 검색을 하는 경우가 많다. 

유저가 유사한 query를 2번 이상 검색했다고 하자. 

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ab0b5f45-caa7-4d05-abec-a0c0def58260/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ab0b5f45-caa7-4d05-abec-a0c0def58260/Untitled.png)

위와 같은 부등호는 Rule 1,2를 2번째 query까지 확장시킨 결과이며, 우리는 위와 같은 규칙을 통하여, 전문가의 판단 없이도 학습 데이터 셋에 Rank 작업을 진행할 수 있다. 해당 Rank 작업은 TF IDF모델을 통해 나온 결과도 함께 고려하여 반영할 수 잇다.

https://www.notion.so/4-6-4-8-7810bee6eea3435384eba24b069d2227


