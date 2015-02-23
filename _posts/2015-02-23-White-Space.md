---
layout: post
title:  "White Space"
date:   2015-02-23 09:15:00
categories: java web
---


### 공백문자
  
  
최근에 어떤 한 사용자만 자신이 쓴 글을
조회할 수 없다는 문의가 들어왔다.

DB에도 다 데이터가 들어가있는데 뭐가 문제일까...
하고 여러가지 삽질을 하던 끝에
u+2028, u+2029 라는 공백문자가 자바스크립트 변수값으로 들어가면 에러가 나면서
사용자의 글을 나타내는 부분이 동작을 안 하면서 생긴 문제였다.

u+2028과 u+2029는 둘다 line terminator로 작동하는데
(u+2028은 line separator, u+2029는 paragraph separator)
내 생각엔 저 이유로 인해 변수가 제대로 선언이 안 된 것처럼 인식한게 아닌가 싶다.
예를 들자면...

  var temp = "abcde"";

와 같은 느낌...??

참고로 저 두 공백문자는 보안상의 이유(피싱 위험)로 쓰지말라는 정보도 있다.

사실 제일 신기한 건 사용자가 저런 공백문자를 어디서 구해왔냐는 거.


참고 링크는
  
  http://stackoverflow.com/questions/16686687/json-stringify-and-u2028-u2029-check
  
입니다.
