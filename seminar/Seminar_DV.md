---
sort: 6
---

# 데이터 시각화 교과서📖

> 데이터 시각화는 '예술'이자 '과학'이다.
> 과학적으로 정확하면서 미적으로 탁월하여 정보를 오도나 왜곡하지 않도록 한다.

---

### 데이터 시각화 꼭 해야하나?🤷🏻‍♀️🤷🏻‍♂️

**1. 분석은 우리가 <u>의사결정은 현업이</u>!**<br><br>

**2. 요약 통계보다 정확한 데이터 분석 결과를 도출할 수 있다.**

> _요약 통계만 믿지 말고, 데이터를 시각화하라!_<br> - Alberto Cairo(데이터 시각화 분야의 유명 인사)<br>

<br>

<p align =center>
<img src = https://d2f99xq7vri1nk.cloudfront.net/DinoSequentialSmaller.gif height="400"><br>

➤ Autodesk Research에 의하면 동일한 요약 통계 정보를 가지고 있으나, 시각화했을 때 시각적으로 뚜렷하게 구분되는 12개의 데이터 셋(Datasaurus Dozen)의 개발 결과 발표<br>

➤ 소수점 두 자릿 수 기준으로 동일한 요약 통계를 갖는 12개의 데이터 셋의 시각적 패턴은 모두 다름<br><br>

💡 **데이터 시각화는 <u>데이터 분석 결과를 전달</u>하기 위한 목적뿐만 아니라 정확한 분석을 위한 <u>데이터 탐색 방법</u>으로 활용**<br><br><br>

**3. 효과적인 데이터 인사이트 공유로 데이터 기반의 의사결정을 할 수 있다!**

➤ 시각화 자료는 사람들의 머릿속에 빠르게 인지되고 기억될 뿐만 아니라, <u>메시지의 스토리텔링</u>에 대한 공감을 더함

---

## 목차

- [1. 데이터 시각화: '읽는' 데이터에서 '보는' 데이터로](#1-데이터-시각화:-'읽는'-데이터에서-'보는'-데이터로)
- [2. 위치 스케일: 좌표와 축](#2-위치-스케일:-좌표와-축)
- [3. 색상 스케일](#3-색상-스케일)
- [4. 수량 데이터의 시각화](#4-수량-데이터의-시각화)
- [5. 데이터 분포의 시각화](#5-데이터-분포의-시각화)
  - [히스토그램과 밀도 도표](#히스토그램과-밀도-도표)
- [6. 여러 분포 상태의 결합 시각화](#6-여러-분포-상태의-결합-시각화)
  - [가로축](#가로축)
  - [세로축](#세로축)
    <br>
    <br>

## 다양한 시각화 방식

**[수량의 시각화]**

<p align ="right">
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/amounts-1.png width = "800" height="210"><br>
<p align =center>
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/amounts_multi-1.png width = "800" height="400"><br>

**[분포의 시각화]**

<p align =center>
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/single-distributions-1.png  width = "800" height="200"><br>
<p align =center>
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/multiple-distributions-1.png width = "800" height="400"><br>

**[비율의 시각화]**

<p align =center>
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/proportions-1.png height="200"><br>
<p align =center>
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/proportions-comp-1.png height="200"><br>
<p align =center>
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/proportions-multi-1.png height="200"><br>

**[x-y 관계로 나타내는 시각화]**

<p align =center>
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/basic-scatter-1.png height="200"><br>
<p align =center>
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/xy-binning-1.png height="200"><br>
<p align =center>
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/xy-lines-1.png height="200"><br>

**[지리공간 데이터의 시각화]**

<p align =center>
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/geospatial-1.png height="200"><br>

**[불확실성의 시각화]**

<p align =center>
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/errorbars-1.png height="200"><br>
<p align =center>
<img src =https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/confidence-dists-1.png height="200"><br>
<p align =center>
<img src = https://clauswilke.com/dataviz/directory_of_visualizations_files/figure-html/confidence-bands-1.png height="200"><br>

## 1. 데이터 시각화: '읽는' 데이터에서 '보는' 데이터로

- 데이터 시각화는 체계적이고 논리적인 방식을 통해 데이터 값을 `시각적 속성`으로 변환한 다음, 속성들로 최종 그래프를 만드는 과정
- `시각적 속성`?
<p align =center>
<img src = https://clauswilke.com/dataviz/aesthetic_mapping_files/figure-html/common-aesthetics-1.png height="300"><br>

- 연속형 데이터: position, size, color, line width
- 이산형 데이터: shape, line type
- 모두: position, size, color, line width
- 그럼 데이터를 시각적 속성으로 어떻게 표현할까?
  - 데이터 값을 시각적 요소로 전환할 때 `스케일`이 필요함
  - 스케일: 데이터와 시각적 속성과의 연결방식, 반드시 <u>일대일로 대응되어야 함</u>
  - 아래 그림은 위치(position) 스케일, 형태(shape) 스케일, 색상(color) 스케일을 나타냄
  <p align =center>
  <img src = https://clauswilke.com/dataviz/aesthetic_mapping_files/figure-html/basic-scales-example-1.png height="200"><br>

[예시 - 미국 기상 관측소 네 곳에서 측정한 일별 평년 기온]<br>

![scale_example_data](..\\assets\\images\\visualization\\scale_example_data.png)

**<표현 방법 1>**<br>

<p align =center>
<img src = https://clauswilke.com/dataviz/aesthetic_mapping_files/figure-html/temp-normals-vs-time-1.png height="400"><br>

- y축: 기온
- x축: 날짜
- 색: 지역

**<표현 방법 2>**<br>

<p align =center>
<img src = https://clauswilke.com/dataviz/aesthetic_mapping_files/figure-html/four-locations-temps-by-month-1.png height="300"><br>

- y축: 지역
- x축: 월
- 색: 온도

## 2. 위치 스케일: 좌표와 축

- 데이터 시각화에 가장 흔히 쓰이는 좌표계는 2D `데카르트 좌표계`
- `데카르트 좌표계`는 x, y축으로 구성되고, 두 축의 단위는 다르지만 반드시 한 축의 데이터 값을 다른 축 값에 비례하게 늘리거나 줄여야 함

<p align =center>
<img src = https://clauswilke.com/dataviz/coordinate_systems_axes_files/figure-html/temperature-normals-Houston-1.png height="450"><br>

- 일반적으로는 간격을 일정하게 유지하는 선형적 위치 스케일을 많이 이용함
- 그러나, 일부 로스 스케일과 같이 비선형 스케일이 유용할 경우가 있음
- '비율' 값은 로그 스케일을 많이 사용함

[예시 - 텍사스 전체 인구 중간 값에 대비한 카운티별 인구 수]

<p align =center>
<img src = https://clauswilke.com/dataviz/coordinate_systems_axes_files/figure-html/texas-counties-pop-ratio-log-1.png height="350"><br>

<p align =center>
<img src = https://clauswilke.com/dataviz/coordinate_systems_axes_files/figure-html/texas-counties-pop-ratio-lin-1.png height="350"><br>

## 3. 색상 스케일

- 데이터 시각화에 색을 사용하는 이유 3가지
  1. 데이터를 잘 구분
  2. 데이터 값을 잘 나타냄
  3. 데이터 값을 잘 강조

1. 데이터를 잘 구분하기 위한 색상

- 순서 개념이 없는 데이터 항목이나 데이터 그룹을 색으로 구분지음
- 이때, `정성적 색상 스케일`을 사용
- `정성적 색상 스케일`은 한정된 색들로 구성하며, 이 색들을 서로 동등하게 치부하면서 확실하게 구별해야 함
- 색에 순서가 정해져 있다는 인식을 주면 안됨

<p align =center>
<img src = https://clauswilke.com/dataviz/color_basics_files/figure-html/qualitative-scales-1.png height="300"><br>

[예시 - 2000~2010년 미국 인구 성장률]

<p align =center>
<img src = https://clauswilke.com/dataviz/color_basics_files/figure-html/popgrowth-US-1.png height="600"><br>

2. 데이터 값을 잘 나타내기 위한 색상

- 순서 개념이 있는 데이터 항목이나 데이터 그룹을 색으로 구분지음
- 이때, `순차적 색상 스케일`을 사용
- `순차적 색상 스케일`은 색에 순서를 부여해서 값의 크기 차이, 특정한 두 값 사이의 거리를 명확하게 보여줌
- 하나의 색조의 채도를 다르게 표현하거나, 여러 색조로 표현하되 자연물에서 볼 수 있는 그라데이션을 따름(암적색 -> 노란색, 남색 -> 녹색 -> 연한 노란색)

<p align =center>
<img src = https://clauswilke.com/dataviz/color_basics_files/figure-html/sequential-scales-1.png height="300"><br>

[예시 - 텍사스 카운티의 연간 중위소득(단계구분도)]

<p align =center>
<img src = https://clauswilke.com/dataviz/color_basics_files/figure-html/map-Texas-income-1.png height="400"><br>

- 중립적인 중간점에서 데이터 값들 간의 편차를 나타내기 위해서는 `발산형 색상 스케일`을 씀
- 이때 중간 점은 보통 가장 연한 색으로 타나내며, 양쪽으로 점점 짙은 색으로 바뀜

<p align =center>
<img src = https://clauswilke.com/dataviz/color_basics_files/figure-html/diverging-scales-1.png height="300"><br>

[예시 - 텍사스 카운티에 거주하는 백인 비율]

<p align =center>
<img src = https://clauswilke.com/dataviz/color_basics_files/figure-html/map-Texas-race-1.png height="400"><br>

3. 데이터 값을 잘 강조하기 위한 색상

- 데이터셋에서 도표의 주제에 대한 핵심 정보를 담은 값이나 범주를 알아보기 쉽게 표현하기 위해 다른 값과 확실하게 구별되는 색을 부여함

[예시 - 인기 종목 선수들의 신장 정보]

<p align =center>
<img src = https://clauswilke.com/dataviz/color_basics_files/figure-html/Aus-athletes-track-1.png height="300"><br>

➤ 알 수 있는 사실: 인기 종목의 남성 선수 중 육상 달리기 종목 선수들이 가장 키가 작고 말랐다.

## 4. 수량 데이터의 시각화

- 수량을 시각화하는데 주로 사용 되는 것은<br>
- 막대 도표
  - 기본 막대
  - 묶은 막대
  - 누적 막대 도표
- 점 도표
- 히트맵

1. 막대 도표(Bar Chart)

- 기본 막대<br>

[예시 1 - 값에 순서가 있을 때]

![수량_데이터_막대도표](..\\assets\\images\\visualization\\수량_데이터_막대도표.png)

- 🤔어떤 그래프가 보기 좋은가요?<br>

![barchart_1](..\\assets\\images\\visualization\\barchart_1.png)
![barchart_2](..\\assets\\images\\visualization\\barchart_2.png)

[예시 2 - 범주에 순서 속성이 있을 때]

<p align =center>
<img src = https://clauswilke.com/dataviz/visualizing_amounts_files/figure-html/income-by-age-1.png height="300"><br>

<p align =center>
<img src = https://clauswilke.com/dataviz/visualizing_amounts_files/figure-html/income-by-age-sorted-1.png height="300"><br>
<br>

- 묶은 막대와 누적 막대
  : 범주형 변수 두 가지를 동시에 다룰 때 주로 사용<br><br>

[예시 1 - 미국의 연령별 연간 중위 가계소득을 연령대와 인종별로 구분]

<p align =center>
<img src = https://clauswilke.com/dataviz/visualizing_amounts_files/figure-html/income-by-age-race-dodged-1.png height="300"><br>

<p align =center>
<img src = https://clauswilke.com/dataviz/visualizing_amounts_files/figure-html/income-by-race-age-dodged-1.png height="300"><br>

👍추천 차트

<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_amounts_files/figure-html/income-by-age-race-faceted-1.png height="400"><br>

[예시 2 - 타이타닉 1,2,3 등실에 탑승한 여성,남성 승객 비율]<br>

<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_amounts_files/figure-html/titanic-passengers-by-class-sex-1.png height="400"><br>

➤ y축을 명확하게 표시하지 않아도 도표에 <u>실제 숫자 값을 넣음</u>으로 도표를 어수선하게 만들지 않으면서도 많은 정보를 전달할 수 있음<br>
<br>

2. 점 도표(Dot plot)

- 막대 도표는 항상 기준점이 '0'이어야 함
- 그러나, 기준 점을 '0'으로 잡음으로 요점을 잘 전달할 수 없거나 시각화하기 힘든 데이터가 존재함

[예시 - 아메리카 대륙 나라들의 기대 수명]

<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_amounts_files/figure-html/Americas-life-expect-bars-1.png height="400"><br>

👍추천 차트

<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_amounts_files/figure-html/Americas-life-expect-1.png height="400"><br>

3. 히트맵(Heatmap)

- 데이터 값을 20개씩 묶은 범주 20개로 구성된 데이터 셋을 시각화한다면?
- 데이터 셋이 아주 방대한 경우 막대나 점 대신 색으로 데이터 값을 나타내는 도표
- 정확한 데이터 값은 알기 어렵지만 <u>전체적인 추세</u>를 확인하기 좋음

<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_amounts_files/figure-html/internet-over-time-1.png height="400"><br>
<br>

## 5. 데이터 분포의 시각화

### 히스토그램과 밀도 도표

- `히스토그램`: 도수분포표 데이터를 나타내는 차트
- `히스토그램` 구간의 폭을 다양하게 적용해보면서 데이터를 정확하게 보여주는 폭을 찾아야 함

[예시 - 타이타닉 승선객 연령분포]<br>

![histogram](..\\assets\\images\\visualization\\histogram.png)

- 🤔어떤 그래프가 보기 좋은가요?<br>
<br>
<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_distributions_I_files/figure-html/titanic-ages-hist-grid-1.png height="400"><br>

- 최근엔 `밀도 도표(Density plot)`를 그리는 추세
- `밀도 도표`: 연속적인 곡선으로 데이터의 내재된 확률 분포 표현
- 여기서 곡선은 데이터를 바탕으로 추산해야 하며, `커널 밀도 추정` 방식을 가장 많이 사용함
- `커널 밀도 추정`: 데이터 포인트 지점마다 폭이 좁은 연속 곡선(커널)을 그린 다음 곡선들을 전부 더해서 최종 밀도 추정 값을 구하는 작업
- 여기서 밀도는 확률 밀도(probability density)를 의미
- 어떤 변수 x의 밀도를 추정하는 것은 x의 확률 밀도 함수 f(x)를 추정하는 것과 같음

<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_distributions_I_files/figure-html/titanic-ages-dens1-1.png height="300"><br>

- `밀도 도표`는 '커널'과 '대역폭' 설정 방식에 따라 결정

<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_distributions_I_files/figure-html/titanic-ages-dens-grid-1.png height="400"><br>

    - a: 가우시안 커널, 대역폭 0.5
    - b: 가우시안 커널, 대역폭 2
    - c: 가우시안 커널, 대역폭 5
    - d: 직사각 커널, 대역폭 2

<br>

> **🙅🏻‍♀️🙅🏻‍♂️ 주의해야할 점**

<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_distributions_I_files/figure-html/titanic-ages-dens-negative-1.png height="300"><br>

➤ 밀도 추정 시 터무니없는 데이터 값이 들어가지 않는지 꼭 확인해야 함!

#### 여러 분포 상태를 하나의 도표로 시각화

[예시 - 성별에 따른 타이타닉호 승선객 연령대 분포 차이]

- 누적 히스토그램(Stacked histogram)

<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_distributions_I_files/figure-html/titanic-age-stacked-hist-1.png height="300"><br>

- 중첩 밀도 도표(Overlapping density plot)

<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_distributions_I_files/figure-html/titanic-age-overlapping-dens-1.png height="300"><br>

👍추천 차트 1

<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_distributions_I_files/figure-html/titanic-age-fractional-dens-1.png height="300"><br>

👍추천 차트 2

- 연령 피라미드

<p align =center>
<img src =https://clauswilke.com/dataviz/visualizing_distributions_I_files/figure-html/titanic-age-pyramid-1.png height="300"><br>

## 6. 여러 분포 상태의 결합 시각화

### 가로축

- `박스플롯`: 분포 상태 시각화에 쓰이는 방식
- 박스플롯 가운데를 지나는 선은 중간 값
- 울타리 밖에 자리하는 데이터 포인트는 각각 이상값이라 하고, 따로 점을 찍음
<p align =center>
<img src =https://clauswilke.com/dataviz/boxplots_violins_files/figure-html/boxplot-schematic-1.png height="300"><br>

[예시 - 2016년 네브라스카주 링컨시의 일평균 기온]

<p align =center>
<img src =https://clauswilke.com/dataviz/boxplots_violins_files/figure-html/lincoln-temp-points-errorbars-1.png height="300"><br>

<p align =center>
<img src =https://clauswilke.com/dataviz/boxplots_violins_files/figure-html/lincoln-temp-boxplots-1.png height="300"><br>

➤ 위 차트와 달리 `박스플롯`으로 아래 차트와 같이 표현하면 여러 가지 분포를 도표 하나에 나란히 시각화할 때 유용함<br>
➤ 12월의 기온은 비대칭성이 가장 강함<br>
<br>

- `바이올린 도표(Violin plot)`: 데이터들의 밀도를 표현하는 차트로, y값의 점밀도가 바이올린의 너비를 의미함
- 바이올린 도표의 시작점과 끝점이 각각 데이터의 최솟값과 최댓값
<p align =center>
<img src =https://clauswilke.com/dataviz/boxplots_violins_files/figure-html/lincoln-temp-violins-1.png height="300"><br>

<p align =center>
<img src =https://clauswilke.com/dataviz/boxplots_violins_files/figure-html/lincoln-temp-sina-1.png height="300"><br>

### 세로축

- 분포를 세로로 층층이 배치한 모양
- `융기선 도표(Ridgeline plot)`: 시간의 흐름에 따른 분포 추세를 보여줄 때 유용함
<p align =center>
<img src =https://clauswilke.com/dataviz/boxplots_violins_files/figure-html/temp-ridgeline-1.png height="300"><br>

[예시 - 시간의 흐름에 따른 영화 상영시간의 변화]

<p align =center>
<img src =https://clauswilke.com/dataviz/boxplots_violins_files/figure-html/movies-ridgeline-1.png height="450"><br>

➤ 1960년대부터 모든 영화의 상영시간 대부분은 90분 정도로 정착<br>

    - 바이올린 도표와 융기선 도표 모두 특정 밀도 값을 보여주기 위해서가 아니라,
    각 그룹 전반의 밀도 형태와 상대적인 높이를 쉽게 비교하기 위해 사용하는 방식
