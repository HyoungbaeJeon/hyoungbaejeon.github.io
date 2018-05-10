---
layout: single
title: Too many open files error 해결하기
date: 2018-05-10 20:32:00 +0900
category: development
tags:
  - ulimit
  - error
  - issue
---

최근 serverless를 이용하여 aws에 deploy하는 프로젝트틀 하고 있다.  
하지만 dependency가 늘어나다 보니 package 할 때  

"Too many open files error"

라는 에러는 출력하며 deploy가 잘 되지 않는 현상이 발생 하였다.  
여기저기 찾아보다 보니 아래 방법으로 해결할 수 있었다.  
다시 사용할 날을 위해서 기록.  

```bash
$ echo kern.maxfiles=65536 | sudo tee -a /etc/sysctl.conf
$ echo kern.maxfilesperproc=65536 | sudo tee -a /etc/sysctl.conf
$ sudo sysctl -w kern.maxfiles=65536
$ sudo sysctl -w kern.maxfilesperproc=65536
$ ulimit -n 65536
```
