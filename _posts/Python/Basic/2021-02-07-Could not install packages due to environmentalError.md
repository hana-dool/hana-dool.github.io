---
title:  "패키지 인스톨 에러"
excerpt: "Could not install packages due to Environmental Error"
categories:
  - Py_Basic
tags:
  - Error
last_modified_at: 2021-02-08

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# 에러

- packages 를 pip install 로 깔더라도 위와 같이 나타나는 경우가 있다.

![png](/assets/images/{Error}/1.png)

- 위 그림처럼 패키지가 그 위치에 없다고 해서 에러가 난다.

# 대처1

- pip install 이나 conda install 을 시도하여 해당 패키지를 업데이트 한다.

- 하지만 이런식으로 설치를 해도 에러가 나는 경우가 있다.

  ![png](/assets/images/{Error}/2.PNG)

- 위와 같이 pytz 의 패키지가 없다고 에러가 나서 install 을 시도하였으나 에러가 난 경우이다.

- 그래서 install 이 안되어서 그런가 하고 해당 위치로 이동해 보았다.

  ![png](/assets/images/{Error}/3.PNG)

- 자꾸 없다고 하는데, 위처럼 이미 존재 하는데에도 에러가 났던 것이였다.

- 혹시 버전이 달라서 그런가 싶어서 pip install == 20.1 버전으로 설치해도 똑같은 에러가 날 뿐이였다.

# 대처2

- 결국 다른 env 에서 해당 파일을 직접 가져와서 해결했다.

  ![png](/assets/images/{Error}/4.PNG)

- 다른 env에서는 pip install 이 잘 먹혔고, 그에 따라 정상적인 파일이 설치가 되었다.

- 그래서 위 파일을 복사한 후, env -> 문제가 된 가상환경 -> Lib -> site-packages 에 업로드 하였다.

  ![png](/assets/images/{Error}/5.PNG)

- 그 이후에야 위처럼 원하는 패키지가 의존성 env 문제 없이 설치가 되었다.