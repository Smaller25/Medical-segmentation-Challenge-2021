# Medical-segmentation-Challenge-2021
https://maic.or.kr/competitions/8/infomation 
--------
## 1. Challenge Image
![image](https://user-images.githubusercontent.com/77380467/148221025-6674aaf1-d382-4c1b-95e5-a4456c31a18b.png)


## 2. Challenge Description
흔히 접할 수 없는 데이터(소아 병리영상)을 제공하여 직접 분석에 활용해볼 수 있는 대회.

선천성 거대결장이라고도 불리는 허슈스프렁병(HIrschsprung disease)은 발생 중 장의 신경세포(신경절 세포) 중 일부 또는 전부가 제대로 발달하지 못하거나 장으로 이주하지 못해 장신경병증(enteric neuropathy)에 의해 발생한다. 장의 운동이 멈추게 되고, 그에 따라 변의 진행이 안 되어 장이 대변으로 막혀 신생아나 어린이가 만성변비 및 복부 팽만으로 인한 통증에 시달리게 된다고 한다.(정상적인 배변을 할 수 없음) 

이번 대회는 장의 근육층 사이에 있는 장신경절(enteric nerve ganglia)을 찾아내기 위해 다양한 Image Segmentation 모델 및 기법들을 통해 AI model을 개발하는 것을 목표로 진행되었다.

## 3. 진행 사항
### 1) 기간 
: 예선) 21/10/18 ~ 21/11/07
: 본선) 21/11/10 ~ 21/11/23

### 2) 최종 순위
: 예선 4위 / 본선 7위
![image](https://user-images.githubusercontent.com/77380467/148221789-26491f76-46b4-4fa1-8178-ec7ca5a9e09a.png)
![image](https://user-images.githubusercontent.com/77380467/148221925-5ff6e01a-d0a1-4774-8ba5-5b23d6f82d1a.png)

### 3) 결과 
![image](https://user-images.githubusercontent.com/77380467/148221995-ac84a83d-0dc4-4d45-870f-ee1c19ed0469.png)
-------
![image](https://user-images.githubusercontent.com/77380467/148222022-83409842-2a7f-4e5f-bd93-ca4c084b8540.png)


## 4. Applied Tech & Issues
### 1) patch 단위의 segmentation
- Ignore background(조직이 없는 부분) 
- 'layer' structure
이 두 가지 이유로 하나의 이미지셋을 index-maintained patch로 자르고, 하얀색 전경을 thresholding으로 제거하는 방식 선택

### 2) Main Model : U-net / Attention U-net 
U-net은 biomedical image segmenation에서 상당히 좋은 성능을 보여줬던 모델 알고리즘으로, encoding 부분과 decoding 부분의 점진적인 downsampling & upsampling 구조를 가지고 있다. (O. Ronneberger, 2015)
이 이후로도 여러가지 발전된 버전들이 나오기 시작했는데, (Unet+, Unet++, Efficient U-net, Attention U-net etc.), 본 프로젝트에서는 Biomedical Image challenge의 특성 상 U-net을 기반으로 시작하여 여러 버전의 발전된 U-net 모델 알고리즘을 파이프라인에 추가하는 방식을 택했다. 

### 3) pretrained U-net
당연하게도 첫 시도에선 점수가 좋지 않았다.
performance 향상을 위해 집중한 부분은 두 가지였는데, pretrained model & 다양한 모델 알고리즘 적용 / loss function 변화 였다. pretrained model은 훨씬 좋았음.

### 4) Loss function : combined [BinaryCrossentropy +Dice coefficient] : custom function

### 5) model pipeline structure (trial)
- 1 track : layer 3 & layer 5 (no weight)
- 1 track : layer 3 & layer 5 (layer 5_weighted method)
- 2 track : layer 3 model + layer 5 model (sequential model training / shared pretrained parameters)


## 5. Reference 
https://github.com/yingkaisha/keras-unet-collection/tree/main/keras_unet_collection
https://arxiv.org/pdf/1505.04597.pdf)%e5%92%8c%5bTiramisu%5d(https://arxiv.org/abs/1611.09326.pdf
https://arxiv.org/abs/1804.03999
https://arxiv.org/abs/2102.03111

now adding...
