# PyTorch 課程筆記

## 基本介紹

- **PyTorch**：由 Facebook 開發的深度學習框架  
- 用於訓練深度神經網路（DNN）

## 資料處理模組

- 載入資料：
  - `torch.utils.data.Dataset`
  - `torch.utils.data.DataLoader`

## 建立模型基本流程

```python
# 定義神經網路、損失函數與最佳化器
import torch.nn as nn
import torch.optim as optim
```

## Tensor 基礎
- 定義：高維度矩陣
- 常見資料型別
  - `torch.float：32-bit 浮點數`
  - `torch.long：64-bit 整數（有號）`

## 建立 Tensor
```
X = torch.tensor([[1, -1], [0, 1]])
X = torch.zeros([2, 2])
X = torch.ones([1, 2, 5])
# ones 和 zeros 的參數是維度大小
```

## Tensor 運算
| 操作            | 說明                |
| ------------- | ----------------- |
| `squeeze()`   | 去除長度為 1 的維度（降維）   |
| `unsqueeze()` | 增加一個長度為 1 的新維度    |
| `transpose()` | 轉置                |
| `cat()`       | 沿指定維度合併張量，其他維度需一致 |
| `pow()`       | 次方運算              |
| `sum()`       | 求總和               |
| `mean()`      | 求平均值              |

## Tensor 屬性
  -.shape：形狀
  -.dtype：資料型別

## 設定裝置（Device）
  - Tensor 或 model 可以被送到 CPU 或 GPU：

```
  X = x.to('cpu')     # 或 'cuda'
```

## 計算 Gradient
```
x = torch.tensor([[1., 0.], [-1., 1.]], requires_grad=True)
z = x.pow(2).sum()
z.backward()
print(x.grad)
#z.backward()：計算 z 對每個變數的偏導，其中對x的微分結果會存在 x.grad 中
```

## 載入資料
```
from torch.utils.data import Dataset, DataLoader

class MyDataset(Dataset):
    def __init__(self, file):
        self.data = ...  # 資料初始化
    def __getitem__(self, index):
        return self.data[index]
    def __len__(self):
        return len(self.data)

dataset = MyDataset(file)
dataloader = DataLoader(dataset, batch_size=batch_size, shuffle=True)
#shuffle=True：訓練時開啟洗牌，測試與驗證時建議關閉
```

## 激活函數（Activation）
```
nn.Sigmoid()
nn.ReLU()
```
##
損失函數（Loss Function）
```
nn.MSELoss()              # 均方誤差
nn.CrossEntropyLoss()     # 適用於多分類問題
```
## 定義模型
  - 使用 nn.Sequential() 按順序定義網路

  - 在 forward() 中傳入資料進行前向傳播

## 最佳化（Optimization）
  - 常用的隨機梯度下降法（SGD）
    - `optimizer = torch.optim.SGD(params, lr=learning_rate, momentum=0)`
    - 需傳入模型參數 params 及學習率 lr


