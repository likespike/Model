# 개요
- BatchNorm
  - batch 기반의 normalization 기법
  - classification 등 batch 간의 correlation 경우 등
  - 단점: batch size에 민감 (16, 8, 4 등) -> 학습이 unstble -> variations 나옴

- LayerNorm
  - 인풋 사이즈가 제한이 되어 있을 때, RNN같은 구조에서 효율적이어서 많이 쓰임 (시퀀셜 데이터)
  - 하나의 인스턴스에 대하여 channel 모두를 한 번에 normalize

- InstanceNorm
  - 배치 간의 correlation이 중요하지 않은 style transfer나 image matching 같은 경우에 효과적
  - 인스턴 하나에 대하여 채널 하나씩만 normalize
 
- GroupNorm
  - group을 input으로 받아준다는게 특징임
  - batch size가 작아질 때 batchnorm은 성능이 아주 떨어짐, groupnorm은 안정적인 성능 보임
  - channel을 group으로 나눠서 group별로 normalize
 
# 관련 논문
- Group Normalization, 2018
