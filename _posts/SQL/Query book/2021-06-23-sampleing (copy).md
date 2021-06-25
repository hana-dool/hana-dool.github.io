```
```

title:  "sampling"
excerpt: "샘플링"
categories:

  - SQL_Query_Book
tags:
  - 1
last_modified_at: 2021-06-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true

<br>

# <center><font size="6">랜덤 샘플링</font></center>

- 아래와 같이 실행할 경우, col1 의 값을 맨 뒤에 더 붙일 수 있다. 

```sql
SELECT df.* , col1 
FROM df;
```

![png](/assets/images/SQL/5_1.png)
