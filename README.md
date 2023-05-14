# 한글의 초성, 중성, 종성 구조를 반영한 OCR 인식 모델 개발
  - Korean OCR (through consonant and vowel recognition)

## introduce
한글은 초성 19자, 중성 21자, 종성 28로 이루어져 만들수 있는 한 음절의 수가 11172자 입니다. \
한글은 사람들은 쉽게 배울수 있지만 컴퓨터가 인식하기에는 쉽지않습니다. \
이러한 복잡한 구조는 OCR모델에서 영어와 같은 한 음절이 한 글자인 언어와 달리 많은 학습 데이터를 필요로 한다. \
이를 해결하기 위해 한글의 초성, 중성, 종성을 구조를 반영하여 인식하는 방식으로 한글 OCR 모델을 개발하고자 합니다.

## Updates
2023-03-29 프로젝트 등록. \
2023-03-30 프로젝트 소개 수정. \
2023-05-13 프로젝트 이미지 수정. \
2023-05-14 기술스택 추가.

# Project
## 1. 데이터 소개 (Data)
![big_log_temp](https://user-images.githubusercontent.com/118142229/228453786-047157d1-0bd3-4780-9ab9-e8c9effdae19.png)
- ai-hub에서 제공되는 한국어 글자체 이미지(인쇄체 데이터)

#### 데이터 예시 (data example)
- 음절 데이터 (syllable data) \
![00000029](https://user-images.githubusercontent.com/118142229/228454358-8e655174-2923-413a-93e0-20c4e833a364.png)
![00000414](https://user-images.githubusercontent.com/118142229/228454722-0629abd7-3080-401b-a714-53095e3910ba.png) 

- 단어 데이터 (word data) \
![02234400](https://user-images.githubusercontent.com/118142229/228454940-5e1629a8-fa83-4e13-9402-11c079545bbf.png)
![02396110](https://user-images.githubusercontent.com/118142229/228455044-811412bd-55ac-406f-99f4-2576eaf429d8.png) 

## 2. 한글(객체) 감지 모델
- 학습 데이터 (1,400개)

![화면 캡처 2023-03-29 165458](https://user-images.githubusercontent.com/118142229/228465720-117f5776-092c-4539-b090-e664e1d7956e.png)

#### 1) 객체 감지 모델 선정
- YOLOv5, YOLOv8를 같은 데이터로 학습 후 이미지에서 한글(음절)을 예측결과 확인 
- YOLOv8로 선정

![화면 캡처 2023-03-29 162709](https://user-images.githubusercontent.com/118142229/228458871-727f694e-8cfb-4831-a870-c42fa2d38146.png)


#### 2) YOLOv8 모델 선정
- Average Precision의 평균값과 연산량의 성능이 가장 높은 YOLOv8x모델을 선정

![화면 캡처 2023-03-17 023308](https://user-images.githubusercontent.com/118142229/228459900-cf07fc19-29e8-475f-b4a0-b3fdc0389268.png)

#### 3) YOLOv8x 학습 결과 그래프
![화면 캡처 2023-03-29 164028](https://user-images.githubusercontent.com/118142229/228461650-f43dbfcc-2431-4183-b38b-7d4ff43a4285.png)

#### 4) YOLOv8x 감지 결과
![화면 캡처 2023-03-29 164354](https://user-images.githubusercontent.com/118142229/228463517-8870b1cb-5558-4eb6-9741-974ab4380754.png)

## 3. 한글 인식 모델
#### 1) 한글 인식 모델 선정
- Resnet, CNN, GRU 모델 비교
- 정확도가 가장 높은 ResNet 모델로 선정

![화면 캡처 2023-03-29 165523](https://user-images.githubusercontent.com/118142229/228465943-a2465fd3-911f-4608-834c-019d4c8b5e0d.png)

#### 2) 이미지 라벨링

![화면 캡처 2023-03-29 170026](https://user-images.githubusercontent.com/118142229/228469412-c9f64b0f-27c5-4c98-8f67-02993155778f.png)
![화면 캡처 2023-05-14 140510](https://github.com/rkdgg0/Korean-OCR/assets/118142229/c43bdf67-de95-47ba-ba28-b80e7567a281)

#### 3) ResNet 모델 학습
- 학습 데이터 (100,000개)

![화면 캡처 2023-05-14 140751](https://github.com/rkdgg0/Korean-OCR/assets/118142229/9666f8dc-5b28-4bfa-9e88-17c5e38bb6eb)

- 모델 훈련

![화면 캡처 2023-05-14 141311](https://github.com/rkdgg0/Korean-OCR/assets/118142229/562b913c-4a7a-47f1-9505-ce1a066a18a0)

## 4. 한글 OCR 결과

![화면 캡처 2023-05-14 142603](https://github.com/rkdgg0/Korean-OCR/assets/118142229/8070d119-f1b1-4ac1-8bb9-2abcb6f23bf2)

## 💾 기술스택
![화면 캡처 2023-05-14 150428](https://github.com/rkdgg0/Korean-OCR/assets/118142229/11e2bd21-7eea-49f0-a3b5-ed3636d32ac6)
