---
layout: post
title:  "Ajax 동기/비동기"
date:   2015-06-17 10:30:00
categories: javascript ajax
---


### Ajax 동기/비동기

ajax는 다들 알다시피 기본적으로 비동기 방식으로 동작한다.  
애초에 ajax는 Asynchronous Javascript And XML의 줄임말이다.  

비동기로 작동하는 만큼, 해당 기능이 데이터를 처리하는 동안 또다른  
동작을 수행할 수 있고, 불필요한 로딩을 줄이고 자유로운 페이지 구성도 가능하다.  

하지만 간혹, ajax를 동기 방식으로 동작하게 해야할 때가 있다.

```javascript
 $.ajax({
   type: 'POST',
   url: 'notice/setting',
   data: "temp=1234",
   success: function(data) {
        if(data != null) {
             // Do somothing.
        }
   }
  });
  doAnything();

```

이러한 자바스크립트 코드가 있다면, doAnything() 함수는 위 ajax의 결과와는  
상관 없이 무조건 실행하게 된다. 비동기 방식이므로 data의 처리는 doAnything() 입장에서는  
처리하든 말든 상관이 없게 된다.  

하지만 만약 doAnything()함수의 처리가 위 ajax콜의 영향을 받는다면 어떻게 될까?  

당연히 제대로 된 결과를 못 받을 가능성이 크다. 
클라이언트의 처리 속도가 서버 쪽 처리보다 느리다면 달라지겠지만...  

이런 경우를 방지하기 위해 ajax의 비동기 방식을 설정할 수 있다.  

```javascript
 $.ajax({
   type: 'POST',
   url: 'notice/setting',
   data: "temp=1234",
   async : false,
   success: function(data) {
        if(data != null) {
             // Do somothing.
        }
   }
  });
  doAnything();

```
async는 기본적으로 true로 가지만 위와 같이   
따로 설정을 해준다면 동기 방식으로 작동한다.  
