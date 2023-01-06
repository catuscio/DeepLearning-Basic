# 선형회귀(Linear Regression)
선형회귀란 러프하게 말해서 **'가장 훌륭한 예측선 긋기'** 이다.\
여러 값으로 산개되어 있는 데이터들을 분석하여, 선형 그래프로 요약하는 것이 선형회귀의 목적이다.

## 독립변수와 종속변수
종속변수 y는 결과를, 독립변수 x는 결과에 영향을 미치는 정보를 의미한다.\
독립변수는 독립적으로 변할 수 있으며, 종속변수는 이러한 독립변수의 변화에 종속적으로 반응하게 된다.

## 일차함수 그래프
독립변수를 $x$, 종속변수를 $y$라고 할 때, 일차함수 그래프 방정식은 다음과 같다.
$$y = ax + b$$

그래프를 정확하게 도시하기 위해서는
- 직선의 기울기 $a$
- 직선의 $y$절편 값 $b$
를 정확히 예측해야 한다.

### 최소제곱법(method of least squares)
$$a = \frac{\sum(x - x평균)(y - y평균))} {(x - x평균)^2 의 합}$$

### $y$절편 구하기
$$b = y의 평균 - (x의 평균 * 기울기 a)$$

-----
## 코딩으로 해보기
### 1. `numpy` 임포트
```python
import numpy as np

x = [2, 4, 6, 8]
y = [81, 93, 91, 97]
```

### 2.최소제곱근 공식 적용
|numpy 함수|함수|
|-|-|
|.sum()|합|
|.mean()|평균|

> x의 합과 y의 합
```python
mx = np.mean(x)
my = np.mean(y)
```

> 분모
```python
divisor = sum([(i - mx)**2 for i in x])   ##분자를 divisor라는 변수로 저장
##x의 원소들을 i에 하나씩 대입하여 연산하라는 의미의 for문
```

> 분자
```python
def top(x, mx, y, my):    ##분자를 top함수를 만들어 연산
  d = 0
  for i in range(len(x)):   ##x리스트에 대한 for문 선언
    d += (x[i] - mx) * (y[i] - my)  ##x의 편차와 y의 편차를 곱하여 d에 누적합
  
  return d    ##d 반환
  
dividend = top(x, mx, y, my)  ##dividend 변수에 분자값 저장
```

> a, b값 구하기
```python
a = dividend / divisor
b = my - (mx * a)
```

## 평균 제곱 오차(mean square error, MSE)
일반적으로 오차를 구하는 방식은 다음과 같다.
$$오차 = \frac{예측값}{실제 값}$$

오차는 양의 값과 음의 값이 존재하므로, 각 오차의 값을 제곱한다.

$$오차의 합 = \sum_{i}^n (y_i - \hat{y}_i)^2 $$


