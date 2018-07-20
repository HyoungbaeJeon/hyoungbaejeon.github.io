---
layout: single
title: aws cognito token의 진실 그리고 Custom Authorizer
date: 2018-07-20 20:01:00 +0900
category: development
tags:
  - aws
  - cognito
  - token
---

aws cognito를 통해 token을 발급받아보면 3개의 token을 받아오게 된다. 

idToken : 자격 증명 정보 포함, 사용자가 인증하고 1시간이 지나면 만료가 된다. 
accessToken : 자격 증명 정보 포함 안함, 사용자가 인증하고 1시간이 지나면 만료가 된다. 
refreshToken : 만료가 되기전 새로운 token으로 갱신할 때 사용 

aws gateway에서 인증을 위해 Cognito Authorizer를 사용하였는데 여기서 idToken을 사용한다. 
(accessToken 은 auth error 발생) 

하지만 문제가 있었다. 
로그아웃을 하기전 idToken을 가지고 있다가 로그아웃을 하고 난다음 
복사한 idToken을 사용하니 만료시간 전까지 사용을 할 수가 있었다. 
idToken의 만료시간은 따로 설정할수 없었고 1시간으로 고정되어 있었다. 
cognito 로그아웃을 하게 되면 token이 사라질것 같았으나 
cognito의 GlobalSignOut같은 경우에는 
accessToken, refreshToken은 만료를 시키고 있었지만 idToken은 만료를 시키지 않고 있더라 

그래서 gateway 인증을 accessToken을 사용하여 확인을 해야하는데 
Cognito type의 authorizer는 accessToken의 인증을 제공해 주지 않고 있었다. 
결국엔 lambda type의 Custom Authorizer를 만들게 되었다. 

Custom Authorizer는 크게 4단계로 구분을 하였다. 
