---
title:  "[Machine Learning] 다중 선형 회귀"
excerpt: "Multiple linear regression"

categories:
  - Machine Learning

toc: true
toc_sticky: true
toc_label: "다중 선형 회귀"

last_modified_at: 2022-01-02
---

## 다중 선형 회귀

여태는 이해의 편의를 위해 입력 변수가 1개인 경우로 한정해서 생각했는데요,<br>
그런데 실제 상황에서는 입력 변수가 하나밖에 없는 경우는 굉장히 드뭅니다.<br>
예를 들어, 집 값은 그 집의 평수만으로 예측하기엔 무리가 있죠,<br>
그래서 보통은 훨씬 많은 입력 변수를 갖고 예측을 합니다.

이렇게 여러 입력 변수를 가지고 선형 회귀를 하면 다중 선형 회귀(Multiple Linear Regression)라고 합니다.

다중 선형 회귀는 시각적으로 표현하기 힘들어서 이해하기가 힘들 수 있는데<br>
시각화를 못할 뿐이지 기본 개념은 이전 챕터에서 했던 것과 거의 똑같습니다.

## 다중 선형 회귀 표현법

다중 선형 회귀에서는 앞서 말했듯이 입력 변수가 여러 개 있습니다.<br>
입력 변수의 개수는 n이라는 변수로 표현하고,<br>
i번째 입력 변수는 \\(x_{i}\\)라고 표현합니다.

학습 데이터의 개수는 똑같이 m이라고 표현하고,<br>
i번째 학습 데이터는 \\(x^{(i)}\\)라고 표현하고,<br>
i번째 목표 변수는 \\(y^{(i)}\\)라고 표현합니다.

i번째 학습 데이터의 j번째 속성(입력 변수)은 \\(x_{j}^{(i)}\\)라고 표현합니다.

## 다중 선형 회귀 가설 함수

입력 변수가 하나였을 때 가설 함수는<br>
\\(h(x) = \theta_0 + \theta_{1}x\\) 이렇게 생겼었습니다.

어떤 입력 변수 하나를 받고 목표 변수를 출력하는 형태입니다.

다중 선형 회귀에서는 아래와 같이 가설 함수를 표현합니다.

\\[h(x) = \theta_0 + \theta_{1}x_{1} + \theta_{2}x_{2} + \dots + \theta_{n}x_{n}\\]

\\(\theta_{0}\\)은 그냥 상수항이고,<br>
\\(\theta_{i}\\)는 \\(x_{i}\\)가 \\(y_{i}\\)에 미치는 영향이라고 생각하면 됩니다.

뭔가 복잡해보이지만 사실 그냥 항이 많아진 일차함수입니다.<br>
여기서도 마찬가지로 목적은 \\(\theta\\)값들을 조금씩 조율하며 학습 데이터에 가장 잘 맞는 \\(\theta\\)들을 찾아내는 것입니다.

그런데 위와 같이 긴 수식으로 표현하면 조금 복잡합니다.<br>
선형대수학의 벡터를 이용하면 좀 더 간결히 표현할 수 있습니다.

\\( \theta =  \left[
\begin {array}{c}
    \theta_{0}  \newline
    \theta_{1}  \newline
    \vdots      \newline
    \theta_{n}  \newline
\end{array}
\right],
x =  \left[
\begin {array}{c}
    x_{0}   \newline
    x_{1}   \newline
    \vdots  \newline
    x_{n}   \newline
\end{array}
\right] \\)

라고 하면, 가설 함수를 아래와 같이 표현할 수 있습니다.

\\[h_{\theta}(x) = \theta^{T}x\\]

## 다중 선형 회귀 경사 하강법

다중 선형 회귀에서 경사 하강법을 시각적으로 표현하긴 어렵지만,<br>
수학적으로 보면 거의 똑같습니다.

다중 선형 회귀에서도 손실 함수가 똑같이 아래와 같이 생겼습니다.

\\[\displaystyle J(\theta) = \frac{1}{m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)}) - y^{(i)})^2\\]

다중 선형 회귀에서는 입력 변수가 여러 개라 가설 함수가 살짝 달라지기만 합니다.

그리고 손실을 줄이기 위해 마찬가지로 경사 하강법을 적용해야 하는데요,<br>
입력 변수가 하나일 때는 \\(\theta_{0}\\)과 \\(\theta_{1}\\)만 업데이트하면 됐는데,<br>
입력 변수가 여러 개면 \\(\theta\\) 값도 여러 개라 그냥 업데이트 할 \\(\theta\\) 값이 많아지는 것 뿐입니다.

이는 아래와 같이 표현할 수 있습니다.

\\[\displaystyle j = 1부터 n까지: \theta_{j} = \theta_{j} - \alpha\frac{2}{m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)}) - y^{(i)}) \cdot x_{j}^{(i)}\\]

이 과정을 한 번 거칠 때마다 손실을 최대한 빨리 감소시키는 방향으로 \\(\theta\\)값들이 업데이트됩니다.<br>
이걸 충분히 반복하면 손실을 최소에 가깝게 줄일 수 있습니다.

다중 선형 회귀에서 \\(\theta\\)의 변화를 수식으로 나타내면 다음과 같습니다.

\\[ X = \left[
\begin {array}{cccc}
    x_{0}^{(1)} & x_{1}^{(1)} & \dots & x_{n}^{(1)} \newline
    x_{0}^{(2)} & x_{1}^{(2)} & \dots & x_{n}^{(2)} \newline
    \vdots & & & \newline
    x_{0}^{(m)} & x_{1}^{(m)} & \dots & x_{n}^{(m)} \newline
\end {array}
\right],
\theta = \left[
\begin {array}{c}
\theta_{0} \newline
\theta_{1} \newline
\vdots \newline
\theta_{n} \newline
\end {array}
\right],
y = \left[
\begin {array}{c}
y_{0} \newline
y_{1} \newline
\vdots \newline
y_{m} \newline
\end {array}
\right] \\]일 때,

\\[ \displaystyle \theta = \theta - \alpha\frac{2}{m}X^{T}(X\theta - y) \\]

## 정규 방정식 (Normal Equation)

여태는 손실을 줄이기 위해 경사 하강법을 사용했는데,<br>
다른 방법도 있습니다.

경사 하강법에서는 특정 지점에서 시작해서 조금씩 아래로 향해서 극소점을 찾아간 건데,<br>
극소점은 기울기가 0이므로 기울기가 0인 지점을 찾는 방법도 있습니다.

따라서, 손실 함수의 기울기가 0이 되는 지점을 방정식을 풀어서 찾아내면 됩니다.<br>
이렇게 방정식을 통해 극소점을 찾는 방법을 정규 방정식 (Normal Equation)이라고 합니다.

그런데 방정식을 매번 직접 푸는 건 어렵습니다.<br>
따라서, 아래와 같은 식을 계산하면 손실 함수의 기울기가 0이 되도록 하는 \\(\theta\\)를 구할 수 있습니다.

\\[ \theta = (X^{T}X)^{-1} \cdot X^{T}y \\]

## 경사 하강법 vs 정규 방정식

경사 하강법과 정규 방정식은 다음과 같은 차이가 있습니다.

| 경사 하강법 | 정규 방정식 |
| --- | --- |
| 적합한 학습율을 찾거나 정해야 한다. | 학습율을 정할 필요가 없다. |
| 반복문을 사용해야 한다. | 한 번에 계산을 끝낼 수 있다. |
| 입력 변수의 개수 n이 커도 효율적으로 계산 가능하다. | n이 커질수록 비효율적이다. |
| | 역행렬이 존재하지 않을 수도 있다. (pseudo inverse를 이용해서 계산하는 방법이 있기 때문에 큰 문제는 안된다.) |

이 둘 중 어떤 걸 선택해야 하는지에 대한 정답은 없습니다.

주어진 상황과 데이터에 맞게 정하는 것이 좋습니다.

## convex 함수

convex 함수는 아래로 볼록한 함수인데요,<br>
convex 함수에서는 항상 경사 하강법이나 정규 방정식을 이용해서 최소점을 구할 수 있는 반면,<br>
non-convex 함수에서는 구한 극소점이 최소점이라고 확신할 수 없습니다.

다행히 MSE는 항상 convex 함수입니다.<br>
따라서 선형 회귀를 할 때는 경사 하강법을 하나 정규 방정식을 하나 항상 최적의 \\(\theta\\)를 구할 수 있습니다.

## scikit-learn을 이용한 간단한 다중 선형 회귀

<script src="https://gist.github.com/Geniemo/be612cdd5c1a80bd1627da1bd4ad3ee5.js"></script>