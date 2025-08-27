---
title:  "Fast AI - Lesson 3: The Basics"
author: "Woohyuk Jang"
draft: false

date: "2021-05-25"
description: ""
categories:
  - CS/AI/FastAI
tags:
  - AI
---

블로그 포스트 다시 정리해서 써보기.

이번 레슨은 머신러닝에서의 가장 기초적인 개념들에 대해 학습한다고 한다.

## 1. 키워드
- arrays, tensors, broadcasting
- SGD (stochastic gradient descent)
- loss function
- mini batch

## 2. 머신러닝의 기초적인 개념

### Array & Tensor
- 다차원으로 쌓은 상자들?의 이미지를 생각하면 될듯
- rank: 몇개의 축을 가진 데이터인지 말해준다. 예를 들어 rank가 2이면 텐서들로 이루어진 텐서 꼴인 것이다.
- shape: 각 축의 길이를 말해 준다. 예를 들어 [28, 28]은 28개의 row와 28개의 column을 가졌다는 것이고, [1010, 28, 28]은 28*28 정사각형이 1010개 쌓였다고 생각하면 된다.

**Array 와 Tensor의 이점**
- 대체로 C로 컴파일된 메소드들을 가지고 있음: 빠르다

**Numpy 와 Pytorch**
- Numpy의 장점: 자유로운 형태를 가질 수 있다. 예를 들면 jagged array (array 안에 길이가 다른/type이 다른 array들이 있는 것). Pytorch는 숫자들로 구성된 길이가 같은 텐서들로 이루어져 있어야 한다. (그러니까 직사각형이나 큐브처럼 이루어져야 한다.)
- Pytroch의 장점: numpy에는 없는 GPU와 미분 (back propagation) 지원이 있다.

### L1 Norm, L2 Norm
- L1 Norm: 편차의 절댓값의 평균: `(x-y).abs().mean()`
- L2 Norm: 분산 (편차의 제곱의 평균에 루트를 씌운 것): `((x-y)**2).mean().sqrt().`
- 물론 pytorch에서 L1, L2 Norm 관련 메소드가 있다. (아래 유용한 pytorch 연산 정리 참고)
- L1 norm과 L2 norm의 차이: L2 norm은 L1에 비해 더 큰 오류에 민감하고 작은 오류에는 덜 민감하다

### Weights, Bias, Parameters
- Parameters: 머신러닝 모델에서 트레이닝 하면서 변하는 것
- Weight: y = w * x + b 에서 w
- Bias: y = w * x + b 에서 b

### Matrix Multiplication
- y = w * x + b를 모든 트레이닝 데이터셋에 대해 for loop을 도는 대신, matrix multiplication을 이용하면 효율적이고 GPU를 이용할 수도 있어서 빠르다.
- python 그리고 pytorch에서 matrix multiplication은 @로 나타낸다.
- `batch @ weight + bias`

### Activation Function
- 숫자들을 해당 분류에 해당할 확률? 같은 것으로 바꿔준다고 일단 이해했다.
- sigmoid의 경우, y값이 0과 1사이에서 왔다갔다하는 커브이다.

## 3. 딥러닝 모델의 구조
1. Parameter 초기화
  - 일반적으로 그냥 random으로 설정한다.
  - 미리 훈련된 다른 모델에서 가져올 수도 있다 (transfer learning)
2. Predict
3. Loss: 실제 레이블과 예측의 차이
  - 미분가능한 함수여야 한다.
4. Gradient: 각각의 parameter을 어떤 방향으로 바꿀지 계산하기 위해
5. Step(Gradient를 근거로)
  - step의 양은 gradient * lr (learning rate)
  - pytorch에서는 step을 한 뒤에 `parameters.grad = None`을 해줘야 한다. ? 왜?
6. Repeat
7. Stop (특정 기준에 의해)
  - 너무 오래 걸려서
  - 모델이 충분히 좋아서 (metric이 특정 기준 이상)



## 4. 유용한 머신러닝 팁

### Baseline Model을 구축하라
- 종종 아주 멋진 모델보다 그냥 간단한 모델의 성능이 더 좋을 때가 있다.
- 그러므로 Baseline model을 구축하고 그 이후의 모든 시도들이 baseline model보다 더 좋은 성능을 보이도록 해야 한다.
- baseline model을 구축할때는 정말 간단하고 짜기 쉬운 모델을 짜거나 기존에 다른 사람이 만든 모델을 이용할 수 있다.

### 중간중간 tensor의 shape를 확인해라.
- shape가 이상해지면 좋을 것 없다.

### Broadcasting을 이용해라.
- pytorch에서는 broadcasting을 이용하여 알아서 tensor의 차원을 확장시켜준다.
- 대부분의 loop는 broadcasting으로 대신할 수 있다.
- Broadcasting은 C언어로/Cuda로 GPU에서 일어나므로 훨씬 빠르고, 메모리도 덜 사용한다.
- broadcasting을 이용하면 여러 shape의 텐서를 입력으로 받아도 둘다 작동하는 함수를 만들 수 있따.



## 5. 유용한 Pytorch 연산 정리

### 기본 연산
- 생성: `tensor()`
- 인덱싱: [1], [:, 1]. python에서의 인덱싱과 동일하다. 처음은 포함, 마지막은 미포함.
- 사칙연산: `+`, `-` ,`*`, `/`. Broadcasting 또는 element-wise로 이루어진다.
- 타입: `.type()`. 다만 알아서 type change도 해준다.
- 복제: `.clone()`

### shpae 조정
- `len(텐서)` 또는 `.ndim`: rank를 반환한다.
- `.shape`: shape를 반환한다.
- `stack`: shape가 같은 여러개의 tensor을 쌓아서 하나의 tensor로 만든다.
- 타입 변화: 변화시키려고 하는 type을 메소드처럼 이용한다. ex) `.float()`
- `.view`: tensor의 shape를 바꾼다. 인자로는 목표로 하는 shape를 파라미터로 넣는다. `-1`을 인자로 넣으면 필요한 만큼 알아서라는 뜻이 된다. 예) `.view(-1, 28*28)`
- `.unsqueeze`: 하나의 차원을 추가한다.

### 루프 대체
- `.cat`: concatenate, 합치기
- `.mean`: 평균을 반환한다. 만약 0,1,2등의 인덱스가 주어질 경우, 그 axis을 가로질러서 평균을 낸다. 예를 들어 shape가 [1010, 28, 28]인 텐서에서 `.mean(0)`을 하면 [28, 28] 텐서가 반환하는 식이다.
- `.where(condition, x, y)`: condition이 성립하면 x, 그렇지 않으면 y를 가지는 텐서를 반환

### L1 Norm, L2 Norm
torch.nn.functional 모듈에서 구현되어 있다. Pytorch 팀에서는 torch.nn.functional을 F로 import하기를 권한다.
- L1: `F.l1_loss()`
- L2: `F.mse_loss().sqrt()` (정확히 말하자면 l2 norm이 아니라 mse가 구현되어 있다.)

### 미분
- 당연히 어떤 사이즈의 텐서이건 미분 할 수 있다.

1. 파라미터 텐서를 고른 후 .requires_grad_()로 설정한다.
  - 텐서에 gradient function을 추가하는데, 여기에 우리가 어떤 연산을 할 때마다 이제 pytorch가 자동으로 함수를 추적해서 나중에 gradient를 계산할 수 있도록 한다.
  - 여기서 메소드가 _로 끝나는 것은 우리가 실제로 텐서를 바꾸고 싶다는 의미이다.
  - 예: `x = tensor(3.).requires_grad_()`
2. 필요한 연산을 해서 새로운 텐서에 저장한다.
  - 예: `y = x ** 2`
3. 그 새로운 텐서에서 `.backward()` 메소드를 부른다. 그러면 pytorch가 gradient를 계산한다. 여기서 backward는 backpropagation을 의미한다.
  - 예: `y.backward()`
4. 원래 데이터 텐서에서 `.grad` 속성을 확인한다.
  - 예: `x.grad`

**주의**
  - grad가 걸려있는 텐서에 계산을 수행할때, 모델에 포함되지 않는 연산이면 .data를 이용해 수정해야 한다. 그러지 않으면 pytorch는 그 연산도 모델의 일부라고 생각한다.

### Dataset 만들기
- Pytorch에서 데이터셋은 아주 구체적이고 한정적인 의미를 가지고 있다.
- 데이터셋은 인덱싱 되었을 때 (x,y) 튜플을 반환해야 한다.
- 구현: `list(zip(train_x,train_y))`

- array & tensor
- python & pytorch tensor programming trics with the baseline model
- L1, L2 norm
- broadcasting
- gradient descent
- cool pytorch features
