```
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
```



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
