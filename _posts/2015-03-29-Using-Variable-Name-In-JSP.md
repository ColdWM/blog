---
layout: post
title:  "JSP 내에서 변화하는 파일명 쓰기"
date:   2015-03-29 09:30:00
categories: java web jsp
---


### JSP 내에서 변화하는 파일명 쓰기
  
제목은 마땅한 게 떠오르지 않아 저렇게 썼는데, 설명으로 이어나가겠다.
JSP 에서 만약 nhnent_10.png라는 파일명인 그림파일을 띄운다고 가정했을 때 
우리는
```html
  <img src="/img/nhnent_10.png">
```
와 같은 형식으로 태그를 작성할 것이다.

근데 만약 파일명이 상황에 따라 변할 수 있는 상황이라면 어떻게 해야할까?
nhnent_10.png가 아닌, nhnent_12.png 나 nhnent_103.png 등 뒤에 숫자가 계속 바뀐다면...?
그리고 그 숫자가 java에서 맵핑해서 보내는 특정값이라면...?

그 숫자를 pngNum이라는 변수명에 담아 넘기고 있다고 생각하면...
```html
  <img src="/img/nhnent_${pngNum}.png">
```
와 같이 작성을 하면 될..것 같지만...
당연히 그렇지 않다.-_-;

만약 ${pngNum}이 현재 프로젝트에서 없는 그림파일을 불러온다면 해당 그림파일은 불러오지 못하고
당연히 소위 인터넷에서 말하는 엑박이 뜰 것이다.

이를 피하고 싶다면 c 태그 라이브러리를 쓰면 된다.
```html
<c:catch var="e">
  	<c:import url="/img/nhnent_${pngNum}.png" var="imgSrc"/>
  	</c:catch>
  <c:choose>
  	<c:when test="${empty e}">
  	  <img src="/img/nhnent_${pngNum}.png">
  	</c:when>
  	<c:otherwise>
    	<img src="/img/nhnent_1.png">
  </c:otherwise>
  </c:choose>
```
이 코드는 우선 /img/nhnent_${pngNum}.png 경로에 파일이 존재하는지 안하는지를 체크하게된다.
만약 없다면 FileNotFoundException이 뜰 것이고 그렇게되면 var e 에 값이 담기게 된다.
비어있지 않은 변수이므로 <c:when test="${empty e}"> 부분은 패스하고
/img/nhnent_1.png 를 불러오게 된다.

만약 그림파일이 존재한다면 /img/nhnent_${pngNum}.png 에 해당하는 그림파일을 불러오게 될 것이다.

개인적으로 이 코드의 장점은 일일이 그림파일 경로에 해당하는 소스를 짤 필요 없이
특정 값만을 이용하여 그림파일명을 변경하는 것만으로 해결이 가능하다는 것이 아닌가 싶다.
