---
title:  "Window to Mac"
excerpt: "윈도우는 이제 안녕"
categories:
  - Others
last_modified_at: 2021-11-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true

---

# [Convert to Mac](#link){: .btn .btn--primary}{: .align-center}

- 최근에 저는 (11/14) 드디어.. 윈도우를 벗어나고 아예 맥으로 갈아탓는데요, 그 과정에서 하필 M1칩을 사용하는 데스크탑으로 바꾸어버려서.. 

> ## Install Brew

- 우선 맥으로 처음 바꾸게 된다면 문제점은 Home brew 를 어떻게 설치하느냐 이다.
  - https://brew.sh/index_ko
- 위 사이트에서 우선 home brew 를 설치하면 됩니다. 하지만 대망의 m1 칩 답게, 설치도 잘 안되는것을 보여주는데요

````
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
````

- 위처럼 brew 를 설치하면 , 설치된 위치의 path 를 잘 인식하지 못한다고 합니다. 그래서 결국에는 아래와 같이 추가적인 step 이 필요하다고 하네요

````
==> Next steps:
- Add Homebrew to your PATH in /Users/<USER_ID>/.zprofile:
    echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/<USER_ID>/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"
- Run `brew help` to get started
- Further documentation:
    https://docs.brew.sh
````

- 즉 위의 안내에 따라 다음을 실행해주면 됩니다.

````
$ echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/<USER_ID>/.zprofile
$ eval "$(/opt/homebrew/bin/brew shellenv)"
````

- 위를 실행하고 나서, brew 가 잘 작동하는지 검사하시면 됩니다. 

````
$ brew --version
Homebrew 3.1.5
bHomebrew/homebrew-core (git revision 543e4a048e; last commit 2021-05-05)
````

> ## Install rbenv

```
brew update
brew install rbenv ruby-build
```

- brew 를 통해서 rbenv 를 설치합니다. 

````
rbenv versions
# * system (set by /Users/idong-uk/.rbenv/version)
````

- 위처럼 잘 설치되었는지를 확인합니다. 
  - 잘 설치되어있다면, 주석의 값이 출력되는데요, 즉, 아직 설치를 안해도 루비가 시스템에 있음을 알 수 있습니다. 
- 하지만 우리가 사용해야할 루비는 시스템 버전이 아닙니다. rbenv 로 관리되는 루비를 원합니다.
  - 그러므로 어떠한 버젼을 설치할 수 있을지 한번 살펴봅시다.

````
rbenv install -l
````

$$\begin{aligned}
&2.6 .7 \\
&2.7 .3 \\
&3.0 .1 \\
&\text { jruby-9.2.17.0 } \\
&\text { mruby-3.0.0 } \\
&\text { rbx-5.0 } \\
&\text { truffleruby-21.1.0 } \\
&\text { truffleruby+graalvm-21.1.0 }
\end{aligned}$$

- 그러면 위처럼 우리가 설치할 수 있는 버젼들이 나오는데요, 여기에서 최신버전인 3.0.1 을 설치하도록 하겠습니다. 

````
rbenv install 3.0.1 
````

- 위와 같이 진행하게 되면 rbenv 를 3.0.1 로 설치하게 됩니다. 즉 

````
rbenv versions
````

````
* system
  3.0.1 (set by/Users/jaekwonchoi/.rbenv/version)
````

- 위와 같이 rbenv 에 3.0.1 이 추가적으로 깔려있는것을 볼 수 있습니다. 
- 그러면 이제, rbenv로 글로벌 버전을 3.0.1로 변경하자.

```
rbenv global 3.0.1
```

- 다시 버전을 확인하면

```
rbenv versions
```

- 아래와 같이 바뀐걸 볼 수 있다.

```
  system
* 3.0.1 (set by /Users/jaekwonchoi/.rbenv/version)
```

> ## Add Path 

- 하지만 위 정도로만 끝나면 좋겠지만, 아직 좀 더 남았습니다. 

````
vim ~/.zshrc
````

- 위를 수행하면 이상한 창이 나오는데, 거기에서 우선 i 를 누른뒤, 

````
[[ -d ~/.rbenv  ]] && \
  export PATH=${HOME}/.rbenv/bin:${PATH} && \
  eval "$(rbenv init -)"
````

- 위 수식을 넣고 , esc 를 누른 뒤에 :wq 를 넣어서 빠져나오면 됩니다. 

````
source ~/.zshrc
````

- 그 이후에는 위처럼 source 로 코드를 적용하면 됩니다.

> ## jekyll, bundler 설치

- 아래와같이 gem install 명령어를 사용하여 jekyll과 bundler를 설치한다.
- 젬(gem)은 분산 패키지 시스템으로 라이브러리의 작성이나 공개, 설치를 도와주는 시스템이다.
- 리눅스에서의 apt 시스템과 유사하다. 루비는 젬(gem)을 사용하여 라이브러리 설치를 진행한다.

```
gem install jekyll bundler
```

이후 jekyll이 잘 설치 되었는지 확인하자.

```
jekyll -v
```

```
jekyll 4.2.0
```

> ## Problem

- 하지만 위처럼 지킬까지 깔았더라도, 다음과 같이 에러가 날 수 있습니다. 
  - 이 경우에는 아래의 링크를 들어가보시면 됩니다. 
  - https://blog.naver.com/kmj4138/222558560724

**Reference**

- <https://choijaegwon.github.io/githubblog/GithubBlog3/>
- <https://minacle.github.io/post/create-a-blog-with-jekyll-on-github-pages/>
- <https://www.lainyzine.com/ko/article/how-to-install-homebrew-for-m1-apple-silicon/>
- <https://blog.naver.com/kmj4138/222558560724>
