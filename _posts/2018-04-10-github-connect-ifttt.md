---
layout: single
title: github에서 push가 되게되면 ifttt로 trigger 시키기
date: 2018-04-10 13:15:00 +0900
category: IoT
tags:
  - jenkins
  - ifttt
  - trigger
---

IFTTT는 If This Then That 의 약자로  
지구상에 존재하는 여러 장치, app, 서비스들을 연결시켜주는 서비스 이다.

예를 들어  
"날씨가 더워지면 스마트전구를 빨간색으로 켠다",  
"일몰이 되면 스마트 전구를 켠다" 등의 행위를 할 수 있다.  

<https://ifttt.com>

조금 더 응용을 한다면  
git repository(github, gitlab, bitbucket)에 push가 되면 ifttt로 trigger를 시켜줄 수 있을 것이다.

이렇게 하기 위해서는 ifttt의 webhooks을 이용하면 된다.  

IFTTT에서 webhooks을 검색하여 service를 활성화 시킨다.  

![](/assets/images/2018/04/10/Cap 2018-04-10 13-12-58-891.png)

그리고 조금의 세팅을 거치게 되면 아래처럼 webhook url이 나올 것이다.  

![](/assets/images/2018/04/10/Cap 2018-04-10 13-17-02-459.png)

그리고 webhook url에 접속하게 되면 아래와 같이 event name과 json body를 입력하여 test를 할 수 있다.

event name에 적당히 git_push로 입력을 하고 test를 해보자  
(여기서 잠깐, json body의 key값은 value1, value2, value3으로 고정되어 있다.)
그리고 세팅된 webhook url을 copy를 해두고

![](/assets/images/2018/04/10/Cap 2018-04-10 13-35-24-117.png)

그리고 github repository의 setting -> webhooks에 등록을 하면 된다.

![](/assets/images/2018/04/10/Cap 2018-04-10 13-26-02-622.png)
![](/assets/images/2018/04/10/Cap 2018-04-10 13-28-20-126.png)

그리고 IFTTT에서 간단하게 git_push event가 일어나게 되면  
twitter에 tweet을 등록하는 applet를 생성해보자

![](/assets/images/2018/04/10/Cap 2018-04-10 14-05-45-728.png)

하지만 twitter에 같은 tweet을 등록하게 되면
```
twitter error: status is a duplicate.
```
에러가 발생하니 tweet 앞에 시간을 기록해주자

![](/assets/images/2018/04/10/Cap 2018-04-10 14-31-10-816.png)

그리고 postman으로 post로 요청하게 되면 아래와 같은 message를 받을 수 있을 것이다
```
Congratulations! You've fired the git_push event
```

그리고 activity log를 확인하게 되면 정상적으로 작동된걸 확인할 수 있고

![](/assets/images/2018/04/10/Cap 2018-04-10 14-33-57-885.png)

twitter에 정상적으로 등록이 되었다.

![](/assets/images/2018/04/10/Cap 2018-04-10 14-35-13-280.png)

github push되면 webhook에 의해 trigger 되는것도 볼 수 있다.
