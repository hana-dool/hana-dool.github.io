---
title:  "anaconda and (base)"
excerpt: "(base) 가 늘 터미널 앞에 뜨는 현상"
categories:
  - Anaconda
last_modified_at: 2021-11-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

아나콘다 설치 후에 base 가 늘 뜨는 에러를 어떻게 잡을 수 없을까요?
{: .notice--warning}

# [anaconda and (base)](#link){: .btn .btn--primary}{: .align-center}

> ## (base) 가 항상 맨 앞에 있어요

- 아나콘다를 설치하고 나서, 터미널을 키면 항상 base 가 앞에 표시되어있는것을 볼 수 있습니다. 
- 이러한 이유는 바로 anaconda 가 기본적으로 터미널이 실행될때 Activate 가 되기 때문입니다.
- 이를 잡아내기 위해서는 다음과 같은 명령어를 사용하여 conda 를 deactivate 할 수 있습니다.

```
(base) gorany@goranys-MacBook-Air R % 
```

```
conda deactivate
```

```
gorany@goranys-MacBook-Air R % 
```

- 위처럼 conda 를 끄고, 기본 셸로 돌아올 수 있습니다.

> ## 앞의 (Base) 를 없애주세요

- 하지만 우리는 위처럼 일시적인 조치가 아니라 영구적인 조치를 원할텐데요, 우선 아나콘다의 auto activate 가 켜져있는지 확인하기 위하여 다음의 명령어를 실행해봅시다.

```
$ conda config --show | grep auto_activate_base
auto_activate_base: True
```

- 위처럼 auto_activate_base 가 Trure 로 되어있는것으로 봐서, 이것을 False 로 돌려주어야 합니다. 

```
conda config --set auto_activate_base False
```

- 위와 같이 설정하면 이제 더이상 base 가 activate 되지 않습니다.

> note

- changeps1를 이용하여 끄는것은 그냥 command 에서만 안보이게 하는거라서 비추

---

**Reference**

- <https://stackoverflow.com/questions/55171696/how-to-remove-base-from-terminal-prompt-after-updating-conda>
- <https://stackoverflow.com/questions/51526503/why-does-base-appear-in-my-anaconda-command-prompt>



