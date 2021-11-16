---
title:  "os"
excerpt: "파이썬 os 패키지 기초"
categories:
  - Module_Others
last_modified_at: 2021-10-25

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"

use_math : true
---

 os 모듈에 대ㅐ서 자세히 알아봅시다.
{: .notice--warning}

# [os packages](#link){: .btn .btn--primary}{: .align-center}

> ## os.getcwd() : 현재 작업 디렉토리 확인

- 현재 제가 실행하고 있는 파일의 위치 / 경로를 반환합니다.

```python
os.getcwd()
```



```
'C:\\Users\\goran\\Desktop\\Bayesian-with-Python-master\\Bayesian-with-Python-master\\Chap02-MorePyMC'
```

> ## os.listdir('.') : 현재 파일 경로에 있는 dir 리스트

- 현재 파일 경로에 있는 디렉토리들의 리스트를 모두 출력합니다.

```python
os.listdir('.')
```

```
['.ipynb_checkpoints', 'Chap02-MorePyMC.ipynb', 'data', 'separation_plot.py']
```

> ## os.mkdir : 현재 경로에 dir 생성

- 현재 저희가 있는 경로에, 폴더(dir) 를 생성합니다.

```python
os.mkdir('test')
```

- 위와 같이 실행할 경우, 같은 위치에 폴더가 형성됩니다.

```python
os.mkdir("C:/Users/User/Desktop/test")
```

- 하지만 이미 있는 디렉토리 명일떄에는 에러가 발생합니다.

> ## os.makedirs() : 모든 하위 폴더 생성

- os.mkdir() 은 경로의 제일 마지막에 적힌 폴더 하나만 생성합니다.
- 하지만 그에 반해서 os.makedirs() 함수는 경로의 모든 폴더를 만들어냅니다.

```python
os.makedirs("C:/Users/User/Desktop/test/a/b")
```

- 실제로 확인해보면, `C:/Users/User/Desktop/test/a/b`이 생겨있습니다.

> ## os.remove() : 파일 삭제 

```python
os.remove("C:/Users/User/Desktop/tes1t/a/b/test.txt")
```

- 위처럼 remove 를 통하여 존재하는 파일을 삭제할 수 있습니다. 

> ## os.chdir() : 작업 디렉토리 변경

- 현재 작업 디렉토리를 변경합니다.

```python
os.chdir("D:/")
os.getcwd() #'D:\\'
```

# [os.path](#link){: .btn .btn--primary}{: .align-center}

> ## os.path.exists() : 파일/폴더의 존재여부 판단

- 파일의 유무를 판단하게 해 줍니다. 

```python
os.path.exists("C:/Users/User/Desktop/test/test.txt")
```

- 파일/폴더가 존재하면 True, 그렇지 않으면 False 를 반환합니다.

> ## os.path.getsize() : 파일의 크기(size) 반환

- 파일의 크기를 반환합니다.

```python
os.path.getsize("C:/Users/User/Desktop/test/test.txt")
```

```
856
```

- 단위는 바이트 입니다. 

> ## os.path.dirname(), os.path.basename()

- dirname() 함수는 입력 경로의 폴더 경로까지 꺼냅니다.
- basename() 함수는 파일 이름만 꺼내줍니다. 

```python
os.path.dirname("C:/Users/User/Desktop/test/test.txt")
```

```
'C:/Users/User/Desktop/test'
```

```python
os.path.basename("C:/Users/User/Desktop/test/test.txt")
```

```
'test.txt'
```

**reference**

- <https://yganalyst.github.io/data_handling/memo_1/>

