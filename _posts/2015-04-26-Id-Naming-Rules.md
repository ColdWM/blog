---
layout: post
title:  "HTML에서의 id naming rules"
date:   2015-04-28 21:40:00
categories: javascript jquery
---


### HTML에서의 id naming rules
  
지난번 포스트와 이어지는 내용이다.
JavaScript jQuery에서 .(dot)이 들어간 id의 경우 \\\을 앞에 추가하면 해결된다고 적은 바가 있다.

```html
  <input id="test.burj"/>
```
```javascript
  $('#test\\.burj').val();
```

그런데 최근에 작성한 코드 중에서 저걸 추가해주었음에도 불구하고
여전히 해당 id의 요소를 select하지 못하는 현상이 발생했다.

```javascript
  for (var i=0; i < index; i++) {
    $("#test[" + i + "]\\.burj").val();
  }
```
(index는 루프문을 돌리기한 임의의 값)

.(dot)만 해결하면 된다고 생각했는데 그게 아니었다.
혹시나해서 대괄호 [ ] 양쪽에 똑같이 \\\를 추가해줬다.

```javascript
  for (var i=0; i < index; i++) {
    $("#test\\[" + i + "\\]\\.burj").val();
  }
```

코드는 뭔가 참 이상해졌지만...이제 제대로 select를 하기 시작했다.
그 이유가 궁금하여 찾아봤다.

알고보니 html의 id naming rules와 관련이 있었다.

기본적으로 HTML4에서의 규칙은

- 알파벳으로 시작(A-Z, a-z), 그 이후는 숫자, 하이픈(-), 밑줄(_), 코론(:), 점(.)을 가질 수 있다.

그리고 HTML5에서의 규칙은
- 최소한 하나의 문자를 가지고, 어떠한 공백문자라도 가져선 안된다.

보다시피, 괄호에 관한 언급이 없다.

만약 괄호를 사용했는데 제대로 id를 찾지 못한다면
해당 괄호 앞에 \\\를 넣어볼 것을 추천한다.
