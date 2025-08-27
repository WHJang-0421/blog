---
title:  "Fast AI - Simple Cat Classifier"
author: "Woohyuk Jang"
draft: false

date: "2021-05-24"
description: "간단한 CNN 모델 만들어보기"
categories:
  - CS/AI/FastAI
tags:
  - AI
---
 
# 지금까지 이해한 것을 가지고 간단한 CNN 모델 (고양이 분류기)를 만들어보았다. 5가지 고양이 종류 중에서 구분할 수 있는 모델이다.

## 구현 소스 및 웹사이트
- 소스코드: [https://github.com/WHJang-0421/cat_classification_model/tree/master](https://github.com/WHJang-0421/cat_classification_model/tree/master)
- prototyping된 웹서비스: [https://mybinder.org/v2/gh/WHJang-0421/cat_classification_model/HEAD?urlpath=voila%2Frender%2Fcat-classifier.ipynb](https://mybinder.org/v2/gh/WHJang-0421/cat_classification_model/HEAD?urlpath=voila%2Frender%2Fcat-classifier.ipynb)

--------------------------------------------------------------------------------------------------------------------
## 기술적인 구현 관련

### 큰 그림
1. bing image downloader을 이용하여 이미지 다운로드
2. Dataloaders 객체를 이용하여 전처리
3. Learner 이용 CNN 모델
4. 모델을 만든 후 ImageClassifierCleaner로 데이터 정리
5. Confusion Matrix
6. 모델 파일로 내보내고 jupyter app 만들기

### DataLoaders
- dataloader 객체를 train, valid 데이터셋으로 저장해줌. dataloader 객체는 GPU로 mini_batch를 보내는 클래스.
- fastai 라이브러리에서 데이터 전처리를 맡고 있음.

만드는 방법)
1. 생성을 위해 필요한 정보를 데이터 블록에 넣는다. 
  * 데이터의 종류: (독립변수, 종속변수)
  * 데이터를 얻는 함수: 예를 들어 get_image_files 함수는 경로를 입력으로 받아 모든 이미지 파일의 경로를 반환한다.
  * 레이블링을 담당하는 함수
  * validation set을 만드는 방법 (splitter)
  * item_tfms: mini_batch를 만들기 위해 데이터의 size를 동일하게 맞추어 주는 함수

2. 만든 데이터 블록 객체에 데이터의 경로를 더 알려준다. (Datablock의 .dataloaders 메소드 이용)

3. 데이터 블록에서 데이터의 종류, 데이터를 얻는 함수 등은 대부분 factory method로 만들어져 있다. 그러나 만약 추가적 구현이 필요하다면 data block api를 이용하여 나만의 함수를 만들 수 있다.

4. .new 메소드를 이용해서 기존의 설정에서 새로운 설정을 추가한 새로운 datablock를 만들 수 있다.

### Resize Methods
- Crop: 일부분을 (주로 중앙) 자른다. 이미지의 일부분을 잃는다는 문제점이 있다.
- Squish: 말 그대로 누른다. 모양이 달라진다는 문제점이 있다.
- Pad: 이미지 바깥 부분을 검은 픽셀/흰 픽셀 등으로 채운다. 패딩된 부분에서 컴퓨팅 파워가 낭비되고 나중에 이미지의 화질이 안 좋아지는 문제점이 있다.
- **RandomResizeCrop**: 가장 일반적으로 사용되는 방법. 일부분을 자르되 랜덤으로 위치와 크기를 약간씩 다르게 한다. 이를 통해 모델은 위치나 각도 같은 것이 조금 변해도 feature을 파악하는 방법을 알게 되고, 결과적으로 데이터 전체에서 이미지가 보존된다는 장점이 있다.

### Data Augmentation
- input data의 본질은 바꾸지 않고 그냥 돌린다던지 밝기를 바꾸던지 해서 조금 다르게 보이게 하는 것.
- **주의사항: Data Augmentation을 통해 데이터의 labeling이 바뀌면 안됨!** 예를 들어 medical data를 다룰때 data augmentation을 하면 병명이 달라질수도. 그런 결과를 낳는 data augmentation은 피해야.
- fastai 라이브러리의 경우, aug_transforms로 정리
- 각각의 batch별로 적용하기 위해서 datablock 객체를 생성할 때 batch_tfms 인자에 넣어줌 (각각의 batch 별로 적용하는 이유: 일단 size가 같아진 다음에 augmentation을 해야 해서)
- 일반적으로 validation set 보다는 training set에만 사용함.

### Data Cleaning
- 많은 데이터 과학자들은 데이터 정리에 자기 시간의 90% 이상을 쓴다고 함.
- 꼭 모델을 만들기 전에 데이터를 정리할 필요는 없음. 대략적인 모델을 만든 다음에 그 모델을 이용해서 데이터를 정리하는 것이 더 빠르고 편함.

### Exporting
- 아키텍쳐와 파라미터, 그리고 데이터의 전처리 방법을 내보내야 함.
- .export() 메소드를 사용: dataloader의 속성까지 기억하므로, 데이터를 어떻게 전처리해서 모델에 집어넣을지도 다 내보냄.
- .pickle 확장자
- 모델을 훈련시키는 것이 아니라 예측하는데 사용할때는 inference라고 부름. 

### Building Apps
- Ipywidegets: Jupyter notebook에서 javascript와 ipython을 함께 사용해서 만든 GUI
- Voila: jupyter notebook에서 코드는 숨기고 마크다운과 output widget만을 처리하는 주피터 기능
- Binder: 주피터 노트북을 온라인 서비스로 바로 만들어주는 서비스
- prototype/취미로 만드는 프로젝트 정도면 굳이 GPU를 쓸 필요는 없음. 그냥 CPU로도 충분. 또 굳이 엣지 컴퓨팅을 쓸 필요도 없음.
-------------------------------------------------------------------------------------------------------------------
## 느낀점
### 이 모델 구현으로 얻게 된 것
- 인공지능 모델을 훈련시키고 그럴듯한 GUI로 만드는 전체 과정에 대한 감을 얻었다.
- jupyter notebook 내에서 git과 github를 사용했다. 뭐 노트북이라고 막 다른 것은 아니고 그냥 할 수 있음을 인식했다.

### 부족한 점
- 사용한 Fastai 라이브러리와 Voila, Binder에 대한 이해가 부족하다. 특히 Voila & Binder 서비스는 이용하면서 오류가 계속 나서 헥헥거렸다. 
- 아직은 코드몽키같은 느낌으로 코드를 이해하고 있기 보다는 그냥 남이 짠 코드를 가져다가 쓰는 수준이다.
