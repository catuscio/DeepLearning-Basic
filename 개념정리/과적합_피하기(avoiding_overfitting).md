# 과적합 피하기
## 과적합 Overfitting
https://github.com/catuscio/DeepLearning-Basic/blob/main/colab%20workout/Overfitting_Example_Sonar.ipynb
위의 예시처럼, 모델이 학습 데이터셋 안에서는 일정 수준 이상의 정확도를 보이지만, 새로운 데이터에 적용할 경우 그렇지 않은 경우를 __과적합 Overfitting__ 이라고 한다.

## trainset & testset
데이터셋에 100개의 샘플이 있을 경우, 7:3 비율로 학습셋과 테스트셋을 나눈다.\
학습셋으로 신경망을 학습한 결과를 __모델model__ 이라고 한다.\
이후 테스트셋으로 테스트를 진행하여, 정확도를 평가하는 과정을 거친다.

> 세즈노프스키(Terrence J. Sejnowski) 연구팀에 의하면, 식이 복잡해지고 학습량이 증가할수록 trainset을 이용한 예측률은 그에 비례하여 증가하지만, testset을 이용한 예측률은 오히려 감소한다.

### 코드로 두 셋을 나눠보자.
https://github.com/catuscio/DeepLearning-Basic/blob/main/colab%20workout/Overfitting_Example_Sonar_Train_Test.ipynb
```python
from sklearn.model_selection import train_test_split

X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.3, random_state=seed)
```

### trainset으로 생성된 모델을 저장하고 재사용 해보자
```python
model.save('my_model.h5')  # 모델을 컴퓨터에 저장
```

## k겹 교차 검증(k-fold cross validation)
k겹 교차 검증이란 데이터셋을 여러 개로 나누어 하나씩 테스트셋으로 사용하고 나머지를 모두 합해 학습셋으로 사용하는 방법입니다.
```python
# 10개의 파일로 쪼갬
n_fold = 10
skf = StratifiedKFold(n_splits=n_fold, shuffle=True, random_state=seed)
```

---
# Best Model
https://github.com/catuscio/DeepLearning-Basic/blob/main/colab%20workout/BestModel_Example_Wine.ipynb

## 체크포인트
https://github.com/catuscio/DeepLearning-Basic/blob/main/colab%20workout/BestModel_Example_Wine_Checkpoint.ipynb
```python
from keras.callbacks import ModelCheckpoint

# 모델 저장 조건 설정(체크포인트 설정)
modelpath="./model/{epoch:02d}-{val_loss:.4f}.hdf5"
checkpointer = ModelCheckpoint(filepath=modelpath, monitor='val_loss', verbose=1, save_best_only=True)
```

## 학습 자동 중단
https://github.com/catuscio/DeepLearning-Basic/blob/main/colab%20workout/BestModel_Example_Wine_Early_Stop.ipynb

```python
from keras.callbacks import EarlyStopping

# 자동 중단 설정
early_stopping_callback = EarlyStopping(monitor='val_loss', patience=100)
```

