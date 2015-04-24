---
layout: post
title:  ".(DOT)이 들어간 id 찾기"
date:   2015-04-24 11:00:00
categories: javascript jquery
---


### .(DOT)이 들어간 id 찾기
  
jquery에서 아이디나 클래스를 찾는 건 기본적으로 다들 알 것이다.

```javascript
  $('#test').val();
  $('.burj').val();
```

문제는 id에 .이 들어가있을 때이다.

```javascript
  $('#test.burj').val();
```

```html
  <input id="test.burj"/>
```

html에서 input태그 안에 아이디 값에 .burj가 들어가있다.
jquery로 이 값을 찾으려고하면 무의식적으로
test.burj를 그대로 쓰려고하게되는데 이렇게 되면 찾지 못한다.

jquery가 test라는 id와 함께 쓰이는 burj class를 찾으려고하기 때문이다.

이를 해결하려면

```javascript
  $('#test\\.burj').val();
```

이런 식으로 \\ 를 추가해주면 된다.
