---
layout: post
title:  "JavaScript에서 함수에 타이머를 주자"
date:   2015-04-08 21:00:00
categories: java web javascript
---


### JavaScript에서 함수에 타이머를 주자"
  
자바스트립트에서 함수를 이용하자면 일정 시간 간격으로
함수를 실행하고 싶을 때가 올 것이다. 이에 대한 예제를 한번 만들어보도록 하겠다.
참고로 예제는 jQuery를 사용한다는 가정 하에서 작성되었다.


```javascript
  function example() {
    //...
  }
```
example() 이라는 함수를 5초마다 실행하고 싶다고 할 때...

```javascript
  setInterval("example()", 5000);
  //....
```
위와 같이 작성하면 5초마다 움직이게 된다.

하지만 항상 example() 함수가 작동하길 원하진 않을 때도 있을 것이다.
그럴 때는 밑에와 같이 작성하면 된다.

```javascript
  var isStop = setInterval("example()", 5000);
  clearInterval(isStop);
```

clearInterval을 이용하면 setInterval을 해준 것을 말그대로 clear해줌으로써
5초마다의 실행을 막을 수 있다.

만약 다시 실행하고싶다면
다시 setInterval을 해주면 된다.

또한, 타이머를 한 번만 실행할 수 있는 방법도 있다.

```javascript
  setTimeout("example()", 5000);
```

위 코드로 실행을 하게 되면 5초 이후에 example() 함수를 호출하고
더이상 함수 실행을 하지 않는다.

본인이 자신이 원하는 때에만 딜레이를 준 후 특정 함수 실행을 하고 싶을 때는
setTimeout()을 이용하면 된다.
