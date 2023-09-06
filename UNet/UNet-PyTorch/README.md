# 출처
https://github.com/hayashimasa/UNet-PyTorch

# 사용법 (colab)
- colab에서 custom library를 import하는 방법은 두 가지임
  - git clone하여 해당 파일, 폴더들을 /content인 root directory로 이동 후 import
  - or ipynb파일이 있는 경로에 git clone -> 해당 디렉터리로 cd명령어로 이동 후 import
- Models 저장소에 하위 폴더로 model들이 있기 때문에 하위 폴더만 clone해야 하는데, 관련 코드는 ipynb파일에 포함돼 있음


# 개론
- Approaches for Semantic Segmentation
- Early Approaches
  - Object propasal: Mask localization + Mask classification
- More Recent Approaches
  - End-to-end CNN architectures
    - segmentation mask를 output label로 주고 input에는 image만 넣어서 맞추도록 네트워크 구성0
    - Categorized roughly into two classes
        - Fully Convolutional Networks (FCNs)
            - FCN
            - DeepLab
        - Convolutional Encoder-Decoders
            - U-Net
            - Deconvolution network

- Basic End-to-End Architectures
  - FCN
  - DeepLab
  - Deconvolution Network
  - U-Net: Convolutional networks for biomedical image segmentation., Ronneberger et al., MICCAI 2015

# U-Net
  - MICCAI 논문에 기재 (2015)
  - challenge에서도 우수한 성적을 거둠
  - segmentation task에서 유명함


# Midical images의 두 가지 문제
- medical image의 특징이 보통 very few annotated images (approx. 30 per application)
- Touching objects of the same class
    - 세포벽을 사이에 두고 붙어 있는 같은 클래스의 세포들
    - instance segmentation과도 다름, 세포1, 세포2 등의 인덱스 구분이 아님
    - 각 세포들을 인덱스 구분이 아닌 클래스로만 구분하게 됨 -> label이 어려움
    - label의 어려움이 instance segmentation을 하지 않는 이유로 판단됨


# Issues on End-to-End Architecture
- Semantic segmentation = Pixel-level classification
- Trade-off between the resolution and the semantic level of prediction
  - resolution을 작게 가져갈수록 더 많은 receptive field를 갖게 됨 -> 더 큰 semantic을 보게 됨
  - 그러나 resolution이 작으면 지역적인 것을 보기 어려움
  - high level의 정보기 너무 커질수록 segmentation이 부정확해질 수 있고, 지역 정보만 봐서도 안됨
- How to achieve both of them at the same time?

# U-Net Architetcture
- 네트워크 모양이 U자로 생김
- input output 영상의 resolution이 거의 비슷함
- High, Low Level 정보를 함께 보존하면서 학습 및 최종 output 가능
- 영상의 바깥 부분 padding을 시행하지 않음 (메디컬 영상 특성상 영상이 너무 적어, zero padding으로 생기는 bais들을 처리하기가 쉽지 않은 것 같음)
    - 인풋 영상에만 mirroring을 이용한 paddig을 통해서 입력 영상의 가장자리 부분도 prediction할 수 있도록 만듦 (feature에 대한 reflection 등은 하지 않음)
- 먼저 3x3 convolution + ReLU에서 imgage의 resolution을 줄여가며 연산을 수행하고 -> 다시 2x2 up-convolution에서 resolution을 두 배씩 키워 가면서 연산을 수행함(Deconvolution, Upsampling) -> 그리고 resolution이 같은 피처끼리 concat시킴
- 왼쪽: contracting path (축소), down-sample
    - 먼저 일반적인 CNN과 같이 인풋 영상 이미지의 resolution을 줄여가면서 convolution을 수행함
        - 장점1: 줄여가면서 Receptive Field를 키우고, High Level 정보를 convolution 연산이 학습 하도록 하기 위함
        - 장점2: 실제 컨볼루션 연산에 필요한 오퍼레이션 숫자가 적어지는 장점 (계산의 효율성)
- 오른쪽: expanding path (확장), up-sample
- feature map의 사이즈가 점점 작아졌다가 -> 점점 커진다
- 단순히 feature map size가 줄어 들었다가 커지는 (압축, 인코딩 -> 복원, 디코딩) 개념으로 보이지만, channel size를 보면 정보를 압축하면서 손실된다고 보기 보다는, 정보를 다른 형태로 추출한다고 해석하는게 좀 더 맞는 해석임
- skip connection
    - contracting path와 expanding path를 channel 방향으로 concatnate
    - encoder에서 만들어진 feature가 decoder를 통과할 때 합침 (channel size가 두 배 커짐)
    - Res down sampling과 up sampling 과정을 다 거친 값(U-Net이 의도한 변형, 추출된 정보)과 원래의 값(기존 정보) 둘 다를 활용한다
    - High level과 Low level 정보를 함께 보존하면서 최종 output을 출력, 학습함
    - output size(388 x 388): padding되지 않은 output에 대해서만 output map을 구하는 것임


# Medical image sementation을 위한 제안들
-
- Augment Training Data using Deformations
    - 기본적인 augmentation과 더불어 deformal augmentation도 사용
    - grid를 설정 후, grid의 위치를 random하게 섞어 가면서 영상에 distortion을 줌 (bio image에 잘 어울리는 증식)
- Ensure Separation of Touching Objects
    - Segmentation of Touching Objects of the Same Class 문제를 해결하기 위해 제시
    - edge를 강조하도록 weight mask 생성 방법을 제안
        - object와 object 사이만 높은 값을 같도록(경계)


# 실제 competition에서의 성과
- challenge 실제 데이터셋의 challenge 문제들
    - structures with very low contrast
    - other cell compartments
    - fuzzy membranes
- 이러한 난제를 극복하고 좋은 성과를 냄
- Warping Error로 평가

