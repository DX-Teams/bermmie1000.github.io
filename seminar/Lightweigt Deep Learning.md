---
sort: 8
---

# 모델 경량화 (MobileNet)

*'20년도 초고압 GIS/Tr. 진단 모델 개발 시 적용한 모델 경량화 기법인 MobileNet에 대한 설명입니다.*



  수백 개의 디바이스가 연결된 실시간 모니터링 시스템에서 초고압 GIS/Tr. 제품을 타겟으로 하는 진단 모델을 만드는 중 삽질했던 경험담입니다.😱

  실시간 진단을 해야하는 만큼 진단 모델이 메모리에 상주해야 하며, 제품마다 다른 모델을 사용하기 때문에 모델 하나의 크기를 최대한 줄이는 작업을 해야 했습니다. 실시간으로 빠른 추론 결과를 얻기 위해서라도 모델 경량화는 필수였습니다. 모델 크기를 줄이는 가장 쉬운 방법은 `1. 레이어 수 줄이기`, `2. Weight size 줄이기` 이었습니다. 개발 중 사용한 데이터는 한 모델 당 약 500장 미만입니다. 이미지 분류 모델을 학습하기에는 턱없이 부족한 수 입니다. 하지만 데이터가 적은 덕분에 1, 2번 방법을 통해 모델을 작게 만들어도 오히려 성능이 좋아지는 효과를 얻을 수 있었습니다. 작은 모델이기에 적은 데이터로 충분히 학습 시킬 수 있었기 때문이죠! 

  그러나 실제 제품에 넣기에는 아직도 무거운 모델이었습니다. 기본적인 CNN 구조에서 레이어 튜닝을 통해 모델을 최대한 작게 만든 후 이보다 더 작게 만들기 위해서는 `3. 경량화 기법`을 적용할 수 밖에 없었습니다. 이를 위해 **모바일 환경에서 CNN을 사용할 수 있도록 나온 경량화 기법인 `MobileNet` 기법을 사용**했습니다. 



## 목차

- [모델 경량화 (MobileNet)](#모델-경량화-mobilenet)
  - [목차](#목차)
  - [1. 배경](#1-배경)
    - [부분방전 이란](#부분방전-이란)
    - [부분방전 진단](#부분방전-진단)
  - [2. 기존 모델 구조](#2-기존-모델-구조)
    - [성능 및 크기](#성능-및-크기)
  - [3. 경량화 방법](#3-경량화-방법)
    - [3.1. 네트워크 경량화의 종류](#31-네트워크-경량화의-종류)
      - [왜 MobileNet?](#왜-mobilenet)
    - [3.2. MobileNet](#32-mobilenet)
      - [3.2.1. MobileNet V1](#321-mobilenet-v1)
      - [3.2.2. MobileNet V2](#322-mobilenet-v2)
    - [3.3. 경량화 모델](#33-경량화-모델)
    - [성능 및 크기](#성능-및-크기-1)



## 1. 배경

### 부분방전 이란

   `부분방전`(Partial Discharge: PD)이란 부분적으로 일어나는 방전 현상이다. 절연체에 이상이 생겨 고전압이 적용되었을 때 부분적으로 절연체와 전도체 사이가 전기적으로 이어지는 현상을 말한다. 보통 부분방전 현상은 전기적 스트레스의 집중으로 인해 발생한다. 절연체의 수명을 단축 시키며, 이를 통해 **절연체의 절연열화나 절연파괴를 조기에 측정**할 수 있다. 



> ❗️**전력기기의 절연체 상태를 진단할 수 있는 중요한 지표**



### 부분방전 진단

  부분방전의 원인은 내부 기공이나 외부 돌기 등 다양한 절연체 이상이다. LS에서는 제품별로 5~7개의 결함 원인을 구분하고 있으며, PD센서를 통해 얻은 이미지를 분석하여 결함의 원인을 진단한다. 

*예) 초고압 GIS의 부분방전 원인 (6가지)*![PD](..\\assets\\images\\mobilenet\\PD.png)



## 2. 기존 모델 구조

500장 미만의 적은 데이터로 5~7개 class를 분류하는 모델은 크기가 클 경우 자칫 학습이 충분히 이뤄지지 않아 성능이 낮을 수 있다. 단순한 모델을 충분히 학습하기 위해 가장 기본적인 CNN 모델인 LeNet-5의 구조를 이용하여 이미지 분류 모델을 구현하였다. 

* LeNet 구조![LeNet](..\\assets\\images\\mobilenet\\LeNet.jpeg)

* PD 진단 모델 구조

```python
class PDModel(nn.Module):
    def __init__(self, classes):
        super(PDModel, self).__init__()

        self.classes = classes

        self.conv = nn.Sequential(
            nn.Conv2d(1, 32, 3, padding=1),  # W: 120 -> 60, H: 60 -> 30
            nn.ReLU(),
            nn.MaxPool2d(2),
            nn.Conv2d(32, 64, 3, padding=1),  # W: 60 -> 30, H: 30 -> 15
            nn.ReLU(),
            nn.MaxPool2d(2),
            nn.Conv2d(64, 128, 3, padding=1),  # W: 30 -> 15, H: 15 -> 7
            nn.ReLU(),
            nn.MaxPool2d(2),
            nn.Conv2d(128, 256, 3, padding=1),  # W: 15 -> 7, H: 7 -> 3
            nn.ReLU(),
            nn.MaxPool2d(2),
        )
        self.dense = nn.Sequential(
            nn.Linear(5376, 64),
            nn.ReLU(),
            nn.Linear(64, 32),
            nn.Dropout(),
            nn.ReLU(),
            nn.Linear(32, len(self.classes)),
            nn.Sigmoid()
        )

    def forward(self, x):
        x = self.conv(x)

        x = x.view(-1, 256 * 3 * 7)

        x = self.dense(x)

        return x
```

### 성능 및 크기

Epoch 80, Batch size 64 기준

* 정확도 : 98.824%
* 모델 크기 : 5.54MB



## 3. 경량화 방법

### 3.1. 네트워크 경량화의 종류

**네트워크의 `정확도`를 높게 유지하며 `연산속도`를 올리거나 `크기`를 줄이는 것**

참고: https://www.youtube.com/watch?v=BhS4EofeY8E&feature=youtu.be
git  : https://github.com/j-marple-dev/model_compression

* **Efficient Architecture Design : 효율이 높은 아키텍쳐 설계**
* Network Pruning : 중요도가 낮은 파라미터 제거
* Network Quantization : 파라미터를 좀 더 작은 크기의 타입으로 표현
* Knowledge Distillation : 학습된 큰 네트워크를 작은 네트워크 학습에 사용
* Network Compile : 바이너리 형태로 네트워크를 변화
* Matrix Decomposition : 네트워크의 행렬 연산을 더 작은 행렬 연산으로 변환
* ...



#### 왜 MobileNet?

✔️ 이해하기 쉬운가?  
     : 빠른 시간 안에 구현할 수 있어야 한다.  
    ⇨ **익숙한 Convolution 레이어에서 계산 방법만 달라지는 것이다.**  

✔️ 기존 모델의 구조를 최대한 유지할 수 있는가?  
     : Java로 구현한 레이어의 수정을 최소화 해야 한다.  
    ⇨ **Convolution 레이어와 레이어를 연결하는 부분만 수정하면 된다.**

✔️ 실제 파라미터의 수를 줄일 수 있는가?  
      : 메모리에 로드한 모델의 사이즈가 작아야 한다. 모니터링 시스템 내에는 수많은 어플리케이션들이 함께 실행된다.  
        전체적인 성능을 위해서라도 모델의 사이즈를 작게 만들어야 한다.  
    ⇨ **연산 속도와 실제 파라미터 수를 획기적으로 줄일 수 있다.**



### 3.2. MobileNet

  모바일이나 임베디드 환경 등 컴퓨터 성능이 제한되거나 배터리 퍼포먼스가 중요한 곳에서 사용될 목적으로 설계된 CNN구조이다. `Depthwise Separable Convolution` 구조를 이용한 **MobileNet V1**과 여기에 ResNet의 `Residual 구조`를 더하여 파라미터 수와 연산량을 더욱 줄인 **Mobile V2**가 있다. 

#### 3.2.1. MobileNet V1

*MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Application (2017) (https://arxiv.org/pdf/1704.04861.pdf)*



  Mobile V1의 핵심은 `Depthwise Separable Convolution` 이다. Depthwise Separable Convolution이란 Depthwise convolution과 pointwise convolution의 결합이다. 채널내 연산과 채널간 연산이라고 생각하면 된다. Depthwise convolution은 입력 이미지의 채널 각각에 공통된 1-channel 필터를 사용하여 연산한다. 그 결과, 입력 채널 수와 출력 채널 수가 동일하다. Pointwise convolution은 depthwise convolution의 출력에 대해 각 point마다 채널끼리 연산한다. 이미지의 크기(WxH)는 동일하나 출력의 채널 수를 조절할 때 사용된다. 

![DepthwiseSeparableConvolution](..\\assets\\images\\mobilenet\\DepthwiseSeparableConvolution.png)



* Depthwise Convolution

  ![DepthwiseConvolution](..\\assets\\images\\mobilenet\\DepthwiseConvolution.png)

  * 입력 이미지의 각 채널마다 spatial feature를 추출하기 위한 방법
  * 각 채널마다 필터가 존재함 (커널 크기 : [출력 채널 수, 1, 필터 높이, 필터 가로])
  * 입력과 출력의 채널 수가 동일함
  * Grouped convolution에서 그룹 수를 입력 채널 수만큼 늘린 것과 동일함  
: 입력 채널을 여러개의 그룹으로 나눈 후 공통된 가중치를 가지고 각각 convolution을 수행하는 방식 (입력 채널을 묶음으로 나누어 훈련시키는 것) (커널크기=[출력채널수, 입력채널수/그룹수, 높이, 폭])

  ![GroupedConvolution](..\\assets\\images\\mobilenet\\GroupedConvolution.png)

  * 일반적인 Convolution Layer과 비교
    * 총 weight 파라미터 수 : $`K^2 C_i C_o → K^2 C_i`$
    * 총 연산량 : $`K^2 C_i C_o H W → K^2 C_i H W`$

    

* Pointwise Convolution (1X1 Convolution)  
  
  ![PointwiseConvolution](..\\assets\\images\\mobilenet\\PointwiseConvolution.png)

  * 1X1 고정된 크기의 커널(필터)를 사용함
  
  * Channel에 대한 연산만 수행하여 출력 채널 수를 조절함
  
  * Dimensional reduction을 위해 많이 사용하며 추후 연산량을 감소시킴

  * 파라미터 수와 연산량
  
    * 총 weight 파라미터 수 : $`C_i C_o`$
    * 총 연산량 : $`C_i C_o H W`$
  
    
  
* **Depthwise Separable Convolution**  
  
  * Depthwise + Pointwise → Channel과 Spatial한 특징을 분리하여 바라봄
  * 파라미터 수와 연산량
    * 총 weight 파라미터 수 :  $`C_i (K^2 + C_o)`$
    * 총 연산량 : $`C_i H W (K^2 + C_o)`$




#### 3.2.2. MobileNet V2

CNN의 분류 부분인 Linear 레이어(Fully connected layer)는 모델 크기에 가장 많은 영향을 끼치는 부분이다. 이전 Convolution 결과를 모두 1차원으로 펼쳐 연산해야 하기 때문이다. MobileNet V2에서는 Linear 레이어를 가장 마지막에 한 레이어만 사용하며 Linear 레이어의 입력을 Convolution 연산을 통해 최소화 한다. 이 때, 분류 성능을 유지하기 위해 ResNet에서 사용하는 residual 구조를 이용한 Inverted residual block 구조를 사용한다. Block 안에서 채널 수를 줄이는 일반적인 Residual block과 반대로 Inverted residual block은 block 내에서 채널 수를 늘려 연산한다.

![InvertedResidualBlock](..\\assets\\images\\mobilenet\\InvertedResidualBlock.png)

* 일반적인 Reidual Blck
  
  * Wide → Narrow(Bottleneck) → Wide
  * Skip connection을 통해 기존에 학습한 정보를 보존하고, 거기에 추가적으로 학습함
    
* Inverted Residual Block
  * 저차원의 데이터를 확장시키고 separable convolution을 통해 많은 데이터를 보존할 수 있도록 설계됨
  * 마지막 projection 레이어는 저차원 데이터를 출력하기 때문에 activation function을 사용하지 않음 (사용 시 유용한 정보가 손실되므로)

  

### 3.3. 경량화 모델

* Convolution Block

  ```python
  def conv(input_channels, output_channels, stride):
      """일반적인 Conv 레이어
  
      Args:
          input_channels: 입력 채널 수
          output_channels: 출력 채널 수
          stride: stride
  
      Return:
          Conv-BatchNorm-LeakyReLU
  
      """
      return nn.Sequential(
          nn.Conv2d(input_channels, output_channels, 3, stride, 1, bias=False),
          nn.BatchNorm2d(output_channels),
          nn.LeakyReLU(0.2, inplace=True),
      )
  ```
  
  * k=3(kernel size)인 Convolution block
  * Normalization을 위한 BatchNorm 레이어 추가
  * LeakyReLU는 성능을 위해 ReLU6로 대체 가능(논문에서는 ReLU6사용)
  
* Inverted Residual Block (Bottleneck)

  ```python
  class InvertedResidualBlock(nn.Module):
      """Inverted Residual Block 클래스"""
      def __init__(self, input_channels, output_channels, stride, expansion_factor):
          super(InvertedResidualBlock, self).__init__()
  
          self.stride = stride
          self.residual_connect = self.stride == 1 and input_channels == output_channels
  
          hidden_dim = int(input_channels * expansion_factor)
  
          if expansion_factor == 1:
              self.conv = nn.Sequential(
                  # dw
                  nn.Conv2d(hidden_dim, hidden_dim, 3, stride, 1, groups=hidden_dim, bias=False),
                  nn.BatchNorm2d(hidden_dim),
                  nn.LeakyReLU(0.2, inplace=True),
                  # pw
                  nn.Conv2d(hidden_dim, output_channels, 1, 1, 0, bias=False),
                  nn.BatchNorm2d(output_channels),
              )
          else:
              self.conv = nn.Sequential(
                  # pw
                  nn.Conv2d(input_channels, hidden_dim, 1, 1, 0, bias=False),
                  nn.BatchNorm2d(hidden_dim),
                  nn.LeakyReLU(0.2, inplace=True),
                  # dw
                  nn.Conv2d(hidden_dim, hidden_dim, 3, stride, 1, groups=hidden_dim, bias=False),
                  nn.BatchNorm2d(hidden_dim),
                  nn.LeakyReLU(0.2, inplace=True),
                  # pw
                  nn.Conv2d(hidden_dim, output_channels, 1, 1, 0, bias=False),
                  nn.BatchNorm2d(output_channels),
              )
  
      def forward(self, x):
          if self.residual_connect:
              return x + self.conv(x)
          else:
              return self.conv(x)
  ```

  * Expansion factor에 따라 저차원 입력 데이터의 채널을 확장 후 학습
  * expansion_factor = 1인 경우, Separable convolution block 수행

* 1x1 Convolution Block (Pointwise Convolution Block)

  ```python
  def conv1x1(input_channels, output_channels):
      """1x1 Conv 레이어
  
      Args:
          input_channels: 입력 채널 수
          output_channels: 출력 채널 수
  
      Return:
          1x1 Conv-BatchNorm-LeakyReLU
      """
      return nn.Sequential(
          nn.Conv2d(input_channels, output_channels, 1, 1, 0, bias=False),
          nn.BatchNorm2d(output_channels),
          nn.LeakyReLU(0.2, inplace=True),
      )
  ```

  * k=1인 Convolution block
  * Output channel 수를 조절하기 위해 사용  

  
* Main Model

  ```python
  class PDLightModel(nn.Module):
      """PD 모델 경량화 버전(MobileNet Ver.2 적용)"""
      def __init__(self, classes):
          super(PDLightModel, self).__init__()
  
          self.classes = classes
  
          self.layers = [
              # conv 3x3
              conv(1, 32, 2),
              # n = 1
              InvertedResidualBlock(32, 16, 1, 1),
              # n = 2
              InvertedResidualBlock(16, 24, 2, 6),
              InvertedResidualBlock(24, 24, 1, 6),
              # n = 3
              InvertedResidualBlock(24, 32, 2, 6),
              InvertedResidualBlock(32, 32, 1, 6),
              InvertedResidualBlock(32, 32, 1, 6),
              # n = 3
              InvertedResidualBlock(32, 64, 2, 6),
              InvertedResidualBlock(64, 64, 1, 6),
              InvertedResidualBlock(64, 64, 1, 6),
              # conv 1x1
              conv1x1(64, 256)
          ]
          # Feature Extractor
          self.extractor = nn.Sequential(*self.layers)
          self.classifier = nn.Sequential(
              nn.Linear(256, len(self.classes)),
              nn.Softmax()
          )
  
      def forward(self, x):
          x = self.extractor(x)
          x = x.mean(3).mean(2)
          x = self.classifier(x)
          return x
  ```

  * 네트워크 구조

    |    Input     |  Operator   | expand_ratio | output_channels | stride |
    | :----------: | :---------: | :----------: | :-------------: | :----: |
    | 1 x 60 x 120 |    conv     |      -       |       32        |   2    |
    | 32 x 30x 60  | bottleneck  |      1       |       16        |   1    |
    | 16 x 30 x 60 | bottleneck  |      6       |       24        |   2    |
    | 24 x 15 x 30 | bottleneck  |      6       |       24        |   1    |
    | 24 x 15 x 30 | bottleneck  |      6       |       32        |   2    |
    | 32 x 7 x 15  | bottleneck  |      6       |       32        |   1    |
    | 32 x 7 x 15  | bottleneck  |      6       |       32        |   1    |
    | 32 x 7 x 15  | bottleneck  |      6       |       64        |   2    |
    |  61 x 3 x 7  | bottleneck  |      6       |       64        |   1    |
    |  64 x 3 x 7  | bottleneck  |      6       |       64        |   1    |
    |  64 x 3 x 7  |  conv 1x1   |      -       |       256       |   1    |
    | 256 x 3 x 7  | avgpool 3x7 |      -       |        1        |   1    |
    |     256      |   linear    |      -       |  len(classes)   |   -    |
    | len(classes) |   softmax   |      -       |  len(classes)   |   -    |

  * 분류기에 Linear layer(Fully connected layer) 1개 + Softmax 함수만 사용  
  * Linear layer 전에 Average pooling layer를 배치함으로써 입력 데이터의 크기를 줄임

  

### 성능 및 크기

Epochs : 36 (learning rate=0.0001) + 17(lr=0.00001)
Batch size : 4

* **정확도 : 92.77% (6% 감소)** (단, 경량화 모델 튜닝 시 성능 향상 가능)
* **모델 크기(파일 크기) : 1.62MB (기존 크기의 29.2%)**

