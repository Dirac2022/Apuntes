
# Introduction to Deep Learning with PyTorch


## Introduction to PyTorch

**PyTorch**
- Originally developed by Meta AI, now part of Linux Foundation
- The fundamental data structure in PyTorch is a tensor.

**Importing PyTorch**

```python
import torch
```


### PyTorch tensors

- Similar to array or matrix
- Building block of neural networks

```python
import torch
my_list = [[1, 2, 3], [4, 5, 6]]
tensor = torch.tensor(my_list)
print(tensor)
```

<h5>Tensor attributes</h5>

- `shape` : `torch.Size([2, 3])`
- `dtype` : `torch.int64`

<h5>Tensor operations</h5>
```python
a = torch.tensor([[1, 1], [2, 2]])
b = torch.tensor([[2, 2], [3, 3]])
```

For **addition** and **subtraction** tensor must have same shape

```python
print(a + b)
# tensor([[3, 3], 
#         [5, 5]])
```


**Element-wise multiplications**

```python
print(a * b)
# tensor([[2, 2], 
#         [6, 6]])
```


**Matrix multiplication**

```python
print(a @ b)
# tensor([[5, 5], 
#         [10, 10]])
```



### Designing a neural network


```python
import torch.nn as nn

# Input tensor with three features
input_tensor = torch.tensor([[0.3471, 0.4547, -0.2356]])

# Define out linear layer
linear_layer = nn.Linear
```

- Input neurons: features
- Output neurons: clases




## Neural Network Architecture and Hyperparameters



## Training a Neural Network with PyTorch



## Evaluation and Improving Models

