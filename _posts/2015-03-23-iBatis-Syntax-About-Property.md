---
layout: post
title:  "iBatis에서 isEqual 쓸 때 프로퍼티 관련"
date:   2015-03-23 09:30:00
categories: java web ibatis
---


### iBatis에서 isEqual 쓸 때 프로퍼티 관련
  
  
iBatis에서의 String 등의 값을 비교하여 if문을 만드는 건
myBatis와는 조금 다르다는 것을 다들 알 것이다.

보통 myBatis에서
  `<if test="value == 'aaa'"> `
와 같은 형태로 작성을 하지만...

iBatis 에서는
  `<isEqual property="value" compareValue="aaa">`
와 같은 형태로 작성을 하게 된다.

여기서 내가 어제 겪었던 에러는
parameterClass를 string으로 주었을 때 내가 준 property를 ibatis에서 못 읽었던 에러다.

내가 자바에서 iBatis로 넘겨주는 변수명이 testValue라고 가정하자.
그렇다면 쿼리문에 '#testValue#' 와 같은 형태로 작성을 할 것이다.

근데
  `<isEqual property="testValue" compareValue="aaa">`
라는 코드에서 property testValue는 java.lang.String에서 읽을 수 없다는 에러가 떳다.

알고보니 iBatis에서 string으로 parameter를 넘겨줄 때  그 변수가 한 개 뿐이라면
isEqual과 같은 구문에서 property를 아예 작성할 필요가 없다고 한다.
참고하도록하자.


