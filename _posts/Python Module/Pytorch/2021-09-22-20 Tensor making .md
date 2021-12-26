---
title: "Making Tensor" 
excerpt: "여러 Tensor 만들어보기"
categories:
  - Py_Pytorch
date : 2021-09-22 16:00:00 +0900
last_modified_at: 2021-09-24

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 텐서의 기본
{: .notice--warning}

# [Making Tensor](#link){: .btn .btn--primary}{: .align-center}

- Tensor는 Pytorch의 자료형입니다.
- Tensor는 단일 데이터 타입으로 된 자료들의 다차원 행렬입니다.
- Tensor는 간단한 명령어를 통해서 GPU로 연산을 수행하게 만들 수 있습니다.
  - Tensor 변수 뒤에 .cuda()를 추가하면 하면 됩니다.

- 이때 텐서의 자료형은 여러가지가 있습니다.

> ## Tensor

- 입력받은 데이터로 텐서를 만듭니다. 이때 값은 복사됩니다.

```python
data = np.array([1,2,3,4,5,6])
t = torch.tensor(data)
print(t,t.dtype)
```

```
tensor([1, 2, 3, 4, 5, 6]) torch.int64
```

```python
t = torch.tensor(data,dtype=torch.float32)
print(t,t.dtype)
```

```
tensor([1., 2., 3., 4., 5., 6.]) torch.float32
```

> Note : tensor 로 바꾸면 기존의 데이터는 영향받지 않음

```python
t = torch.tensor(data)
t[0] = 999
print("Tensor values : ",t,"\nOriginal np array values : ",data)
```

- 위와 같이 data 를 통해서 tensor 로 바꾼 이후에, tensor 에게 영향을 가하면 data 는 바뀌지 않습니다.

> ## FloatTensor, IntTensor, ... etc

- Tensor 는 여러가지 Tensor 형태가 존재합니다.

| Data type                                                    | dtype                                 | CPU tensor             | GPU tensor                  |
| ------------------------------------------------------------ | ------------------------------------- | ---------------------- | --------------------------- |
| 32-bit floating point                                        | `torch.float32` or `torch.float`      | `torch.FloatTensor`    | `torch.cuda.FloatTensor`    |
| 64-bit floating point                                        | `torch.float64` or `torch.double`     | `torch.DoubleTensor`   | `torch.cuda.DoubleTensor`   |
| 16-bit floating point [1](https://pytorch.org/docs/stable/tensors.html#id4) | `torch.float16` or `torch.half`       | `torch.HalfTensor`     | `torch.cuda.HalfTensor`     |
| 16-bit floating point [2](https://pytorch.org/docs/stable/tensors.html#id5) | `torch.bfloat16`                      | `torch.BFloat16Tensor` | `torch.cuda.BFloat16Tensor` |
| 32-bit complex                                               | `torch.complex32`                     |                        |                             |
| 64-bit complex                                               | `torch.complex64`                     |                        |                             |
| 128-bit complex                                              | `torch.complex128` or `torch.cdouble` |                        |                             |
| 8-bit integer (unsigned)                                     | `torch.uint8`                         | `torch.ByteTensor`     | `torch.cuda.ByteTensor`     |
| 8-bit integer (signed)                                       | `torch.int8`                          | `torch.CharTensor`     | `torch.cuda.CharTensor`     |
| 16-bit integer (signed)                                      | `torch.int16` or `torch.short`        | `torch.ShortTensor`    | `torch.cuda.ShortTensor`    |
| 32-bit integer (signed)                                      | `torch.int32` or `torch.int`          | `torch.IntTensor`      | `torch.cuda.IntTensor`      |
| 64-bit integer (signed)                                      | `torch.int64` or `torch.long`         | `torch.LongTensor`     | `torch.cuda.LongTensor`     |
| Boolean                                                      | `torch.bool`                          | `torch.BoolTensor`     | `torch.cuda.BoolTensor`     |
| quantized 8-bit integer (unsigned)                           | `torch.quint8`                        | `torch.ByteTensor`     | /                           |
| quantized 8-bit integer (signed)                             | `torch.qint8`                         | `torch.CharTensor`     | /                           |
| quantized 32-bit integer (signed)                            | `torch.qfint32`                       | `torch.IntTensor`      | /                           |
| quantized 4-bit integer (unsigned) [3](https://pytorch.org/docs/stable/tensors.html#id6) | `torch.quint4x2`                      | `torch.ByteTensor`     | /                           |

- tensor처럼 데이터를 복사하여, 지정된 텐서형태를 출력하게 됩니다.

```python
data = np.array([0,1,2,3,4,5])
torch.FloatTensor(data)
# tensor([0., 1., 2., 3., 4., 5.])
```

```python
torch.IntTensor(data)
# tensor([0, 1, 2, 3, 4, 5], dtype=torch.int32)
```

> ## As_tensor

- 입력받은 데이터로 텐서를 만든다는 점에선 tensor와 같습니다.
- 그러나 As_tensor 를 쓰게 될 경우에, 원본과 만들어진 텐서가 같은 cpu상에서 동작할 경우 원본의 값을 복사하지 않고 참조하게 됩니다.
  - 즉 텐서의 값을 바꾸면 원본 데이터의 값도 변하게 됩니다.
  - 또한 이 원본 데이터를 참조하고 있는 모든 텐서의 값도 변한다.

```python
data = np.array([1,2,3,4,5,6])
t = torch.as_tensor(data)
print(t)
# tensor([1, 2, 3, 4, 5, 6])
```

```python
t[0] = 999
print("Tensor values : ",t,"\nOriginal np array values : ",data)
# Tensor values :  tensor([999,   2,   3,   4,   5,   6]) 
# Original np array values :  [999   2   3   4   5   6]
```

- 위처럼 t (as_tensor 데이터 형태) 를 바꾸었을뿐인데 , 원본 데이터 (data) 도 영향을 받았습니다.

````python
data = np.arange(5)
print(data) 
# [0 1 2 3 4]

t1 = torch.as_tensor(data)
t2 = torch.as_tensor(data)
print("t1 : ",t1)
print("t2 : ",t2)
# t1 :  tensor([0, 1, 2, 3, 4])
# t2 :  tensor([0, 1, 2, 3, 4])

t2[0] = 999
print("original np data : ",data)
print("t1 : ",t1)
print("t2 : ",t2)
# original np data :  [999   1   2   3   4]
# t1 :  tensor([999,   1,   2,   3,   4])
# t2 :  tensor([999,   1,   2,   3,   4])
````

- 위와 같이 '같은 데이터' 를 참조하고 있다면 , 하나를 변환하게 되면 모든게 변화게 됩니다.

> ## Zero , Ones : 주어진 크기의 0,1 텐서

> Zeros

```python
torch.zeros(5)
# tensor([0., 0., 0., 0., 0.])
```

```python
torch.zeros((2,3))
#tensor([[0., 0., 0.],
#        [0., 0., 0.]])
```

> Ones

```python
torch.ones(5)
# tensor([1., 1., 1., 1., 1.])
```

```python
torch.ones(2,4)
# tensor([[1., 1., 1., 1.],
#         [1., 1., 1., 1.]])
```

```python
torch.ones((2,3))
# tensor([[1., 1., 1.],
#         [1., 1., 1.]])
```

```python
torch.ones(3,dtype=torch.bool)
# tensor([True, True, True])
```

> ## _like : 동일한 크기의 값 텐서

```python
x = torch.FloatTensor([[0, 1, 2], [2, 1, 0]])
print(x)
#tensor([[0., 1., 2.],
#        [2., 1., 0.]])
```

```python
print(torch.ones_like(x)) # 입력 텐서와 크기를 동일하게 하면서 값을 1로 채우기
#tensor([[1., 1., 1.],
#        [1., 1., 1.]])
```

```python
print(torch.zeros_like(x)) # 입력 텐서와 크기를 동일하게 하면서 값을 0으로 채우기
#tensor([[0., 0., 0.],
#        [0., 0., 0.]])
```

```python
torch.empty_like(x)
# tensor([[0.0000e+00, 5.1380e+31, 7.0295e+28],
#         [6.1949e-04, 7.5556e+28, 5.2839e-11]])
```

```python
torch.full_like(x,2.717)
# tensor([[2.7170, 2.7170, 2.7170],
#         [2.7170, 2.7170, 2.7170]])
```

- 위와 같이, x 와 동일한 크기를 가지는 1, 0 tensor 를 만들어낼 수 있습니다.

> ## empty : 아무값 가지는 텐서

- 주어진 크기의 아무값으로도 초기화되지 않은 텐서를 만든다. 텐서 성분의 값들은 의미없는 아무값입니다.

```python
torch.empty(4)
# tensor([ 1.6751e-37, -1.9427e-13,  1.6751e-37, -1.9427e-13])
```

```python
torch.empty((4,5))
#tensor([[0.0000e+00, 0.0000e+00, 0.0000e+00, 0.0000e+00, 0.0000e+00],
#        [0.0000e+00, 0.0000e+00, 0.0000e+00, 1.4013e-45, 0.0000e+00],
#        [0.0000e+00, 0.0000e+00, 0.0000e+00, 0.0000e+00, 0.0000e+00],
#        [0.0000e+00, 0.0000e+00, 0.0000e+00, 0.0000e+00, 0.0000e+00]])
```

```python
torch.empty(2,3)
#tensor([[4.1102e+08, 4.5579e-41, 2.7585e-36],
#        [0.0000e+00, 2.7548e-36, 0.0000e+00]])
```

```python
torch.empty(2,3,dtype=torch.int)
#tensor([[1304689952,      32526,   74107072],
#        [         0,         32,          0]], dtype=torch.int32)
```

> ## arange : 지정된 차이의 범위를 가지는 list 텐서

```python
torch.arange(5)
# tensor([0, 1, 2, 3, 4])
```

```python
torch.arange(1,4,2)
# tensor([1, 3])
```

```python
torch.arange(3,4,0.2)
# tensor([3.0000, 3.2000, 3.4000, 3.6000, 3.8000])
```

> ## linspace : 지정된 범위의 k 개 list 텐서

```python
torch.linspace(0,10,20)
# tensor([ 0.0000,  0.5263,  1.0526,  1.5789,  2.1053,  2.6316,  3.1579,  3.6842,
#          4.2105,  4.7368,  5.2632,  5.7895,  6.3158,  6.8421,  7.3684,  7.8947,
#          8.4211,  8.9474,  9.4737, 10.0000])
```

# [Making Tensor](#link){: .btn .btn--primary}{: .align-center}

**Reference**

- <https://wikidocs.net/52460>
- <https://tempdev.tistory.com/9>



ing
{: .notice--success}

