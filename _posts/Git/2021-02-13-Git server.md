---
title:  "Server"
excerpt: "서버 저장소(원격 저장소) 에 대해 알아보자."
categories:
  - Git
tags:
  - 3
last_modified_at: 2021-02-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# 서버 저장소

- 서버 저장소는 다른말로 remote 저장소라고 한다.
- 로컬 저장소의 코드를 복제한 복사본



# Repository 만들기

1. 컴퓨터에 폴더 만들기
   - 이 폴더는 Local 저장소가 될 폴더가 된다.
2. git bash here
3. git init
   - 숨겨져 있는 파일 형식으로 .git 이 형성된다.
4. git remote add origin [깃허브의 repository 주소]
   - 주소를 복붙할때 git 는 ctrl shift insert 를 쓴다는것을 주의하자.
   - 이때 repository 주소는 https://github.com/hana-dool/2102_JSproject.git 처럼 뒤에 .git 을 추가해주어야한다.

- 위와 같이 하게 되면, 내 컴퓨터에 Repository 가 형성이 된다.



# 저장소 이름 바꾸기

1. git remote -v 
   - 이를 통해서 기존의 주소를 확인하자.
2. git remote set-url origin [깃허브 주소+.git]
   -  https://github.com/hana-dool/2102_JSproject.git 처럼 저장소 주소 + .git
3. 다시 git remote -v 를 통해서 잘 바뀌었는지 확인한다.



# 저장소 Clone

- 저장소를 단순 백업하고 싶을때에 사용한다.
  - original 프로젝트와 연결되어있지 않다. 즉 권한이 없으면 Push가 불가능
  - Commit 등의 로그를 보지 못한다.

- git clone [........git] 을 통해서 clone 을 할 수 있다.
- 단순 다운로드와는 다른점이, pull 을 통해서 원격 저장소의 갱신된 내용을 추가로 내려받는것이 가능하다는 것이다.
  - git pull 을 통해서 원격 저장소의 커밋 정보를 최신으로 내려받게 된다.



# git Pull 과 git Fetch

- git pull

  - git pull 은 수정된 코드를 즉시 merge하고 코드를 반영한다. 
  - 편리하긴 하지만 충돌이 일어날 수 있다.

- Fetch 

  - git fetch 원격저장소url

  - 내려받은 후 브랜치와 자동 병합하지 않고 그저 데이터를 내려받기만 할 뿐, 자동병합하지  않는다.
  - merge 
    - git merge [브랜치 이름]
    - Fetch 를 통해서 내려받은 커밋을 로컬 저장소에 적용하기 위해서는 병합 명령을 내려주어야 한다.

# 충돌 방지

- 원격 저장소에 푸시하기 위해서는 자신의 로컬 저장소를 최신상태로 유지해야 한다.

  - 즉 원격 저장소의 제일 최근 commit 보다 최신이여야 한다는 것
  - A라는 사람이 나보다 10초 먼저 Push 해서 저장소를 업데이트 했다고 하자. 그러면 내 Push 는 최신상태(제일 최근 커밋이 반영되지 않았으므로)보다 뒤쳐지게 되고, Git 은 푸시 동작을 거부하게 된다.
  - 그러므로 자신의 저장소를 pull 을 통해서 최신 상태로 Update 시킨 후에 Push 할 수 있게 된다.

- A,B 가 같은 영역을 동시에 수정하게 되면 한쪽에서 Pull 을 할 때에 충돌이 발생한다.

  - 이를 해결하기 위해서는 Pull 을 자주 해주면서 지속적으로 commit 갱신을 확인해야 한다.
  - 내 수정 내역을 다른사람도 빨리 확인해 줄 수 있도록 Push 를 자주하는것도 중요하다.

  

