---
layout: single
title: jekyll, minimal-mistakes 적용하기
date: 2018-04-04 20:19:00 +0900
category: development
tags:
  - jekyll
  - minimal-mistakes  
---

github page로 blog를 시작하려고 마음을 먹었을 때 어떤 blog framework를 사용해야할까 고민하게 되었다.  
검색하다 보니 크게 2가지가 나오게 되던데

jekyll vs hexo

hexo는 마음에 드는 theme들이 많이 있었고 쉽게 시작할 수 있었지만 blog source와 publish 되는 blog repository가 나누어 진다는 점은 마음에 들지 않았다.
jekyll은 github에서 post를 작성할 수 있다는 점과 기본적으로 github에서 지원하고 있다는 점이 마음에 들어서 최종적으로 선택을 하게 되었다.

class, method를 처음 작성할 때 name을 고민하듯...  
jekyll로 시작하면서 가장 먼저 했던 고민은 바로 theme였다.  
너무 많아서 무엇을 선택 해야 할 지 감이 전혀 오지 않았다.  

그래서 github를 검색하여 3.4k star를 가지고 있는 minimal-mistakes를 선택하게 되었다.

minimal-mistakes: <https://github.com/mmistakes/minimal-mistakes>

## 1. jekyll, bundler install

gem 명령어를 통해 jekyll을 설치하게 되는데 gem을 실행시키기 위해서는 ruby가 설치되어 있어야 한다.  
추가로 bundler로 같이 설치 해준다.(minimal-mistakes theme에서 정의한 gem을 설치하기 위한 용도로 사용)

```shell
$ gem install jekyll
```
```shell
$ gem install bundler
```

## 2. git repository clone

username.github.io 형태로 만들어진 git repository를 clone한다.

```shell
$ git clone git@github.com:username/username.github.io.git
```
```shell
$ cd username.github.io
```
```shell
$ jekyll new .
```

이렇게 하게 되면 jekyll이 init되게 되어 blog를 시작할 준비가 되게 된다.
```shell
$ jekyll serve
```
실행을 시키게 되면 http://127.0.0.1:4000 으로 blog를 확인해 볼 수 있다.
```shell
$ jekyll serve
Configuration file: /Users/user/username.github.io/_config.yml
            Source: /Users/user/username.github.io
       Destination: /Users/user/username.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 1.062 seconds.
 Auto-regeneration: enabled for '/Users/user/username.github.io'
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.
```

## 3. minimal-mistakes 적용하기

jekyll에 theme를 적용하는 방법에는 크게 2가지가 있다.

첫번째는 github의 fork기능을 사용하는 것이고  
두번째는 theme를 직접 download받아 copy를 하는 것이다.

minimal-mistakes theme의 적용 방법은 아래 Reference를 참고하도록 하자

---

### References
- [Jekyll 블로그 테마 적용하기 (minimal-mistakes)](https://junhobaik.github.io/jekyll-apply-theme/)
