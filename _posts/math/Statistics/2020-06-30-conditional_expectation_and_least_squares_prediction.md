---
title: 조건부 기댓값과 최소제곱 예측
author: Monch
category: Statistics
layout: post
---

<h2>조건부 기댓값</h2>

$$X=a$$라는 관측값을 얻었을 때 $$Y$$를 예측하기 위해 조건부 확률 $$P(Y=b|X=a)$$를 계산하면 된다. 이외에 $$X=a$$라는 조건하에 Y의 조건부분포를 구해 그 기대값을 취하는 방식을 선택할 수도 있다.  
조건부 기대값은 다음과 같다.


$$
E[Y|X=a] \equiv \sum_{b}bP(Y=b|X=a)
$$


또한, 모든 X의 확률을 알고 있다면 다음을 구할 수 있다.

$$
E[Y] = \sum_b b P(Y=b) \\ =\sum_{b} b \sum_{a} P(Y=b,X=a) \\
=\sum_{b} b \sum_{a} \frac{P(Y=b,X=a)}{P(X=a)} P(X=a) \\
= \sum_{a} \sum_{b} b P(Y=b|X=a) P(X=a) \\
= \sum_{a} E[Y|X=a]P(X=a)
$$


<h2>최소제곱 예측</h2>



조건부분포 $$P(Y=b \mid X=a)$$가 주어지고 $$X$$의 값을 입력하면 $$Y$$의 전망값 $$\hat{Y}$$를 출력하는 프로그램을 작성했을 때, 제곱 오차 $$(Y-\hat{Y})^2$$의 기대값 $$E[(Y-\hat{Y})^2]$$를 최소로 하자.

다시 말하면, 'X를 입력했을 때 Y의 예측값이 나오는 형태의 함수 g 중 $$E[(Y-g(X))^2]$$이 최소가 되는 것을 답하라'라는 문제이다. 여기서 $$g(a)$$는 다음과 같이 표현할 수 있다.

$$
g(a)=E[Y|X=a]
$$

우선 이해하기 쉽도록 X를 1에서 3까지의 정수값을 가진다고 가정하자. 이때 제곱 오차의 기대값은


$$
E[(Y-\hat{Y})^2]=E[(Y-g(X))^2] \\
= \sum_{a=1}^3 \sum_{b} (b-g(a))^2 P(X=a,Y=b) \\
= \sum_{b}(b-g(1))^2 P(X=1,Y=b) \\
+ \sum_{b}(b-g(2))^2 P(X=2,Y=b) \\
+ \sum_{b}(b-g(3))^2 P(X=3,Y=b) \\
= (g(1)으로 정해진 양)+(g(2)으로 정해진 양)+(g(3)으로 정해진 양)
$$

처럼 세 개로 나뉘고 각각 최소가 되도록 개별적으로 조사하면 최적의 g를 얻을 수 있다.

$$
\sum_{b} (b-g(1))^2 P(X=1,Y=b) = \sum_{b} (b-g(1))^2 P(Y=b|X=1)P(X=1) \\
= P(X=1) \sum_{b} (b-g(1))^2 P(Y=b|X=1)
$$

여기서 $$P(X=1)$$은 고정이므로 결국 $$\sum_{b} (b-g(1))^2 P(Y=b \mid X=1)$$를 최소화 해야한다. 

$$
h_1 (g(1)) \equiv \sum_{b} (b-g(1))^2 P(Y=b|X=1)
$$

로 두고 $$g(1)$$에 대해 미분을 하면 다음과 같다.


$$
\frac{dh_{1}}{dg(1)} =2\sum_{b}(g(1)-b) P(Y=b|X=1) \\
=2 \left( \sum_{b} g(1) P(Y=b|X=1) - \sum_{b} b P(Y=b|X=1)\right) \\
=2 \left(g(1) \sum_{b} P(Y=b|X=1) - \sum_{b} b P(Y=b|X=1)\right) \\
=2(g(1) - E[Y|X =1])
$$

따라서 $$dh_{1}/dg(1) =0$$이 될 때( $$g(1)=E[Y \mid X=1]$$ 일 때), $$h_{1}(g(1))$$이 최소가 된다. 또한, g(2), g(3)도 동일하다.

결과적으로 $$g(a) = E[Y \mid X=a]$$일 때 최소화된다.

