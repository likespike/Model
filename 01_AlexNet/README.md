# 개요
- ILSVRC'12 (Imagenet Large Scale Visual Recognition Challenge)
- 8 layers
  - 5 convolutional layers with a combination of max-pooling layers
  - 3 fully connected layers
- 650K neurons, 62.3 millions parameters 
- Trained with a larger amount of data (ImageNet)
- Using better activation function (RELU) and regularization techinique (droupout)
  - It used two Dropout layers
- The activation function used in the output layer is Softmax
- Overall architecture
  - Cong-Pool-LRN-Conv-Pool_LRN-Conv-Conv-Conv-Pool-(AdaptiveAvgPool)-FC-FC-FC
    - LRN(Local Response Normalization): batch normalization의 시초 정도

# 성과
![alexnet_01](https://github.com/likespike/Models_and_Papers/assets/117564349/b8c674a9-0e72-4ff1-a68b-a42b19fe8a80)
<img width="320" alt="alexnet_02" src="https://github.com/likespike/Models_and_Papers/assets/117564349/bab264be-35cd-4916-a875-993190bad05b">



# 관련 논문
- Image Net Classification with Deep Convolutional Neural Networks (2012)
- One weird trick for parallelizing convolutional neural networks (2014)
