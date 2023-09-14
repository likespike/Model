# 개요
- 16 and 19 layers
- No local response normalization (LRN)
- Only 3x3 conv filters, 2x2 max-pooling and a few FC layers
- Using many 3x3 conv layers instead of a small number of larger conv filters (AlexNet이 처음 레이어에 11x11 conv filters를 쓴 것과 는 다름)
  - Keeping receptive field sizes large enough -> more effective
  - Deeper with more non-linearities
  - Fewer parameters
  - 보통 3x3이 gpu나 hardware 최적화하기에 좋은 연산
