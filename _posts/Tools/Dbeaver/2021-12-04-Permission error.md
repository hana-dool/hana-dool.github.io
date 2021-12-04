---
title:  "[Error] do not have a permmision to open"
excerpt: "어플리케이션을 열 수 있는 권한이 없다는 오류"
categories:
  - DBeaver
last_modified_at: 2021-12-04

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [Error](#link){: .btn .btn--primary}{: .align-center}

> ## 에러

![jpg](/assets/images/Program/34_1.jpg)

- 위와 같이 이러한 에러가 가끔 일어납니다. (m1 칩 + dbeaver 베타버젼이라 에러가 나는듯..)

> ## 해결

```
codesign --force --deep --sign - /Applications/DBeaver.app
```

- 위와 같이 DBeaver 에 sign 을 추가하여 해결할 수 있습니다.

---

**reference**

- https://doda.tistory.com/entry/macOS-Big-sur%EC%97%90%EC%84%9C-%EA%B6%8C%ED%95%9C%EC%9D%B4-%EC%97%86%EB%8B%A4%EB%A9%B0-%EC%96%B4%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98%EC%9D%B4-%EC%95%88%EC%97%B4%EB%A6%AC%EB%8A%94-%EA%B2%BD%EC%9A%B0%EC%9D%98-%ED%95%B4%EA%B2%B0
- <https://stackoverflow.com/questions/64842819/cant-run-app-because-of-permission-in-macos-v11-big-sur>



