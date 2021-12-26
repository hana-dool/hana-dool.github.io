---
title: "Tensor Attribute"
excerpt: "Tensor 의 여러속성"
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

# [Tensor Attributes](#link){: .btn .btn--primary}{: .align-center}

- 텐서의 속성은 텐서의 모양(shape), 자료형(datatype) 그리고 어느 장치(device)에 저장되는지 등을 말합니다.

> ## tensor.ndim : 차원 확인

```python
# 텐서의 속성
tensor = torch.rand(11,28)
print(f"Dimension of tensor: {tensor.ndim}") # ndim(차원) 확인
# Dimension of tensor: 2
```

```python
tensor = torch.rand(11,28,22)
tensor.ndim
# 3
```

> ## tensor.shape : 모양 확인

```python
tensor = torch.rand(11,28)
tensor.shape
# torch.Size([11, 28])
```

> ## tensor.dtype : 데이터 타입 확인

- A [`torch.dtype`](https://pytorch.org/docs/stable/tensor_attributes.html#torch.torch.dtype)는 의 데이터 유형을 나타내게 됩니다.

| Data type                                                    | dtype                                 | Legacy Constructors      |
| ------------------------------------------------------------ | ------------------------------------- | ------------------------ |
| 32-bit floating point                                        | `torch.float32` or `torch.float`      | `torch.*.FloatTensor`    |
| 64-bit floating point                                        | `torch.float64` or `torch.double`     | `torch.*.DoubleTensor`   |
| 64-bit complex                                               | `torch.complex64` or `torch.cfloat`   |                          |
| 128-bit complex                                              | `torch.complex128` or `torch.cdouble` |                          |
| 16-bit floating point [1](https://pytorch.org/docs/stable/tensor_attributes.html#id3) | `torch.float16` or `torch.half`       | `torch.*.HalfTensor`     |
| 16-bit floating point [2](https://pytorch.org/docs/stable/tensor_attributes.html#id4) | `torch.bfloat16`                      | `torch.*.BFloat16Tensor` |
| 8-bit integer (unsigned)                                     | `torch.uint8`                         | `torch.*.ByteTensor`     |
| 8-bit integer (signed)                                       | `torch.int8`                          | `torch.*.CharTensor`     |
| 16-bit integer (signed)                                      | `torch.int16` or `torch.short`        | `torch.*.ShortTensor`    |
| 32-bit integer (signed)                                      | `torch.int32` or `torch.int`          | `torch.*.IntTensor`      |
| 64-bit integer (signed)                                      | `torch.int64` or `torch.long`         | `torch.*.LongTensor`     |
| Boolean                                                      | `torch.bool`                          | `torch.*.BoolTensor`     |

- 위와 같이 여러 데이터타입이 존재하는데요, data.dtype 을 출력하게 되면 데이터타입을 출력하게 됩니다.

> ## tensor.device

```python
tensor = torch.rand(11,28)
tensor.device #(cpu / gpu)
# cpu
```

- 위처럼 어떤 device 에 tensor 가 저장되는지를 나타냅니다.

**Reference**

- <https://wikidocs.net/52460>
- <https://tempdev.tistory.com/9>



ing
{: .notice--success}

