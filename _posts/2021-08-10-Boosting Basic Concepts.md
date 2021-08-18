---
date: 2021-08-10
title: "부스팅 (Boosting) 개념 이해하기 쉬운 수식 정리"
categories: 
 - Math
tags:
 - 머신러닝
 - 기계학습
 - 부스팅
 - 통계학습
 - Ensemble
 - 앙상블
 - Boosting
author: Hyeong
description: 부스팅 개념 정리
---
__Boosting__ 은 모델을 순차적으로 결합하는 모델 합성 방식이다. 첫 부스팅 알고리즘인 AdaBoost가 등장한 지 20년이 넘었기 때문에
구체적인 알고리즘은 모델마다 크게 다르지만, 순차적으로 이전 모델들의 오답에 유의하여 새 모델을 학습하는 아이디어는 동일하다.

이번 포스트에서는 가장 기초적인 AdaBoost를 뜯어보며 '순차적'으로 '오답'에 유의한다는 것이 어떤 의미인지 알아볼 것이다. 
비유를 들어서 설명하고 싶었는데 너무 길어진다.. 그냥 수식 쓰는 게 마음 편할 것 같다.

#### Step 1: 모델의 총오차
AdaBoost는 약한 학습자 (weak learner) 여럿을 합쳐 판단을 한다. Adaboost에서는 약한 학습자로 그루터기 (stump)를 사용하는데, 그루터기는
하나의 변수만을 사용하여 판단을 내리고, 그 판단은 이분법적이다. 그루터기가 궁금한 사람들은 [그루터기에 대한 설명](https://en.wikipedia.org/wiki/Decision_stump)을 읽어보자.
각설하고, 그루터기가 정확할수록, 그리고 이전 모델이 못 맞춘 문제를 잘 맞출수록 발언권이 세진다. 이 발언권은 나중에 최종 투표를 할 때, 그리고 자기 다음 모델이 얼마나 문제를
잘 맞추는지 판단하는데 쓰인다.

재밌는 스팀 게임을 판단하는 모델을 만든다고 가정하자. 데이터의 개수는 100개, 독립 변수는 별점, 판매량, 판매 가격, 그리고 종속 변수는 재미 (-1 혹은 1)라고 하자.

이때 각 데이터의 가중치(sample weight)는 1/100이다. 첫 단계에서 제일 성능이 좋은 그루터기 모델을 뽑았는데, 이 그루터기는 별점 변수를 사용했다고 가정하자 (분류가 얼마나 잘 됬는지 판단할 때는 지니 계수를 사용한다).
잘못 분류한 데이터의 개수를 10개라고 하면, 총오차 (total error)는

<img src="https://latex.codecogs.com/gif.latex?TE_i&space;=&space;10/100&space;=&space;1/10,&space;(0&space;\leq&space;TE_i&space;\leq&space;1)" title="TE_i = 10/100 = 1/10, (0 \leq TE_i \leq 1)" />

#### Step 2: 발언권 계산 
발언권(Amount of Say)는 다음과 같은 수식으로 구해진다.

<img src="https://latex.codecogs.com/gif.latex?A_i&space;=&space;\frac{1}{2}log(\frac{1-TE_i}{TE_i})" title="A_i = \frac{1}{2}log(\frac{1-TE_i}{TE_i})" />

이 발언권은 마지막에 분류를 할 때 사용한다. 총오차가 1에 가까워지면 발언권은 마이너스 무한대로 발산한다. 너가 말하는 것의 반대가 맞을 확률이 높다는 뜻이다. 슈반꿀, 홍반꿀 같은 개념이라고 볼 수 있을 것 같다.
반대로 총오차가 0에 가까워지면 발언권은 양의 무한대로 발산한다. 총오차가 0.5이면 발언권은 0인데, 이 뜻은 자명하리라 생각한다.

아무튼 위 예에서 총오차는 1/10이었으니, 발언권은 약 1.1이다.

#### Step 3: 다음 모델을 위한 표본 가중치 설정
다음 모델을 훈련시키기 위해 표본을 다시 추출해야 하는데, 이번에는 이전 모델에서 틀린 표본이 더 잘 뽑히게 발언권을 사용해서 표본 가중치를 바꿔줄 것이다.

이전 모델에서 예측이 맞은 데이터의 가중치:
<img src="https://latex.codecogs.com/gif.latex?W_{i&plus;1}^n&space;=&space;W_{i}^n&space;exp(A_i)" title="W_{i+1}^n = W_{i}^n exp(A_i)" />

예측이 틀린 데이터의 가중치:
<img src="https://latex.codecogs.com/gif.latex?W_{i&plus;1}^n&space;=&space;W_{i}^n&space;exp(-A_i)" title="W_{i+1}^n = W_{i}^n exp(-A_i)" />

발언권이 양수인 경우 틀린 데이터는 가중치가 커지고, 맞은 데이터는 가중치가 작아진다. 발언권이 음수면 틀린 걸 맞았다고 생각해야하고, 맞은 걸
틀렸다고 생각해야하니 같은 음수인 경우에도 결국 같은 뜻이다.

이렇게 한 후 가중치에 대해 정규화를 진행해서 모든 가중치의 합을 1로 만들어 주면 된다.

#### Step4: 다음 모델에서 표본 추출
100개의 데이터에 대해 복원 추출을 100번 진행하되, 추출 확률을 가중치에 비례하게 설정한다. 간단한 트릭인데, 우리의 Adaboost는 0과 1 사이의
소수를 무작위로 생성해 추출했다

이렇게 추출한 100개의 표본에 대해 Step1부터 다시 반복한다. 새로운 표본 100개에 대해 가중치를 각각 1/100으로 다시 설정해준다. 똑같은 표본을 중복 추출했는데,
이건 노린거다. 틀렸던 데이터가 많이 들어있으니 이번에는 틀린 부분에 더 신경을 써서 학습하게 된다

#### Step5: 마지막 판단
이것을 M차례 반복하면, 각 단계마다 모델과 발언권을 얻을  수 있다. 각 모델의 판단 (-1 또는 1)에 발언권을 곱하고, 모든 모델에 대해 합을 구해 0보다 크면 재미있는 게임,
0보다 작으면 재미 없는 게임이라고 판단할 수 있겠다.