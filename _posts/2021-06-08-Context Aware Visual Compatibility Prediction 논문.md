---
title: Context-Aware Visual Compatibility Prediction 논문 정리
categories: [Deep Learning]
comments: true
---

# Context-Aware Visual Compatibility Prediction
(논문 출처: https://arxiv.org/abs/1902.03646)

인공지능으로 코디를 추천할 때, 단순한 상품 추천보다는 고려해야 할 사항이 많다.    
  
의류 상품 추천은 사용자의 취향을 고려하여 비슷한 취향을 가진 집단의 데이터를 분석하여 추천하겠지만,
(~~사실 상품 추천에 대해 제대로 공부해본 적은 없다.~~)  
코디 추천은 상품의 시각적 요소를 분석하여 다른 상품들과 잘 어울리는지 고려되어야 한다.  
  
  이 논문에서는 graph neural network를 이용하여 코디를 추천하는 알고리즘을 소개한다.

## 용어 정의  
- 옷의 context: 그 옷이 잘 어울리는 옷들의 집합을 의미한다.
- vertices: '그래프'라는 자료 구조에서 정점을 뜻한다.
- edges: '그래프'라는 자료 구조에서 vertex들을 잇는 경로라고 이해하면 된다.
- outfit: 하나의 코디 세트를 의미한다.
- compatible: 같이 입었을 때 어울린다는 뜻이다.
- extend: outfit에 아이템 하나를 추가하여 compatible한 outfit을 만든다.

## Proposed Method
여기서 제시한 모델은 graph auto-encoder framework를 기반으로 한다. encoder는 input으로 incomplete graph를 받고, 각 노드에 대한 embedding을 output으로 내놓는다.  
그 후 decoder는 이 embedding을 활용하여 incomplete graph에서 빠진 edge를 예측한다.
  
  이제 여기서 사용되는 그래프를 살펴보자. Undirected graph, 즉 edge의 방향이 정해져 있지 않으며, 이 말은 즉 출발점과 도착점이 정해져있지 않다. 
  그래프의 각 노드는 옷의 이미지에서 뽑은 특징들의 벡터가 담겨있다. (~~구체적인 수식은 논문에서 확인하길 바란다.~~)  
  이 노드들에 담긴 특징은 R이라는 행렬에 저장한다. 또한, 노드 간의 관계가 edge로 연결되어 있으면 1, 아니면 0으로 나타내어 adjacency 행렬 A에 저장한다.
      
  이 모델의 목적은 이 두 행렬로부터 encoding과 decoding 함수를 학습하는 것이다.
  Encoder는 adjacency matrix를 이용해서 옷의 초기 특징 X를 새로운 representation으로 나타낸다. 초기 이미지에서 CNN으로 뽑은 feature인 벡터 $\vec{x_i}$에 저장하고, 이를 새로운 representation인 벡터 $\vec{h_i}$로 나타내는 것이다. 이때 여기서 deep Graph Convolutional Network(GCN)를 사용한다.  
  Decoder는 encoder에서 내놓은 특징들을 이용하여 item i와 j가 compatible한 확률을 계산한다. 즉, 각 노드가 edge로 연결되어 있을 확률을 계산하는 것인데, 이 과정을 metric learning이라고 한다. 
  
## Tasks
이 논문에서는 위의 모델을 활용한 2가지 적용 방법을 제시한다.
1. Fill In The Blank (FITB)
FITB에서는 outfit에서 두 아이템마다의 comptibility를 계산하여 그 합으로 compatibility score를 계산하는 방식이다. 그래서 예를들어 4가지 아이템으로 구성된 outfit이 있을 때 나머지 하나의 item이 어느 것이 가장 적합할지 compatibility score가 높은 것으로 판단한다. 
1. Outfit Compatibility Prediction
이 방식에서는 outfit에서 각 edge가 연결되어 있을 확률을 평균내서 compatibility score를 구한다. 1로 가까울수록 compatible한 것으로 나타난다.
  
  
  그 뒤 논문 내용은 활용된 dataset과 train한 결과들을 제시하고 있다. 알아서 읽어보길 바란다.



  
