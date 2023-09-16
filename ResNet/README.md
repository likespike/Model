# Overview
- Revolution of Depth
  - Comparisons
    - AlexNet (2012) - 8 layers
    - VGG (2014) - 19 layers
    - ResNet (2016) - 152 layers
  - Depth is of crucial importance as deeper neetworks learn more powerful features
    - Larger receptive fields: Capturing semantic concepts with larger context
      - Depth가 커질수록 receptive field도 커짐
    - More non-linearites: Modeling more and richer feature space complicated
  - Known obstacles
    - Backward gradients that are easily vanished or exploded
    - Forward responses that are easily vanished or exploded
  - Enablers
    - ReLU activations
    - An appropriate initialization technique
    - Batch normalization
   
  # Batch Normalization
- Conv / FC -> output(x) -> Batch Normalization(normalization + scaling & shifting) -> Non-linearity(ReLU) -> Conv / FC -> ...
- The Reason Why Batch Normalization Works (주장1과 주장1에 대한 반박 주장2)
  - Internal covariate shift (주장1)
    -  내부 공변량 변화는 네트워크의 각 레이어에서 활성화 함수를 통과하는 입력 데이터 분포가 훈련 과정 동안 크게 변화할 때 발생함, 이 변화는 훈련 과정을 느리게 만들 수 있고, 더 나아가 수렴을 방해할 수 있음
    -  The distribution of each layer's inputs changes during training, as the parameters of the previous layers change
    -  Batch Normalization은 각 미니배치의 입력 데이터를 정규화하고 스케일링하는 방법을 사용하여 각 레이어의 활성화 함수를 안정화시키는데 도움을 줌
  - Batch normalization makes the optimization lanscapes significantly smoother (주장2)
    - optimization landscapes를 좀 더 부드럽게 만듦 -> 덜 민감하고, 빠르고, 안정적이게 함
- 효과
  - Normalizing each layer, for each mini-batch
  - Greatly accelerate training
  - Less sensitive to initialization
  - Improve regularization
 
# Deep residual learning
- 하지만 단순히 network initialization을 잘하고, batch normalization만 하면, 층을 잘 쌓을수록 무조건 성능이 좋은가? -> 그렇지 않음
- Skip Connection 추가 제안

# Basic Architecture Design
- Simple but just deep
  - Following the style of VGG
  - All 3x3 conv filters, except the first conv layer
  - Batch normalization after every conv layer
  - Periodically, double the number of filters and downsample spatially using stride 2
- Other remarks
  - No FC layer at the end besides the final classification layer
    - Using global average pooling after the last conv layer to feed dimensional features to the final classification layer regardless of the input size
  - No dropout
- Using deeper residual blocks with bottlenecks
  - 3x3 layer 2개 -> 1x1 + 3x3 + 1x3 3개의 layers로 중첨해서 하나의 residual bottlenecks block 만듦 (complexity 증가)

# Conclusion
- 이런 architecture design으로 인해 VGG보다 complexitys는 적고, 파라미터수도 적은데, 더 좋은 결과 내게 됨




