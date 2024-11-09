---
title: Pytorch Deep Learning Example
author: Joonseo Hyeon
layout: post
---

GPT가 작성한 Pytorch 코드의 예시를 통해 딥러닝이 어떻게 이뤄지는지 보자.

```python
import torch
import torch.nn as nn
import torch.optim as optim
from torch.utils.data import DataLoader, TensorDataset

# Define a simple neural network
class SimpleNN(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc1 = nn.Linear(10, 50)
        self.fc2 = nn.Linear(50, 1)

    def forward(self, x):
        x = torch.relu(self.fc1(x))
        x = self.fc2(x)
        return x

# Generate some random data
x_train = torch.randn(100, 10)
y_train = torch.randn(100, 1)
x_test = torch.randn(20, 10)
y_test = torch.randn(20, 1)

# Create DataLoader
train_dataset = TensorDataset(x_train, y_train)
train_loader = DataLoader(train_dataset, batch_size=10, shuffle=True)

# Initialize the model, loss function, and optimizer
model = SimpleNN()
criterion = nn.MSELoss()
optimizer = optim.SGD(model.parameters(), lr=0.01)

# Training loop
for epoch in range(100):
    for inputs, targets in train_loader:
        optimizer.zero_grad()
        outputs = model(inputs)
        loss = criterion(outputs, targets)
        loss.backward()
        optimizer.step()

# Testing
model.eval()
with torch.no_grad():
    test_outputs = model(x_test)
    test_loss = criterion(test_outputs, y_test)
    print(f'Test Loss: {test_loss.item()}')
```

## class SimpleNN(nn.Module)

- pytorch의 nn.Module을 상속받는 자식 클래스이다.
  - nn.Module은 pytorch로 작성된 모든 신경망의 Base Class로 상속받는 것을 권장한다.
  - 때문에 생성자도 상속받으며 forward 함수도 nn.Module의 함수이기 때문에 상속받아 작성된다.

## def __init__(self)

- 훈련을 위한 layer가 속성으로 선언된다.
  - 10개를 입력받고 50개를 출력하는 fc1 layer, 50개를 입력받고 1개를 출력하는 fc2 layer가 선언되어있다.

## def forward(self, x)

- 실질적으로 훈련이 이뤄지는 부분이다.
  - 10차원의 입력을 받고 ReLU 활성화함수를 통과한 후 1개의 값만 내뱉는 단순 신경망이다.

## DataLoader

- DataLoader는 dataset을 batch size만큼 차례로 꺼내주는 역할을 하며 shuffle의 여부도 결정할 수 있다.
  - DataLoader를 위한 dataset 클래스는 __init__, __len__, __getitem__ 함수를 반드시 구현해야 한다.
  - __init__함수는 실제적인 데이터를 불러와야 한다.
  - __len__함수는 데이터셋 전체 갯수를 반환해야 한다.
  - __getitem__함수는 index를 입력받고 index에 해당하는 데이터와 label을 같이 출력한다.

## criterion

- 선언된 함수를 통해 모델의 loss를 평가한다.
  - MSE, L1, CrossEntropy, BCELoss 등

## optimizer

- 선언된 함수로 모델의 파라미터를 업데이트하며 그 수치는 lr(학습률)로 조절한다.

## training

1. train셋의 dataloader에서 데이터에 해당하는 변수 inputs와 라벨에 해당하는 변수 targets를 꺼낸다.
2. optimizer의 gradient를 0으로 초기화한다.
3. inputs에 대한 모델의 outputs를 얻는다.
4. outputs와 targets 간의 loss를 criterion으로 정의된 함수로 계산한다.
5. 역전파할 gradient를 계산한다.
6. optimizer가 모델의 파라미터를 값을 업데이트한다.
7. 1~6의 과정을 전체 데이터에 대해 batch 단위만큼 반복한다.
8. 1~7의 과정을 epoch 수만큼 반복한다.

## torch.no_grad

- optimizer의 gradient를 update하지 않는다고 선언한다.
