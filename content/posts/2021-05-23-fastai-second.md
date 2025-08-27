---
title:  "Fast AI - Lesson 2"
author: "Woohyuk Jang"
draft: false

date: "2021-05-23"
description: ""
categories:
  - CS/AI/FastAI
tags:
  - AI
---
Fast AI 2강에서 이론적인 부분을 정리한 것이다.

** 책을 보고 좀 더 자세히 정리한 내용을 https://whjang-0421.github.io/ai/fastai-second-revised/에 정리해두었다. 3강부터는 책 내용을 보고 정리한 내용과 동영상 강의를 본 내용을 함께 정리해 두려고 한다.

## 1. The State of Machine Learning
[State of Machine Learning](assets/images/state_machinelearning.PNG)
- 흥미로운 점은 머신러닝이 대화에는 별로 성능이 좋지 않다는 것이다. 즉, 머신러닝을 통해 뭔가 대화처럼 보이는 것을 만들 수는 있지만 실제로 사실인 말을 하게 만들 수는 없다는 점이다.

## 2. Interpreting Models: P-values
- P-values are terrible: [American Statistical Association Releases Statement on Statistical Significance and P-Values](https://www.amstat.org/asa/files/pdfs/p-valuestatement.pdf)
- multivariate model을 사용하면 낮은 p-value를 얻을 수 있음.

- p-value에서 주의사항: p-values > 0.05여도 대립가설이 기각되는 것은 아님. 그저 귀무가설이 기각될 수 없다는 것을 의미.

## 2. Insights for Deploying Predictive Models

[Building Machine Learning Powered Applications: Going from Idea to Product](https://www.amazon.com/Building-Machine-Learning-Powered-Applications/dp/149204511X)

### Prediction vs Action
- 머신러닝은 단지 예측만 할 뿐, 무엇을 할지 알려주는 것은 아니다. 예) 아마존 상품추천: 설령 이미 아는 작가의 상품을 살 확률이 높아도 알지 못하는 작가의 상품을 사게 하는 것이 결과적으로 매출 증가에 도움이 될 수 있다.
- 예측만 하는 모델을 통해서 실제로 행동의 변화를 이끌어내기 위해서는 다른 과정이 필요하다.
- [Designing Great Data Products](https://www.oreilly.com/radar/drivetrain-approach-data-products/)
- 데이터를 이용하여 가치를 창출하는 4단계: 목표 정의 --> 레버 (조절할 수 있는 입력 즉 독립변수) 찾기 --> 데이터 --> 모델
- 책 appendix에 관련 내용이 있다고 함.

### Feedback Loops
- 모델을 실제 세계에 적용할때, 환경이 바뀌어버리면 피드백 루프가 생길 수 있다. 모델의 예측 결과가 다음에 받을 트레이닝 데이터에 영향을 주는 한, 이런 피드백 루프를 피하기는 사실상 불가능하다.
- 그러므로 데이터를 "객관적인 관찰 결과"가 아닌 모델과 세계의 상호작용의 결과로 바라보고, 시스템 모니터링 (인간 관리)를 추가해야 한다.
- 예: predictive policing algorithm


cf) 블로그 팁
- [Advice for Better Blog Posts](https://www.fast.ai/2019/05/13/blogging-advice/)
- 블로그를 쓰는 것이 개발자로서 매우 유용한 일임을 다시 한번 확인했다.
