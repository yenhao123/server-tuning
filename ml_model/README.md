# ML Pipeline


## 1. Collecting Data

Performance data was collected by running a workload over time while recording system metrics using a profiling tool.

- **Raw Output Shape**: `(61, 103)` → 61 time intervals × 103 performance counters  
- **Performance Counter Types**:
  - **Cache** (e.g., Copy Reads/sec) – file system cache, not CPU cache
  - **Memory** (e.g., Available Bytes, Page Faults/sec, Transition Pages RePurposed)
  - **Logical Disk (D:/)** (e.g., Disk Transfers/sec)
  - **Physical Disk** (e.g., Disk Transfers/sec)  
    *Note: Physical disk data is identical to logical disk due to RAID controller abstraction.*
  - **Process** (e.g., Processor Time, Thread Count)

---

## 2. Preprocessing Data

- **Missing Values**: Filled with 0  
- **Feature Selection**: Irrelevant features removed using CART  
  - Feature count reduced: `156 → 103`

---

## 3. Model Training

A fully connected neural network was used for classification.

- **Parameter Count**: ~1400M  
- **Model Size**: ~53MB  
- **Loss Function**: `CrossEntropyLoss`  
- **Optimizer**: `Adam`  
```python
import torch
import torch.nn as nn

class Classifier(nn.Module):
    def __init__(self):
        super(Classifier, self).__init__()
        self.layer1 = nn.Linear(N_SAMPLES * N_COUNTERS, 2048)
        self.layer2 = nn.Linear(2048, 512)
        self.layer3 = nn.Linear(512, 128)
        self.out = nn.Linear(128, N_CLASSES)
        self.act_fn = nn.LeakyReLU()

    def forward(self, x):
        x = torch.flatten(x, start_dim=1)
        x = self.act_fn(self.layer1(x))
        x = self.act_fn(self.layer2(x))
        x = self.act_fn(self.layer3(x))
        return self.out(x)
```

## 4. Model Testing & Rejecting

如需我補上 testing 的 metrics（如 accuracy、confusion matrix、reject mechanism），請告訴我！


OpenMax

## 5. Options Tuning
Based on the predicted class, corresponding options are applied to improve performance.

## 6. Results
The proposed method improves task performance by an average of 1.43× across tested workloads.
![alt text](../images/image.png)
