---
title: Context-Aware Visual Compatibility Prediction 논문 정리
categories: [Deep Learning]
comments: true
---

# Context-Aware Visual Compatibility Prediction

인공지능으로 코디를 추천할 때, 단순한 상품 추천보다는 고려해야할 사항이 많다.    
  
의류 상품 추천은 사용자의 취향을 고려하여 비슷한 취향을 가진 집단의 데이터를 분석하여 추천하겠지만,
(~~사실 상품 추천에 대해 제대로 공부해본 적은 없다.~~)  
코디 추천은 상품의 시각적 요소를 분석하여 다른 상품들과 잘 어울리는지 고려되어야 한다.  
  
  이 논문에서는 graph neural network를 이용하여 코디를 추천하는 알고리즘을 소개한다.

