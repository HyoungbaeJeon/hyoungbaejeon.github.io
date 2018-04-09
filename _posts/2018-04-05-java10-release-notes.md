---
layout: single
title: Java10 Release Notes로 알아보는 신규 기능
date: 2018-04-05 17:15:00 +0900
tags:
  - java 10
  - Surveillance Station
  - License
---

### 1. new method : Optional.orElseThrow()

#### java 10
```java
Optional.ofNullable(sample).orElseThrow();
```
#### java 8
```java
Optional.ofNullable(sample).orElseThrow(() -> new NoSuchElementException());
```
orElseThrow() method가 생겨서 value값이 null이면 NoSuchElementException을 throw 한다.
