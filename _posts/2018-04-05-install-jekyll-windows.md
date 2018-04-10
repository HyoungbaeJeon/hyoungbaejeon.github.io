---
layout: single
title: windows에서 jekyll 설치하기
date: 2018-04-05 00:20:00 +0900
category: development
tags:
  - jekyll
  - ruby
  - windows
---

jekyll을 설치하기 위해서는 먼저 ruby를 설치해야 한다.  
windwos에서 ruby를 설치하기 위해서는 ruby installer for windwos를 이용한다.

<https://rubyinstaller.org>

devkit이 포함되어 있는 Ruby+Devkit 2.5.1-1 버전을 download 한다.

[Ruby+Devkit 2.5.1-1 download](https://github.com/oneclick/rubyinstaller2/releases/download/rubyinstaller-2.5.1-1/rubyinstaller-devkit-2.5.1-1-x64.exe)

설치를 정상적으로 끝나게 되면 windwos cmd에서 gem을 실행할 수 있다.

```shell
> gem --version
2.7.6
```

그다음 jekyll을 설치한다.
```shell
> gem install jekyll
....생략
25 gems installed
```
```shell
> jekyll --version
jekyll 3.7.3
```

그다음 jekyll serve 명령어로 실행을 하게 되면 아래와 같은 오류가 발생한다.
```shell
> jekyll serve                                                                                                                  
Traceback (most recent call last):                                                                                              
        5: from C:/Ruby25-x64/bin/jekyll:23:in `<main>'                                                                         
        4: from C:/Ruby25-x64/bin/jekyll:23:in `load'                                                                           
        3: from C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/jekyll-3.7.3/exe/jekyll:11:in `<top (required)>'                         
        2: from C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/jekyll-3.7.3/lib/jekyll/plugin_manager.rb:48:in `require_from_bundler'   
        1: from C:/Ruby25-x64/lib/ruby/2.5.0/rubygems/core_ext/kernel_require.rb:59:in `require'                                
C:/Ruby25-x64/lib/ruby/2.5.0/rubygems/core_ext/kernel_require.rb:59:in `require': cannot load such file -- bundler (LoadError)  
```
bundler가 필요하다고 하니 bundler를 설치해준다.
```shell
> gem install bundler
Fetching: bundler-1.16.1.gem (100%)
Successfully installed bundler-1.16.1
Parsing documentation for bundler-1.16.1
Installing ri documentation for bundler-1.16.1
Done installing documentation for bundler after 5 seconds
1 gem installed
```

그다음 bundle 명령어를 통해 gem dependency를 추가한다.  
그런다음 jekyll serve를 올리니
```shell
> jekyll serve
Configuration file: C:/username.github.io/_config.yml
            Source: C:/username.github.io
       Destination: C:/username.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
  Conversion error: Jekyll::Converters::Scss encountered an error while converting 'assets/css/main.scss':
                    Invalid CP949 character "\xE2" on line 54
jekyll 3.7.3 | Error:  Invalid CP949 character "\xE2" on line 54
```
에러가 발생한다. 구글링을 해서 찾아보니 아래와 같은 글이 있었다.  
Ruby on Windows 가 기본적으로 CP949 Encoding 으로 동작하기 때문에 벌어지는 issue였다.

[Windows 환경에서 jekyll 실행 시 CP949 에러](https://jprogram.github.io/articles/2017-12/Windows)

```shell
> chcp 65001   # 윈도우 터미널에서 사용할 Encoding(Code Page) 변경
> jekyll server> jekyll server
Configuration file: C:/username.github.io/_config.yml
            Source: C:/username.github.io
       Destination: C:/username.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 1.874 seconds.
 Auto-regeneration: enabled for 'C:/username.github.io'
  JekyllAdmin mode: production
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.
```
