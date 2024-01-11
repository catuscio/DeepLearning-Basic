# 퍼셉트론(Perceptron)
- 뉴런과 뉴런이 연결되는 인간의 뇌 구조를 본딴 연구가 바로 인공신경망(Artificial Neural Network)이다.
- 신경망을 이루는 가장 중요한 기본 단위를 퍼셉트론(perceptron)이라고 한다.
- 퍼셉트론은 입력 값과 활성화 함수를 사용해 출력 값을 다음으로 넘기는 역할을 한다.

## 용어 정리
$$y = wx + b$$
|용어|뜻|
|-|-|
|$w$|가중치, weight|
|$b$|편향, bias|


- 가중합(weighted sum)
$$\sum^{n}_{i} x_i w_i + b$$

- 활성화 함수(activation function)\
가중합의 결과를 놓고 1 또는 0을 판단하는 함수. e.g)시그모이드 함수

## XOR 문제 - 퍼셉트론의 한계
- XOR(exclusive OR)

- AND 진리표

|$x_1$|$x_2$|결괏값|
|-|-|-|
|0|0|0|
|0|1|0|
|1|0|0|
|1|1|1|

- OR 진리표

|$x_1$|$x_2$|결괏값|
|-|-|-|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|1|

- XOR 진리표

|$x_1$|$x_2$|결괏값|
|-|-|-|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

XOR 게이트는 좌표평면에 $x_1 - x_2 그래프$를 그려 구분할 수 없다.
이러한 문제는 신경망의 입력층과 출력층 사이에 은닉층(hidden layer)를 삽입하는 것으로 해결할 수 있다.

## 다층 퍼셉트론
은닉층의 노드node는 입력층의 가중치와 바이어스를 시그모이드 함수를 이용해 최종 값으로 결과를 보낸다.
가령, input이 $x_1$, $x_2$일 때 노드의 연산은 다음과 같다.\

$$n_1 = \epsilon (x_1 w_11 + x_2 w_21 + b_1)$$
$$n_2 = \epsilon (x_1 w_12 + x_2 w_22 + b_2)$$

출력값 $y$의 연산은 다음과 같다.
$$y_out = \epsilon (n_1 w_31 + n_2 w_32 + b_3)$$

$$ W(1) = \begin{bmatrix} -2 & -2\\
-2 & 2 \end{bmatrix}$$

$$B(1) = \begin{bmatrix} 3\\
-1 \end{bmatrix}$$

$$W(2) = \begin{bmatrix} 1\\
1 \end{bmatrix}$$

$$B(2) = \begin{bmatrix} -1 \end{bmatrix}$$

---
## 코드로 구현해보기
https://github.com/catuscio/DeepLearning-Basic/blob/main/colab%20workout/XOR_Problem.ipynb


---
# 오차 역전파(back propagation)
입력층, 은닉층, 출력층으로 이루어진 신경망에서, 연산에 필요한 가중치와 바이어스를 구하는 방법이다.\
오차 역전파는 경사 하강법의 다층 퍼셉트론에 대한 응용이다.\
다층 퍼셉트론에서는 (1)출력층 가중치를 수정하고 (2)은닉층 가중치를 수정하는 방향으로 나아간다.

1. 임의의 초기 가중치($W$)를 대입하여 결과($y_{out}$)를 계산한다.
2. 계산 결과와 우리가 원하는 값 사이의 오차를 구한다.
3. 경사 하강법을 이용해 바로 앞 가중치를 오차가 작아지는 방향(=기울기가 0이 되는 방향)으로 갱신한다.
4. 위 과정을 오차가 최소가 될 때까지 반복한다.

해당 과정을 수식으로 나타내면 다음과 같다.
$$W(t+1) = W_t - \frac{\delta 오차}{\delta W}$$

---
# 지난 주차 실습 과제
https://github.com/catuscio/DeepLearning-Basic/blob/main/colab%20workout/LogisticRegression_forStudent_ipynb%EC%9D%98_%EC%82%AC%EB%B3%B8.ipynb
