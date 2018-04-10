---
layout: single
title: Java10 Release Notes로 알아보는 신규 기능
date: 2018-04-05 17:15:00 +0900
category: development
tags:
  - java 10
---

jdk 10 Release Notes는 아래 url에서 확인 할 수 있다.
<http://www.oracle.com/technetwork/java/javase/10-relnote-issues-4108729.html>

Release Notes로 추가된 기능에 대해서 알아보자.

## What's New in JDK 10

### 1. new method : Optional.orElseThrow()

#### java 10
```java
Optional.ofNullable(sample).orElseThrow();
```
orElseThrow() method가 생겨서 value값이 null이면 NoSuchElementException을 throw 한다.
[See JDK-8140281](https://bugs.java.com/view_bug.do?bug_id=JDK-8140281)

### 2. unmodifiable collections의 create api가 추가되었다.
#### java 10
```java
List<String> sampleList = List.of("sample");
Set<String> sampleSet = Set.of("sample");
Map<String, String> sampleMap = Map.of("key", "value");

List<String> unmodifiableList = List.copyOf(sampleList);
Set<String> unmodifiableSet = Set.copyOf(sampleSet);
Map<String, String> unmodifiableMap = Map.copyOf(sampleMap);

Stream<String> stream = Stream.of("Java6", "Java7", "Java8", "Java9", "Java10");

List<String> unmodifiableListFromStream = stream.collect(Collectors.toUnmodifiableList());
Set<String> unmodifiableSetFromStream = stream.collect(Collectors.toUnmodifiableSet());
Map<String,String> unmodifiableMapFromStream = stream.collect(Collectors.toUnmodifiableMap(key -> key+"Key",value->value));
```
[See JDK-8177290](https://bugs.java.com/view_bug.do?bug_id=JDK-8177290)

### 3. disableLastUsageTracking system property 추가
JRE Usage Tracking을 disable 시킬 수 있는 system property가 추가 되었고  
만약 enable 시키고 싶은 경우라면 아래 옵셥을 주면 된다고 한다.(기본 값은 disable)
JRE Usage Tracking 정확히 어떤 일을 하는지는 모르겠다.
#### java 10
```java
-Djdk.disableLastUsageTracking=true
```

### 4. jmxremote.password가 hashed password로 저장됨
password의 format은 아래와 같음.
```
role_name W hashedPassword
```
[See JDK-5016517](https://bugs.java.com/view_bug.do?bug_id=JDK-5016517)

### 5. G1(Garbage First) GC를 위해 Full GC를 Parallel하게 개선
G1 GC는 full collections을 피하게 설계가 되었지만   
메모리가 충분치 않을 경우 full gc가 일어날 수 있음.

[See JDK-8172890](https://bugs.java.com/view_bug.do?bug_id=JDK-8172890)

### 6. JDK에 기본 CA(루트 인증 기관)인증서 세트를 제공

[See JDK-8189131](https://bugs.java.com/view_bug.do?bug_id=JDK-8189131)

### 7. TLS세션 해시 및 확장 마스터 암호 확장 지원

[See JDK-8148421](https://bugs.java.com/view_bug.do?bug_id=JDK-8148421)

### 8. Loop code성능 향상을 위한 Bytecode 생성

[See JDK-8175883](https://bugs.java.com/view_bug.do?bug_id=JDK-8175883)

### 9. javadoc이 다양한 stylesheet를 지원

[See JDK-8185371](https://bugs.java.com/view_bug.do?bug_id=JDK-8185371)

### 10. javadoc에서 Overriding Method들이 더이상 규격을 변경하지 않는다.

[See JDK-8157000](https://bugs.java.com/view_bug.do?bug_id=JDK-8157000)

### 11. javadoc을 위한 Summary tag 추가

[See JDK-8186403](https://bugs.java.com/view_bug.do?bug_id=JDK-8186403)
