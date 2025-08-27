---
title:  "Fast AI - Lesson 2 Revised"
author: "Woohyuk Jang"
draft: false

date: "2021-05-25"
description: ""
categories:
  - CS/AI/FastAI
tags:
  - AI
---
## A. The practice of deep learning
- 딥러닝의 한계와 가능성을 모두 염두에 두고 있어라. (지나친 낙관/비관 x)

### 1) Starting your project
- 프로젝트 접근 방법: 완벽주의 X, 일단 간단하게 만들고 나중에 발전시켜라
- end-to-end, 즉 데이터 수집부터 서비스(GUI/앱)을 만들기까지의 과정을 대충 끝내고, 그 다음에 추가 학습/발전하는 과정을 여러번 반복하기. 특히 데이터셋의 접근성에 유의
- **이 책을 학습하는 방법: 클론 코딩처럼 새로운 데이터셋을 이용하여 노트북을 처음부터 다시 만들어라**
- 초보일때는 잘 알려진 분야부터

### 2) The state of deep learning
- computer vision
    * (심지어는 해당 과제에 전문적으로 훈련받은) 인간 수준이다. 
    * 그러나 out-of-domain, 즉 트레이닝 데이터와 아주 약간 다른 데이터는 잘 다루지 못한다. 
    * ex) 고양이 사진 학습 --> 고양이 그림 인식 (X).
    * 레이블링 작업이 돈이 많이 든다: Image Augmentation을 이용하면 보다 적은 레이블링으로 훈련시킬 수 있다.

- text (NLP)
    * 텍스트 분류, 상황/맥락에 맞는 말은 잘 한다. 그러나 맞는 말은 하지 못한다. 그러니까 그럴 듯하게 들리는 헛소리를 하고 있는 것이다. 
    * 텍스트 생성은 잘 할 수 있다. GAN의 특성상 인공지능이 생성한 텍스트를 찾아내는 모델보다 텍스트 생성 모델이 항상 더 낫다.
    * 인공지능 모델을 사용하여 구별하기 힘든 그럴듯하게 들리는 거짓 텍스트를 대량 생산하는 것은 사회적으로 악영향을 끼칠 여지가 다분히 있다.

- combining text and images

- tabular data & time series
    * 아직은 Random Forest나 Gradient Boosting등 앙상블 기법과 성능은 비슷하지만, 속도가 좀더 느리다 ㅠ
    * 대신에 데이터 자체에 텍스트나 이미지 등을 포함할 수 있다.

- recommendation systems
    * 그냥 독특한 종류의 tabular data이다.
    * high-cardinality data (사용자 ID처럼, 서로 공통점이 거의 없는 불연속적인 데이터로 이해했다)와 이미지, 텍스트, 과거 검색기록 등을 포함함 --> 다양한 데이터를 혼합할때 머신러닝 이용

- other data types
    * 일반적으로는 그냥 위에서 언급한 것들 중에 하나로 만들면 된다. ex) 소리 --> 주파수로 이미지로 만들어서 분류

### 3) The Drivetrain Approach
[Designing great data products](https://www.oreilly.com/radar/drivetrain-approach-data-products/)
Drivetrain Approach는 그냥 단순히 작동하는 것이 아닌 유용한 모델을 만들기 위해서 생각해볼 것들을 정리한 것이다.

[drivetrain_approach](/assets/images/drivetrain-approach.png)

**왜 모델을 만드는지 생각해보아야 한다.**
현실 세계에 모델을 적용할때는 단순히 현상을 기술하거나 예측하기 위해 모델을 만드는 것이 아니라, 뭔가 목표를 달성하기 위해 모델을 만드는 경우가 많다.

Drivetrain Approach의 과정

1. 목표 정하기
2. 레버 찾기
- 레버는 목표를 달성하기 위해 바꿀 수 있는 것들을 의미한다.
3. 데이터 수집
- 아무 데이터나 막 수집하는 것이 아니라, 레버들이 목표에 어떤 영향을 끼치는지에 대한 정보를 담고 있는 데이터를 수집해야 한다.
4. 모델 만들기

예시: 아마존 상품추천

1. 목표 정하기: 장기적 매출 증가 (즉, 사용자의 구매량 증가)
2. 레버 찾기: 상품 추천의 배열 순서
3. 데이터 수집: 상품 추천에 따른 사용자의 구매 여부 A/B 테스팅 등을 이용
4. 모델 만들기: 예를 들어서 추천하지 않았을때 사용자의 구매 확률과 추천했을때 사용자의 구매 확률을 예측하는 모델을 만들 수 있다.

## B. How to avoid disaster

**핵심 자료: [Building Machine Learning Powered Applications](https://www.oreilly.com/library/view/building-machine-learning/9781492045106/)**

### Handling the Complexity
- 뉴럴 네트워크는 너무 복잡하기 때문에, 일반적인 컴퓨터 프로그램처럼 분석적으로 이해할 수 없다.
- 문제가 되는 것들: out-of-domain data(e.g. 인터넷에 올라온 이미지와 실제 현장에서 볼 수 있는 이미지의 차이), domain shift (환경이 변함. 예를 들어 곰을 추적하는 시스템을 만들었는데, 이제 곰 대신 뱀이 나타남)

- 그러므로 아래 그림과 같은 방법으로 서서히 활용범위를 넓혀 나가야 한다.
[Handling Complexity](/assets/images/handling_complexity.png)

- 모델이 의도대로 제대로 작동하고 있는지 평가할 수 있는 reporting system이 필요하고, 잘못될 수 있는 상상할 수 있는 모든 경우에 대해 이에 대응하는 reporting system이 있는지 생각해보아야 한다.

### unforseen consequences and feedback loops
- 특히 bias가 있는 환경에서, 피드백 루프를 통해 인공지능 모델이 그 bias를 증가시킬 수 있음
- 이러한 피드백 루프에서 빠져나갈 수 있도록 여러 안전장치들과 인간 관리 등을 추가할 수 있음.
