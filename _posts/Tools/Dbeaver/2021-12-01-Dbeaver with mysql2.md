---
title:  "Connect mysql with DBeaver (dmg)"
excerpt: "Dbeaber 와 mysql 연결 해결방법"
categories:
  - DBeaver
last_modified_at: 2021-12-04

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [mysql with DBeaver](#link){: .btn .btn--primary}{: .align-center}

> ## Dbeaver 연결 에러

`Communications link failure The last packet sent successfully to the server was 0 milliseconds ago. The driver has not received any packets from the server.`

- homebrew 로 잘 설치하고 나고, 설정도 잘 했고, dbeaver 실행도 다 잘 했는데, 막상 컴퓨터를 껏다 켜보니,  위처럼 Dbeaver 에서 연결 에러가 날 수있습니다.
- 이럴 경우에는 mysql 연결 에러가 발생한 것입니다.. 즉 이는 dbeaver 의 문제가 아니라 mysql 의 문제인데요, 터미널에서 mysql 명령어를 실행해보아서 대체 어떤일이 일어나고 있는지 알아봅시다.

> ## Mysql 연결 실패?

```
Starting MySQL
./usr/local/Cellar/mysql/8.0.15/bin/mysqld_safe: line 674: /usr/local/var/mysql/MacBook-Pro.local.err: No such file or directory
Logging to '/usr/local/var/mysql/MacBook-Pro.local.err'.
/usr/local/Cellar/mysql/8.0.15/bin/mysqld_safe: line 144: /usr/local/var/mysql/MacBook-Pro.local.err: No such file or directory
/usr/local/Cellar/mysql/8.0.15/bin/mysqld_safe: line 199: /usr/local/var/mysql/MacBook-Pro.local.err: No such file or directory
/usr/local/Cellar/mysql/8.0.15/bin/mysqld_safe: line 937: /usr/local/var/mysql/MacBook-Pro.local.err: No such file or directory
/usr/local/Cellar/mysql/8.0.15/bin/mysqld_safe: line 144: /usr/local/var/mysql/MacBook-Pro.local.err: No such file or directory
 ERROR! The server quit without updating PID file (/usr/local/var/mysql/MacBook-Pro.local.pid).
```

- homebrew 로 mysql 을 설치하고 나면 위처럼 진행이 안될떄가 있습니다. 
- Mysql 을 터미널에서 실행하게 되어도, 디렉토리가 없다는둥 ,PID 를 업데이트 못해서 그렇다는둥.. 에러가 나는 경우가 있습니다.

> 문제점

- 우선 해당케이스의 경우 brew로 mysql설치 후 /usr/local/var/mysql/ 위의 폴더가 생성되지 않아 발생한 문제 였습니다.
- 공식문서에 따르면 mysql을 자동설치 파일로 설치하지 않고 다른 방식으로 설치하면 폴더가 생성되지 않는다는거 같습니다.

> ## 해결

- 애초에 위처럼 homebrew 로 설치하려 하지 말고 그냥 홈페이지에서 dmg 로 설치하는것을 추천합니다.
- https://velog.io/@inyong_pang/MySQL-%EC%84%A4%EC%B9%98%EC%99%80-%EC%B4%88%EA%B8%B0-%EC%84%A4%EC%A0%95
- https://daimhada.tistory.com/121
- 위처럼 dmg 파일로 깐 뒤에, 유저 아이디를 설정하면 , 문제가 해결될 것입니다.

---

**reference**

- <https://niees.tistory.com/72>



