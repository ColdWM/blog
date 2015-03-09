---
layout: post
title:  "toEquals를 쓸 때 주의점"
date:   2015-03-09 09:30:00
categories: java web
---


### toEquals를 쓸 때 주의점
  
  
예전에 업무 도중에 String 비교를 하려고 toEquals를 썼었을 때,
null값으로 인한 NullPointerException을 본 적이 있다.

예를 들어...

String a가 있고 이 a가 "abcd"라는 문자열과 같은지 알고싶다면 보통
a.toEquals("abcd") 이런 식으로 많이 코딩을 하는데
이 경우에 a가 null이라면 NullPointerException을 띄운다.

이를 방지하는 가장 간단한 방법은 위치를 바꾸는 것이다.
"abcd".toEquals(a) 같은 형태로 코딩을 하면
앞에 null일 걱정은 없다. 

물론, 저런 하드코딩을 하지 않고
변수르 선언을 해주고, null값이 안 들어가도록 짜는 게 제일
낫지 않을까 싶지만....

