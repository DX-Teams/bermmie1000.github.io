---
sort: 7
---

# Generalization
- 참고 추천 사이트: http://dmqm.korea.ac.kr/activity/seminar?p=1&s%3D
<br>
# Machine Learning

Q. 모델 학습 후 어떤 기준으로 모델을 선택하나요?

Trained model ultimately needs to have __<u>consistency between train data and future data.</u>__ 
- Traning data
- Future data
- We want to do well on future data
    - Trained model doesn't work well = Low performance in test data
    - Problems
        1. Underfitting
            - the number of hyperparameters, imappropriate model
            - new domain : unseen environment
        1. Overfitting
            - small data(compared to the number of parameters), complex model
            - new data (new or unexpected pattern) : usually same domain
                - small data

<br><img src='https://cdn.analyticsvidhya.com/wp-content/uploads/2020/02/Screenshot-2020-02-06-at-11.06.24.png' width='450'>

> k-fold 검증  
- k-fold, stratified K Fold 등의 검증 방법은 특정 모델의 성능에 대한 일반적인 지표를 알고자 검증하는 것.  
 즉, "모델이 갖는 성능을 일반화"하는 것. 어떤 데이터에는 성능이 높고, 어떤 데이터에는 성능이 낮고 할 수 있으니 전체적인 성능값을 파악하기 위해 고안된 방법.

<br><br>
# Generalization(일반화)
- Future Data를 잘 맞추기 위한 장애물들 해결하기 위한 방법
- 목적: Train data와 Input data가 달라져도 출력에 대한 성능 차이가 나지 않게 하는 것
    - Generalization Error <-> Train Error
    - Robust Model: 이상치나 노이즈에 크게 흔들리지 않음

> Always Best is <u>Augmenting Data</u>.  
> When impossible we need to use several methods.

> Optimization(최적화)
> - 손실함수를 최소화하는 Hyper Parameter 값을 찾는 것
> - e.g. batch-size, learning-rate 등


<br><br>
# Method

## Underfit
### 새로운 방식의 모델
* Domain Adaptation(DA)
<br><img src='https://ars.els-cdn.com/content/image/1-s2.0-S0165168418303967-gr1.jpg' width=500>  
Train data의 domain과 Future data의 domain이 다른 경우(Domain shift)에 사용되는 방법  
e.g.) MNIST Data -> 숫자 by 맑은 고딕, 한국에서 자동차 detection -> 미국에서 자동차 detection
    - supervised adaptation
    - unsupervised adaptation
    : 이전 task에서 배운 지식을 사용해 (정답이 없는) 새로운 상황에서도 맞출 확률을 올려주는 방법

* Like batch normalization, weight initialization etc., Domain Adaption(DA) is the way of improving performance
* DA is one of concepts for transfer learning. There are lots of application for DA.
    - Research Area: https://paperswithcode.com/task/domain-adaptation?page=18

* Reference Link: https://blog.lunit.io/2018/04/24/deep-supervised-domain-adaptation/  
https://www.youtube.com/watch?v=GmqW_v_bXiM


## Overfit
### 기존 모델에 제한 추가
* Parameter constraints (Regularization)
    * Neural Net: Dropout (<-> Fully-Connected)
    <br><img src='https://blog.kakaocdn.net/dn/rETIS/btqKoo3zriE/8olZJ4GnhEMcMs2KjSuOC1/img.png' width=500>
        - parameter 개수 감소를 통해 모델 복잡성 완화

    * Linear Model: Weight Size Penalty
        - variance를 줄이기 위해 bias를 키우는 방법 (variance-bias trade-off)
<br>    <img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FIGyDl%2FbtqK71GSY3Q%2FP3pJ1E99LY2TUpGkzd8iw1%2Fimg.png'>
    <img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcbiHw0%2FbtqLcTuhyey%2FiNX3pCLeXT3Q6tztoTZh2K%2Fimg.png'>
    <br>![Regularization](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile4.uf.tistory.com%2Fimage%2F99BED3425CE4B1341814F6)
        - L2 norm(Ridge, Weight Decay) - 규제를 통해 이상치에 의한 변동성을 잡음 
        - L1 norm(Lasso): Feature Selection - appropriate for sparse model, still cannot differentiate at specific point, needed to be careful when do gradient-based learning        

        - Bias and Variance Tradeoff
            - Error(X) = noise(X) + bias(X) + variance(X)
            - High bias: not well trained (underfit)
            - High variance: fitted too much (overfit)
<br><img src='https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F5342660%2F79eb51fe9f8bfb0a9da32b500d2264e9%2FScreenshot%202020-08-04%2017.07.11.png?generation=1596541060787859&alt=media' width='400'>

        - Reference: https://data-science-hi.tistory.com/143
* Early Stopping
<br><img src='https://www.researchgate.net/publication/335604816/figure/fig2/AS:799391489220609@1567601191401/Bias-variance-trade-off-in-machine-learning-This-figure-illustrates-the-trade-off.png' width='450'>  
    - 모델 Fit이 잘 된 시점에 학습을 중단하는 방법
        - 너무 많은 epoch는 overfitting을 일으키고, 너무 적은 epoch는 underfitting을 일으킴

* Stacked Generalization
<br>![SG](https://miro.medium.com/max/946/1*T-JHq4AK3dyRNi7gpn9-Xw.png)

<br>
===
---
<br>


## Stacked Generalization (One of Ensemble)
* Ensemble Model
    - Voting: 서로 다른 알고리즘이 도출해낸 결과물에 대해 최종 투표하는 방식
    - Stacking: Performance 향상 목적 (Voting 진화 버전)
    - Bagging: Variance 감소 목적 (Random Forest 등)
    - Boosting: Bias 감소 목적 (XGBoost 등)
    
* What is Stacked Model?
    * Model Stacking is one of Ensemble which is the method of Generalization
    * Through making ensemble model, we can reduce the effect of overfitting problem.
* Model Average -> Weighted Averaging Model -> Stacked Generalization
* Stacking Step
    1. making sub-model results
    2. Input = results of sub-models, Output = target
        - Meta learner: simple linear or neural network
        - More various type of sub-model, better results
        - ** each model’s predictions becomes a slice of a new feature

> - 사람이 늘어나고, 각자의 좋은 점만 가져오는 것과 같은 원리 (각 모델의 장단점을 보완하지만 연산량 큼)  
> - Feature만 고려한 condition-base 모델과 결과 수치만 고려한 시계열 모델을 mix하는 것처럼 다양한 활용 가능  
> - 성능의 영혼까지 끌어모을 수 있음

* CODE
    - https://inspiringpeople.github.io/data%20analysis/Ensemble_Stacking/
    - https://mlfromscratch.com/model-stacking-explained/#/



