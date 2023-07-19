# AIFFEL Campus Online 5th Code Peer Review
- 코더 : 김석영
- 리뷰어 : 황인준


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 네 pix2pix:GAN을 generator와 discriminator를 잘 구현해서 사진을 얻었습니다. 
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네 변수들에 대한 설명이나 output의 특징에 대해 설명했습니다.
  ```python
  class DiscBlock(layers.Layer):
    # __init__() 에서 필요한 만큼 많은 설정을 가능하게 함 
    # 필터의 수(n_filters)
    # 필터가 순회하는 간격(stride)
    # 출력 feature map의 크기를 조절할 수 있도록 하는 패딩 설정(custom_pad)
    # BatchNorm의 사용 여부(use_bn)
    # 활성화 함수 사용 여부(act)
    def __init__(self, n_filters, stride=2, custom_pad=False, use_bn=True, act=True):
        super(DiscBlock, self).__init__()
        self.custom_pad = custom_pad
        self.use_bn = use_bn
        self.act = act
        
        if custom_pad:
            self.padding = layers.ZeroPadding2D() # 1. width 및 height의 양쪽 면에 각각 1씩 패딩되어 총 2만큼 크기가 늘어남
            self.conv = layers.Conv2D(n_filters, 4, stride, "valid", use_bias=False)
        else:
            self.conv = layers.Conv2D(n_filters, 4, stride, "same", use_bias=False)
            # 2. 패딩하지 않고 필터 크기 4 및 간격(stride) 1의 convolution 레이어를 통과하면 width 및 height 가 3씩 줄어듬 (OutSize=(InSize+2∗PadSize−FilterSize)/Stride+1), 채널 수는 사용한 필터 개수와 같음
        
        # 3. 다른 레이어(BatchNorm, LeakyReLU)는 출력의 크기에 영향을 주지 않음
        self.batchnorm = layers.BatchNormalization() if use_bn else None
        self.lrelu = layers.LeakyReLU(0.2) if act else None
    ```
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 에러없이 정상적으로 작동했습니다.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 정상적으로 코드가 작동됐고, 주석도 올바르게 하셨기때문에 제대로 이해하고 작성하신것 같습니다.
- [O] 코드가 간결한가요?
  > 간결하고 가독성이 좋습니다.

# 참고 링크 및 코드 개선
> epoch를 1회 하고 생성된 이미지를 보면 격자무늬가 생성되는데, 더 많이 에포크를 돌리면 이 현상이 더 심해지는 것 같았습니다. 100회epoch를 학습하던 중에 제출 하셨는데, 아마 체크무늬가 더 많이 생길수도 있습니다. l1 loss 가중치 람다를 다른 것으로 바꿔 볼수도 있고, augmentation을 바꿔가면서도 해볼 수 있을것 같습니다. 
