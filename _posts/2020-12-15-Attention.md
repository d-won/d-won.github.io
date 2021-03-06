---
title:  "Attention Mechanism"
excerpt: "Attention 설명"

categories:
  - AI
tags:
  - Blog

use_math: true
last_modified_at: 2020-12-15
---

* 아래 내용은 '밑바닥부터 시작하는 딥러닝2'를 참고하였습니다.

### Seq2Seq의 문제점

* Encoder 출력이 '고정 길이의 벡터'이므로 필요한 정보를 다 못 담을 수 있음

### Encoder 개선

* Seq2Seq는 LSTM 계층의 마지막 은닉 상태만을 Decoder에 전달했다면,
* 단어별 LSTM 계층의 은닉 상태 벡터를 모두 이용하는 게 첫번째 개선점
	* 5개의 단어라면 5개의 벡터가 출력되므로 '고정 길이의 벡터' 단점에서 벗어날 수 있음
	* 해당 벡터들은 각 단어별 정보를 담고 있음
* 앞으로 은닉 상태 벡터 모은 걸 $hs$로 표현

### Decoder 개선 (1)

* 번역을 할 때 중요한 건 각각 단어에 대한 대응 
	* 예를 들어, '나는 고양이다' 라는 문장을 'I am a cat'으로 번역할 때
	* 'cat'은 고양이와 대응이 되어야 함
* 해당 작업을 하려면, 결국 번역 단어별로 이전 Encoder 단어에서 대응 되는 부분 선택 필요
* '선택' 작업을 미분으로 대신하기 위해 '가중치' 벡터 생성 ($a$)
	* 위 가중치 벡터는 0~1로 이뤄지며 모두 합하면 1이 되게 생성
* 여기에서 $hs$와 $a$ 사이에 가중합을 구하면 '맥락 벡터'인 $c$를 구할 수 있음
	* 예를 들어 '나'라는 단어에 가중치 0.8이 곱해져서 더해진다면 해당 맥락벡터는 '나' 벡터의 성분을 가장 많이 포함
	* 가장 많이 포함한다는 게 결국 선택되는 것이라고 해석 가능