# 개요
- 11, 13, 16 and 19 layers
- No local response normalization (LRN)
- Only 3x3 conv filters, 2x2 max-pooling and a few FC layers
- Using many 3x3 conv layers instead of a small number of larger conv
  -  AlexNet은 11x11 conv layers, InceptionNet은 5x5 conv layers
  -  small conv layes 사용 이유
    - Keeping receptive field sizes large enough -> more effective (더 잘 분류해 냄, 성능up)
    - Deeper with more non-linearities
      - activation을 많이 통과시킬수록 decision boundary를 더 많이 만들어 성능 좋음, depth 깊게 가능
      - Alexnet 대비 2배 이상 깊은 네트워크
    - Fewer parameters
      - 7 x 7 = 49 parameters
      - 3 x 3 * 3번 = 27 parameters
    - 보통 3x3이 gpu나 hardware 최적화하기에 좋은 연산
- Betch Size: 256
- L2 Regularization
- Momentum: 0.9
- 단점: 마지막 FC Layers에 몰려있는 많은 Params
  - 총 138M param중에 120M 정도가 3개의 FC Layers에 몰려 있음

# 관련 논문
- VERY DEEP CONVOLUTIONAL NETWORKS FOR LARGE-SCALE IMAGE RECOGNITION (2015)

# 참고 자료
- https://www.youtube.com/watch?v=bweAXJgZGyE
