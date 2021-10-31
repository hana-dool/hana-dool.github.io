---
title:  "Folder manipulation"
excerpt: "폴더 및 파일 생성, 이름 바꾸기 "
categories:
  - Py_Advanced
last_modified_at: 2021-10-25

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"

use_math : true
---

 os 모듈을 활용하여 폴더를 생성하고, 파일을 만드는 법을 알아봅시다.
{: .notice--warning}

# [os packages](#link){: .btn .btn--primary}{: .align-center}

> ## 폴더 생성하기

- 아래는, 지정된 directory 에 폴더를 생성하는 custom 함수입니다.

```python
import os
 
def createFolder(directory):
    try:
        if not os.path.exists(directory):
            os.makedirs(directory)
    except OSError:
        print ('Error: Creating directory. ' +  directory)
createFolder('./Test/rest')
```

**reference**

- <https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=wideeyed&logNo=221653260516>
- <https://ybworld.tistory.com/116>

