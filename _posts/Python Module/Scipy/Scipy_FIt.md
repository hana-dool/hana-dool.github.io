---
title: "" 
excerpt: "Tensor 를 자유자재로 다루어보기"
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

 텐서의 연산에 대해서 알아봅시다.
{: .notice--warning}

# [Tensor Manipulation](#link){: .btn .btn--primary}{: .align-center}

> ## 행렬 곱셈과, 곱셈

- 메인 Namespace 입니다. 다양한 수학 함수가 포함되어 있으며 Numpy 와 유사한 행동을 합니다. 

> 행렬 곱셈

```python
m1 = torch.FloatTensor([[1, 2],
                        [3, 4]])
m2 = torch.FloatTensor([[1],
                        [2]])
print(m1.matmul(m2)) # m1@m2 도 같습니다.
#tensor([[ 5.],
#        [11.]])
```

- 위와 같이 m1 과 m2 를 행렬곱한 결과를 `m1@m2` 와 같은 형태로 나타낼 수 있습니다.

> 내적 곱

```python
m1 = torch.FloatTensor([[1, 2],
                        [3, 4]])
m2 = torch.FloatTensor([[1],
                        [2]])
print(m1 * m2) 
#tensor([[1., 2.],
#        [6., 8.]])

```

- 하지만 위와 같은 작업을 그냥 곱셈을 이용해서 하게된다면, 위와 같이 브로드캐스팅 된 이후의 곱셈으로 계산됩니다. 

> ## 평균 

```python
t = torch.FloatTensor([1, 2])
print(t.mean())
# tensor(1.5000)
```

- 위와 같이 1차원 Tensor 인 경우 mean 메서드를 실행하면 평균을 출력합니다.

```python
t = torch.FloatTensor([[1, 2], [3, 4]])
print(t.mean())
# tensor(2.5000)
```

- 위와 같이 2차원 이상의 경우에도 아무 인자없이 mean 을 그대로 실행하면 전체의 평균이 나오게 됩니다. 

```python
print(t.mean(dim=0))
# tensor([2., 3.])
print(t.mean(dim=1))
# tensor([1.5000, 3.5000])
```

- 위와 같이 mean 에 dim 인자를 주어서 '해당 차원의 입장에서' 평균을 보겠다는 의미가 됩니다.
  - dim = 0 이면 첫번쨰 차원(행) 을 제거하면서 mean 을 보게 됩니다. 즉 행이 제거된(행을 기준으로 평균).
  - dim = 2 이면 두번쨰 차원을 제거하면서 mean 을 보게 됩니다. 즉 열이 제거된 (열을 기준으로 평균)

```python
print(t.mean(dim=-1))
tensor([1.5000, 3.5000])
```

- 위는 마지막 차원을 제거하면서 평균을 본다는 의미입니다. 

> ## 최소, 최대 

- 최대나, 최나 결국엔
- 최대는 기본적으로 원소의 최댓값을 Return 합니다. 
- Argmax 는 최댓값을 가지는 인덱스를 Return 하게 됩니다. 

```python
t = torch.FloatTensor([[1, 2], [3, 4]])
print(t.max())
# tensor(4.)
```

- 위와 같이 max 메서드를 그냥 사용하게 된다면 Tensor 내에서 최댓값을 그대로 출력하게 됩니다. 

```python
print(t.max(dim=0))
#torch.return_types.max(
#values =tensor([3.,4.]),
#indices=tensor([1, 1]))
```

- max 를 지정한 뒤에 위처럼 dimension 을 지정하게 되면
  - dim 에 지정한 차원을 제거하면서 max 를 봅니다. 
  - 또한 argmax 를 출력합니다.
    - max index 는 각각 열 기준으로 1 번 index 이기 떄문에 (1,1) 을 출력합니다.

> ## 뷰(View)

- 원소의 수를 유지하면서 텐서의 크기를 변경합니다.
- Pytorch 의 뷰는 넘파이에서의 Reshape 와 같은 역할을 합니다. 

```python
t = np.array([[[0, 1, 2],
               [3, 4, 5]],
              [[6, 7, 8],
               [9, 10, 11]]])
ft = torch.FloatTensor(t)
```

- 위와 같이 2,2,3 의 shape 를 가지는 tensor 를 만들어보았습니다.

> 3차원 텐서 -> 2차원 텐서

```python
print(ft.view([-1, 3])) # ft라는 텐서를 (?, 3)의 크기로 변경
print(ft.view([-1, 3]).shape)
#tensor([[ 0.,  1.,  2.],
#        [ 3.,  4.,  5.],
#        [ 6.,  7.,  8.],
#        [ 9., 10., 11.]])
#torch.Size([4, 3])
```

- 위와 같이 view 를 통해서 reshape 를 적용하면 그 크기가 변하게 됩니다. 
  - -1 은 사용자가 잘 모르겠는 경우에 나타냅니다.
  - 2,2,3 -> ?,3 으로 바뀌려면 ? 은 4가 되어야 합니다. 

> 3차원 텐서 -> 3차원 텐서 

```python
print(ft.view([-1, 1, 3]))
print(ft.view([-1, 1, 3]).shape)
#tensor([[[ 0.,  1.,  2.]],
#        [[ 3.,  4.,  5.]],
#        [[ 6.,  7.,  8.]],
#        [[ 9., 10., 11.]]])
#torch.Size([4, 1, 3])
```

> ## Squeeze 

- 1인 차원을 제거하는 방법입니다. 

```python
ft = torch.FloatTensor([[0], [1], [2]])
print(ft)
#tensor([[0.],
#        [1.],
#        [2.]])
print(ft.shape)
#torch.Size([3, 1])
```

- 위의 텐서는 (3,1) 의 크기를 가집니다. 
- 두번째 차원이 1 이므로, squeeze 를 사용하면 (3,) 의 크기를 가지는 텐서로 변경을 할 수 있습니다.

```python
print(ft.squeeze())
#tensor([0., 1., 2.])
print(ft.squeeze().shape)
# torch.Size([3])
```

> ## Unsqueeze

- 특정 위치에 1인 차원을 추가합니다. 
- Squeeze 와 정반대입니다. 

```python
ft = torch.Tensor([0, 1, 2])
print(ft.shape)
# torch.Size([3])
```

- 이제 위에서, 첫번째 차원에 1을 추가해보겠습니다.

```python
print(ft.unsqueeze(0)) # 인덱스가 0부터 시작하므로 0은 첫번째 차원을 의미
#tensor([[0., 1., 2.]])
print(ft.unsqueeze(0).shape)
#torch.Size([1, 3])
```

- 이번에는 두번째 차원에 1을 추가해보겠습니다. 

```python
print(ft.unsqueeze(1)) # 인덱스가 0부터 시작하므로 0은 첫번째 차원을 의미
#tensor([[0., 1., 2.]])
print(ft.unsqueeze(1).shape)
#torch.Size([1, 3])
```

> Note : 위와 같은 작업을 View 을 이용하여 할 수도 있습니다.

```python
print(ft.view(1, -1))
#tensor([[0., 1., 2.]])
print(ft.view(-1, 1))
#tensor([[0.],
#        [1.],
#        [2.]])
```

- 그리고, unsqueeze 를 마지막 차원에 대해서 적용하고 싶다면 -1 을 적용하면 됩니다.

```python
print(ft.unsqueeze(-1))
#tensor([[0.],
#        [1.],
#        [2.]])
print(ft.unsqueeze(-1).shape)
#torch.Size([3, 1])
```

> ## Type Casting

- 텐서플로에도 자료형이 있습니다.
  - 32비트의 부동 소수점은 torch.FloatTensor
  - 64비트의 부호 있는 정수는 torch.LongTensor를 사용
  - GPU 연산을 위한 자료형도 있습니다. 예를 들어 torch.cuda.FloatTensor가 그 예입니다.

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

```python
lt = torch.LongTensor([1, 2, 3, 4])
print(lt)
# tensor([1, 2, 3, 4])
```

- 위와 같이 LongTensor (int 자료형을 가지는 Tensor) 을 정의하였기 떄문에 1,2,3,4 로 정수 자료형이 나오는것을 볼 수 있습니다.

```python
print(lt.float())
# tensor([1., 2., 3., 4.])
```

- 위와 같이 float() 을 붙여주면 바로 float 형으로 타입이 변경됩니다.

> ## Concatenate

```python
x = torch.FloatTensor([[1, 2], [3, 4]])
y = torch.FloatTensor([[5, 6], [7, 8]])
```

- 두 텐서를 연결하는법을 알아보겠습니다.
- 사실 연결 방법도 Numpy 의 concat 과 동일합니다.

```python
print(torch.cat([x, y], dim=0))
#tensor([[1., 2.],
#        [3., 4.],
#        [5., 6.],
#        [7., 8.]])
```

- 위의 경우는 dim = 0 을 기준으로 붙이는 방법입니다. 

```python
print(torch.cat([x, y], dim=1))
#tensor([[1., 2., 5., 6.],
#        [3., 4., 7., 8.]])
```

> ## Stacking

- 스태킹은 Concat 의 다른 방법입니다. 

```python
x = torch.FloatTensor([1, 4])
y = torch.FloatTensor([2, 5])
z = torch.FloatTensor([3, 6])
```

```python
print(torch.stack([x, y, z]))
#tensor([[1., 4.],
#        [2., 5.],
#        [3., 6.]])
```

- 위의 결과는 3개의 벡터가 순차적으로 쌓여 만들어진것입니다. 
  - 위와 같은 결과를 concat 을 이용해 작업하려면 어떻게 해야할까요?

```python
print(torch.cat([x.unsqueeze(0), y.unsqueeze(0), z.unsqueeze(0)], dim=0))
#tensor([[1., 4.],
#        [2., 5.],
#        [3., 6.]])
```

- x, y, z는 기존에는 전부 (2,)의 크기를 가졌습니다. 그러므로 2차원의 값을 concat 으로 수행하려면 concat 하는 값 또한 2차원으로 만들어야 합니다.
  - 그러므로 .unsqueeze(0)을 하므로서 3개의 벡터는 전부 (1, 2)의 크기의 2차원 텐서로 변경됩니다. 
  - 여기에 연결(concatenate)를 의미하는 cat을 사용하면 (3 x 2) 텐서가 됩니다.

> ## Zero , One tensor

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

- 위와 같이, x 와 동일한 크기를 가지는 1, 0 tensor 를 만들어낼 수 있습니다.

**Reference**

- <https://wikidocs.net/52460>

ing
{: .notice--success}

