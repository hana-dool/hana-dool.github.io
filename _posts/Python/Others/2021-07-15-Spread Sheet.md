---
title:  "Google Spread Sheet 연동"
excerpt: "스프레드시트 연동하기"
categories:
  - Py_Others
tags:
  - 1
last_modified_at: 2021-07-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

<br>

ref : <https://hyeshinoh.github.io/2020/04/18/python_18_pygsheets/>

# 1. gspread VS pygsheets?

![png](/assets/images/Python/12_1.png)

- <https://maxpearl.us/gspread-vs-pygsheets.html>

- Google spread sheet 를 연동하기 위해 찾다보면, 위와 같이 2개의 모듈이 있음을 알 수 있따.
- 그 중에서 하나를 선택하자면 위 아티클에서와 같은 이유로 , pygsheet 를 추천한다. 

<br>

# 2. Install

```python
pip install gspread
pip install --upgrade oauth2client
```

- 위 두 명령어를 통해 필요한 패키지를 인스톨하자. 
  - gspread : 구글 Spread Sheet 를 다루기 위해 필요한 도구 
  - OAuth2 : open API 를 제공하는 서비스에서 인증을 위해 사용하는 도구

<br>

# 3. Google Set up 

![png](/assets/images/Python/12_2.png)

- 위와 같이 프로젝트를 만든다. 
  - 왼쪽 상단메뉴에서 IAM 및 관리자 -> 프로젝트 만들기 로 만들어도 상관없다.
- 프로젝트의 이름은 상관 없습니다.

![png](/assets/images/Python/12_3.png)

![png](/assets/images/Python/12_4.png)

- 그 이후엔 위와 같이, 라이브러리를 들어간 이후에 Drive API , Google Sheets API 를 설치합니다. 

![png](/assets/images/Python/12_5.png)

- 위와 같이 사용자 인증 정보를 만듭니다. 

![png](/assets/images/Python/12_8.png)

![png](/assets/images/Python/12_9.png)

![png](/assets/images/Python/12_10.png)

![png](/assets/images/Python/12_11.png)

- 만든 이후에는 위와 같이 동의화면을 구성합니다. 

![png](/assets/images/Python/12_12.png)

- 사용자 인증정보를 위와 같이 만듭니다. 

![png](/assets/images/Python/12_13.png)

- 그 이후 Oauth 클라이언트를 다운받습니다.

![png](/assets/images/Python/12_14.png)

- 마지막으로는, 앱이 테스트 상태이므로, 테스트 사용자를 제 이메일로 넣습니다. 
- 여기에 넣은 사용자만 사용이 가능합니다. 

<br>

# 4. IPYNB 에서 사용

![png](/assets/images/Python/12_16.png)

- 위와 같이, 다운받은 Oauth 클라이언트 이름을 client_secret.json 으로 바꿉니다.(이름은 사실 상관없음)
- 그 이후, 같은 공간에 ipynb 를 생성합니다. 

![png](/assets/images/Python/12_15.png)

- 위와 같이, 클라이언트를 실행하고, 주소로 가서 로그인 후 인증받으면 됩니다. 

<br>

# 5. 시트 가져오고 수정하기

> 읽어오기

```python
sh = gc.open('data')
```

- drive 경로에 있는 data 시트를 읽어옵니다. 
- 처음에는 항상 시트 1 을 가져옵니다. 

> 시트 생성하기 

```python
sheet2 = sh.add_worksheet("new_sheet", rows=20, cols=5)
```

- 현재 읽어들인 data 스프레시트에 새로운 시트 "new_sheet" 를 생성할 수 있습니다. 

> 시트 선택하기

```python
# 모든 시트 리스트로 가져오기
sheet_list = sh.worksheets()
sheet_list
```

```python
# 시트 제목으로 가져오기
new_sheet = sh.worksheet_by_title("new_sheet")
print(new_sheet)
```

```python
# index로 시트 가져오기
sheet0 = sh.worksheet("index", 0)
print(sheet0)
```

<br>

# 5. 데이터 가져오기

> 모든 값 가져오기 

```python
# 모든 records(row) 불러오기 - 딕셔너리 타입: 첫 행이 key가 됨
sheet1.get_all_records()
```

```python
>>> output
[{'name': 'Paul', 'email': 'paul@naver.com', 'phone': '010-1111-1111'},
 {'name': 'Jennie', 'email': 'jennie@daum.net', 'phone': '010-1234-5678'},
 {'name': 'Chloe', 'email': 'chloe@gmail.com', 'phone': '010-9999-9999'}]
```

> 모든 데이터를 행렬(리스트 타입) 으로 가져오기 

```python
# 모든 데이터 행렬로 가져오기 (리스트 타입) - 설정된 rows, cols 수 전체에 대해 가져옴
all_data_sheet1 = sheet1.get_all_values(returnas='matrix')
all_data_sheet1
```

```python
>>> output
[['name', 'email', 'phone'],
 ['Paul', 'paul@naver.com', '010-1111-1111'],
 ['Jennie', 'jennie@daum.net', '010-1234-5678'],
 ['Chloe', 'chloe@gmail.com', '010-9999-9999'],
 ['', '', ''],
 ['', '', ''],
 ['', '', '']]
```



> 위치를 특정하여 행렬 상태로 데이터 가져오기

```python
# 위치를 지정하여 행렬 형태로 데이터 가져오기
some_data_sheet1 = sheet1.get_values(start=(1,1), end=(4,3), returnas='matrix')
some_data_sheet1
```

```python
>>> output 
[['name', 'email', 'phone'],
 ['Paul', 'paul@naver.com', '010-1111-1111'],
 ['Jennie', 'jennie@daum.net', '010-1234-5678'],
 ['Chloe', 'chloe@gmail.com', '010-9999-9999']]
```

<br>

# 6. 데이터 수정 및 삽입



# 7. Pandas Dataframe 

- 사실 pandas 에서 작업하는게 제일로 편하다.
- 이를 위해서라면 get_as_df 함수를 쓰면 된다. 

- https://hyeshinoh.github.io/2020/04/18/python_18_pygsheets/
