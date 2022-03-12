---
title:  "image 실습(~ing)"
excerpt: "실습해보기"
categories:
  - docker
last_modified_at: 2021-11-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 이제! 컨테이너를 실행하고 이를 한번 이용해봅시다.
{: .notice--warning}

# [Install](#link){: .btn .btn--primary}{: .align-center}

> ## mysql 다운로드

- https://hub.docker.com/_/mysql
- 위에서 

> ## Start a `mysql` server instance

- Starting a MySQL instance is simple:

```console
$ docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
```

- ... where `some-mysql` is the name you want to assign to your container, `my-secret-pw` is the password to be set for the MySQL root user and `tag` is the tag specifying the MySQL version you want. See the list above for relevant tags.
- MYsql 은 로그인에 필요한 패스워드와 아이디를 입력해야 접근할 수 있습니다.
  - `-e` : 환경변수의 역활을 하는것
  - `-d` : 백그라운드 
  - `mysql:tag` : 원하는 버젼 
- 환경변수를 넘겨서 세팅하는경우가 많습니다. 
  - 그냥 컨테이너에다가 고정으로 패스워드를 박아넣으면 문제가 있음
  - 공유기 해킹의 경우 초기 패스워드로 되어있는 경우 (iptime , 등) 해킹의 위험이 있습니다.
- 그런것들 떄문에, 컨테이너 안에서 사용자가 컨테이너를 만드는 시점에서 패스워드를 세팅하기 위해서 위와 같이 설정하게 됩니다.
  - 이런 이해가 없으면 환경변수가 필요한 이미지를 사용할 경우에, 제한적일수밖에 없는것! 

> ## 환경변수 사용하여 데이터 전달하기 

- 

**reference**

- <https://www.youtube.com/watch?v=i-gP10UvrC8&list=PLnIaYcDMsSczk-byS2iCDmQCfVU_KHWDk&index=7>

