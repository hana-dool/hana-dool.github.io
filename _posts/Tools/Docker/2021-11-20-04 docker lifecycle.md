---
title:  "Using docker"
excerpt: "도커 사용해보기"
categories:
  - docker
last_modified_at: 2021-11-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 이제! 컨테이너를 실행하고 이를 한번 이용해봅시다.
{: .notice--warning}

# [Install](#link){: .btn .btn--primary}{: .align-center}

> ## 라이프 사이클

![png](/assets/images/Program/8_1.png)

- 레지스트리에서 Pulling 을 통해서 이미지를 저장할 수 있습니다.
- 레지스트리에 Push 를 통해서 이미지를 업로드 할 수도 있습니다.
- 이러한 이미지는 처음 받는다면, 이 자체로는 사용할 수 없습니다.
  - 컨테이너가 필요합니다. 그래서 create 를 통해서 컨테이너를 말해야 합니다. 
- 컨테이너를 만들었다고 해도, 이를 구동하려면 (실행) 즉 메모리에 띄워서 어플리케이션을 시작하려 한다면, START 명령을 내려서 메모리에 올려야 합니다.
- 이때 run 이란 Pull + Create + Start 를 한번에 해줍니다.
  - 위 이미지에서 풀링은 빼놧는데, 이미 풀링이 되어있는 이미지라면, 풀링을 다시 하지 않기때문에 빼놨습니다. 
- 이미지를 컨테이너로 실행했다고 하면, create 와 start 가 계속 됩니다.
  - run 을 두번하면 컨테이너가 계속 새로 만들어집니다. 
  - 이렇게 하면 불필요한 컨테이너가 계속 만들어집니다.
- 즉 run 이라는 명령어는 create 가 필요한 순간만 쓰는것입니다.
  - 즉 create 와 start 를 따로 따로 쓰는것을 권장드립니다. 
- 메모리에 올린 (즉 돌아가고 있는 컨테이너) 를 중단하고 싶으면 STop 을 사용하면 됩니다.
- 컨테이너를 지우고 싶다면 RM 을 쓰면 됩니다.
- 이미지를 지우고 싶다면 RMI (remove image) 를 쓰면 됩니다.
- 컨테이너를 쓰게되면, 쓰고있던 이미지를 다시 만들어주는것을 commit 이라고 합니다.
  - 즉 기존에 쓰던 것을 이미지화 시킬 수 있습니다.
  - 엄청 많이 어플리케이션을 설치한 이후에 다시 이미지화 하면 된다는 것입니다. 

> ## 명령어

### 5.1 도커 이미지 다운로드와 삭제

```bash
docker pull consol/tomcat-7.0
docker rmi consol/tomcat-7.0
```

### 5.2 톰캣 컨테이너 생성

```bash
docker run -d --name tc tomcat # 톰캣 생성 및 실행
```

### 5.3 실행중인 컨테이너 확인

```bash
docker ps # 톰캣 컨테이너 확인
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
f6e513b399a6        tomcat              "catalina.sh run"   27 seconds ago      Up 26 seconds       8080/tcp            tc
```

### 5.4 모든 컨테이너 확인

```bash
docker ps -a # 모든 컨테이너 확인
```

### 5.5 컨테이너 중지

- 컨테이너의 아이디 또는 이름을 주면 됩니다.

```bash
docker stop f6e513b399a6 # 컨테이너 실행 중지
f6e513b399a6
```

### 5.6 컨테이너 삭제

- 중지가 된 상태에서만 삭제가 가능하다는것을 명심합니다.

```bash
docker rm f6e513b399a6 # 컨테이너 삭제
f6e513b399a6
```

**reference**

- <https://www.youtube.com/watch?v=i-gP10UvrC8&list=PLnIaYcDMsSczk-byS2iCDmQCfVU_KHWDk&index=7>

