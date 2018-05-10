---
layout: single
title: serverless deploy time 줄이기
date: 2018-05-10 20:43:00 +0900
category: development
tags:
  - serverless
  - deploy
  - build
---

aws gateway와 lambda를 배포 하기 위해 serverless를 사용중이다.  
handler의 수가 적을 때는 deploy 시간이 문제가 되지 않았다.  
하지만 dependency가 늘어나고 handler가 늘어나게 되니  
build time이 15min을 넘어가는 일이 발생하게 되었다.  

처음 배포가 된다면 serverless deploy function을 이용하여 빠르게 배포할 수 있었지만  
신규 handler가 추가 되게 되면 배포하기 위해 15min이상이 걸리다니...
처음이 문제였다.  

그래서 어디에서 시간이 많이 걸릴까 찾다보니  
package 과정에서 dev dependency를 exclude 하면서 시간이 많이 걸리더라  
그래서 package option에서 excludeDevDependencies를 false로 세팅하였다.  

그렇게 되면 devDependencies node_module이 포함이 되게 되니  
node_modules 전체를 exclude 시켰다.  
이렇게 되면 handler에서 사용하는 dependency가 빠지게 되니  
이를 다시 넣어줘야 했는데 아래 plugin으로 쉽게 해결하였다.  
serverless-plugin-include-dependencies  

[](https://github.com/dougmoscrop/serverless-plugin-include-dependencies)

```yaml
package:
  excludeDevDependencies: false
  individually: true
  exclude:
    - node_modules/**
    - test/**

plugins:
  - serverless-plugin-include-dependencies
```
