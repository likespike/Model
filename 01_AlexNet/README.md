# 개요
## Overall architecture
- 8 layers
  - 5 convolutional layers with a combination of max-pooling layers
  - 3 fully connected layers
- Softmax
  - The activation function used in the output layer is Softmax
- 650K neurons, 62.3 millions parameters 
- 딥러닝의 시대를 열었음
- ReLUs
  - Using better activation function
  - Tanh, Sigmoid -> ReLUs (최대 6배 정도 빠른 실험 결과)
- GPU 2대 병렬 사용
- Normalization
  - LRN(Local Response Normalization)
  - batch normalization의 시초 정도
  - 강한 뉴런의 활성화가 근처 다른 뉴런의 활동을 억제 시키는 현상에서 영감 -> 특정 값에 의해 과대적합 되는 것을 방지
- overlapping pooling
  - Traditional pooling은 kernel과 stride의 크기가 같았음 -> Pooling window의 크기를 stride보다 더 크게 함
    - ex> kernel=3x3, stride=1
  - overfitting 줄이고, error rates도 낮추는 효과
- data augmentation (Reducing Overfitting1)
  - Image Translation 
    - 256x256이미지를 랜덤으로 잘라 224x224-> 좌우 32픽셀씩 32x32=1024에 horizontal reflection으로 1024x2 = 2048배 증가
    - test set에 대해서는 4개의 코너와 센터 5개의 패치에만 horizontal reflection을 적용하여 총 10개의 224x224 patch생성
    - 10개의 patch의 softmax 결과 값을 평균 내 사용
  - jittering
    - RGB 값에 PCA를 통해 찾은 중요성분들만큼 랜덤하게 더해줌
    - 전체 이미지의 R,G,B 공분산에서 고유벡터, 고유값을 구함
    - 특정 공시겡 따라 값을 모든 픽셀에 더해줌
- dropout (Reducing Overfitting2)
  - regularization techinique
  - It used two Dropout layers
  - 0.5의 확률로 hidden neiron의 값을 0으로 바꿔줌
  - Droupout된 hidden neuron은 forward, backpropagation 시 영향을 끼치지 않음
  - 뉴런들 사이의 의존성을 눚추고, co-adaption을 피할 수 있음
  - 3개의 Fully-connected layer 중 앞의 2개에만 적용
  - Test시 droupout 적용x, 대신 0.5를 곱해줌
- Trained with a larger amount of data (ImageNet)
  - 1,000 classes
  - ILSVRC-2010 datasets with labeled
  - trainset: 1,200,000, validation set: 50,000, test set: 150,000
  - 256x256x3 (RGB)
    - 길이가 짧은 쪽에 맞춰 256으로 rescale 후 center-crop함
 - Cong-Pool-LRN-Conv-Pool_LRN-Conv-Conv-Conv-Pool-(AdaptiveAvgPool)-FC-FC-FC

 
# Alexnet(ILSVRC-2012) - Imagenet Large Scale Visual Recognition Challenge
![alexnet_01](https://github.com/likespike/Models_and_Papers/assets/117564349/b8c674a9-0e72-4ff1-a68b-a42b19fe8a80)
<img width="320" alt="alexnet_02" src="https://github.com/likespike/Models_and_Papers/assets/117564349/bab264be-35cd-4916-a875-993190bad05b">


# 관련 논문
- Image Net Classification with Deep Convolutional Neural Networks (2012)
- One weird trick for parallelizing convolutional neural networks (2014)
