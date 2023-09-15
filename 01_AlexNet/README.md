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

# 관련 논문
- Image Net Classification with Deep Convolutional Neural Networks (2012)
- One weird trick for parallelizing convolutional neural networks (2014)
