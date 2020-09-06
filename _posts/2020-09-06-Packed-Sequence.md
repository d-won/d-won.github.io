---
title:  "Pytorch-RNN-Packed Sequence"
excerpt: "Packed Sequence"

categories:
  - AI
tags:
  - Blog
last_modified_at: 2020-09-06
---

# Packed Sequence  
  
> ** 길이가 다른 데이터의 경우, 어떻게 하나의 Batch로 만들 수 있을까? **  
  
- Sequence Data들은 길이가 통일되어 있지 않은 경우가 많음 (예: 문장, 대화)  
- image의 경우 모든 image가 규격이 정해져 있는 것은 아니지만, 28 x 28 등 대표적인 규격들 존재  
- 컴퓨터가 인식하려면 동일한 크기 필요  
  
* 대표적으로 2가지 방법 존재
  * Padding Method : 가장 긴 문장에 맞춰 그보다 짧은 문장은 빈칸에 pad를 넣는 방법 (쉽지만, 계산하지 않아도 될 pad가 늘어남)
  * Packed Method : 문장의 길이를 함께 처리하여 한 개의 Pack으로 만드는 방법 (쓸 데 없는 pad 계산 안해도 되지만, 구현이 복잡함)
