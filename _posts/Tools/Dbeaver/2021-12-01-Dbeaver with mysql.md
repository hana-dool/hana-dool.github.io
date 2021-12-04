---
title:  "Connect mysql with DBeaver (Hombrew)"
excerpt: "Dbeaver 사용법"
categories:
  - DBeaver
last_modified_at: 2021-06-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [mysql with DBeaver](#link){: .btn .btn--primary}{: .align-center}

> ## Mysql 연결

- 먼저 brew 를 통해서 mysql 를 설치하는게 좋습니다.

```
brew search mysql

# mysql 설치
brew install mysql
# Rosetta2 관련 에러 발생 시
arch -arm64 brew install mysql
```

- 위와 같이 실행한 뒤, 설치가 되어있는지 확인합시다.

```
gorany@goranys-MacBook-Air ~ % brew list
==> Formulae
apache-spark	jupyterlab	mpdecimal	pkg-config	six
autoconf	libevent	mysql		protobuf	sqlite
brotli		libnghttp2	node		python@3.9	xz
c-ares		libsodium	openjdk		rbenv		zeromq
ca-certificates	libuv		openjdk@11	readline	zstd
gdbm		lz4		openssl@1.1	ruby-build
icu4c		m4		pandoc		scala@2.12
```

- mysql 이 설치되어있는것을 볼 수 잇습니다.

> ## Mysql 세팅하기

```
gorany@goranys-MacBook-Air ~ % mysql.server start

Starting MySQL
 SUCCESS! 
```

- 위와 같이 연결이 잘 된것을 확인할 수 있습니다.

> 암호 설정하기

```
gorany@goranys-MacBook-Air ~ % mysql_secure_installation


Securing the MySQL server deployment.

Connecting to MySQL using a blank password.

VALIDATE PASSWORD COMPONENT can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD component?

Press y|Y for Yes, any other key for No:
```

- 이 설정은 비밀번호 가이드 설정에 대한 부분이고 Yes를 하면 복잡한 비밀번호를, No를 하면 간단한 비밀번호를 설정할 수 있습니다.
- 옵션을 선택하면 root의 비밀번호를 설정하게 된다.
- 저는 No 선택 (어짜피 로컬이니까요)

> 사용자 설정 옵션

```
By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them. This is intended only for
testing, and to make the installation go a bit smoother.
You should remove them before moving into a production
environment.

Remove anonymous users? (Press y|Y for Yes, any other key for No) :
```

- 사용자 설정에 관한 옵션인데 -u 옵션을 주고 로그인할 것인지에 대한 질문으로 이해하면 된다.
- 그냥 yes 를 주는편임

> 원격 접속에서 root 로그인 허용? 

```
Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network.

Disallow root login remotely? (Press y|Y for Yes, any other key for No) :
```

- 다른 IP에서 root를 로그인하게 해주지 않는 편이라서 yes를 준다.
- 이 옵션은 로컬에서 DB를 올려두고 프로젝트를 개발하는 대부분의 사람들에게는 크게 의미없는 부분이니까, 편한대로 선택하면 된다.

> 테스트 DB 를 둘것인가요? 

```
By default, MySQL comes with a database named 'test' that
anyone can access. This is also intended only for testing,
and should be removed before moving into a production
environment.


Remove test database and access to it? (Press y|Y for Yes, any other key for No) : No    
```

- 저는 No 선택 

> 변경된 권한을 테이블에 적용할것인지에 대한 옵션

```
Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.

Reload privilege tables now? (Press y|Y for Yes, any other key for No) : y
```

- 이 부분은 본인의 상황에 따라 적용한다.
- 만약, 변경한 게 하나라도 있으면 그냥 yes를 주자. (변경한 게 없어도 그냥 yes 줘도 된다)

> 다 되고나면? 

```
gorany@goranys-MacBook-Air ~ % mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 5
Server version: 5.7.36 Homebrew
```

- 위와 같이 `mysql -u root -p` 의 명령어를 통해서 로그인이 가능

> ## Dbeaver 

![jpg](/assets/images/Program/29_2.jpg)

- 위와 같이 parameter 를 설정하도록 합시다.
  - <https://wakestand.tistory.com/496> 참고

> Parameter

- Server Host에는 localhost
- username 에는 root
- password 에는 MySQL 설치 시 비밀번호를 넣어주면 된다 (위에서 설정한것!)
- Database는 접속 시 기본 스키마를 말하는데 굳이 설정하지 않아도 된다
- 이후 왼쪽 하단의 Test Connection을 눌러주면 다운로드 하라는게 나올 수 있습니다 (이때는 다운로드 하기) 그 이후 Test Connect 를 했을때 잘 작동하면 끝! 

> ## Testing

![jpg](/assets/images/Program/29_3.jpg)

- 위와 같이 쿼리가 잘 실행되는지 보면 잘 되는것도 볼 수 있습니다.

---

**reference**

- <https://twinparadox.tistory.com/619>
- <https://m.blog.naver.com/pareko/221758528826>
- <https://velog.io/@noyo0123/MYSQL-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%82%AC%EC%9A%A9%EC%9E%90-%EA%B6%8C%ED%95%9C-%EC%84%A4%EC%A0%95>
- <https://velog.io/@kozi15/MAC-m1-MySQL-MySQL-%EC%84%A4%EC%B9%98>
- <https://whitepaek.tistory.com/16>
- <https://wakestand.tistory.com/496>



