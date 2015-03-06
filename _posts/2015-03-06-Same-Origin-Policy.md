---
layout: post
title:  "White Space"
date:   2015-03-03 10:23:00
categories: java web security
---


### Same Origin Policy (동일 출처 정책)
  
  
Origin : URL의 포트 ,호스트, 그리고 스킴으로 정의되는 것을 오리진이라 한다.  
일반적으로 정보들은 서로 독립적이고 구별되는 출처로부터 가져와진다. 
예를 들어 http://example.com/doc.html에서 가져온 문서가 https://example.com/target.html에서 
가져온 문서의 DOM에 접속하려고 한다면 user agent는 이를 불허할텐데 
그 이유는 첫번째는 http, example.com, 80 이고 두번째의 경우는 https, example.com, 443 이기 때문이다.

네트워크 API에서 동일 출처 정책은 정보 송수신을 구별해준다. 
대략 말하자면, 하나의 출처가 다른 출처로 데이터를 보내는 것이 허용되어도 
다른 출처로부터 데이터를 받는 것은 허용되지 않는다.  
정보 수신 금지는 악의적인 사이트에서의 비밀 정보를 읽는 것을 막아줄 뿐만 아니라 
다른 웹사이트로부터 요청된 합법적인 정보를 읽는 것도 막아준다.

이 정책은 사이트간의 정보 교환 역시 위험하다는 알려준다. 
CSRF(Cross-Site Request Forgery)나 
clickjacking(실제 보는 웹페이지의 콘텐츠가 아닌, 다른 웹페이지의 콘텐츠를 클릭하게 하는 것)의 위험성 등을 막아준다. 

기본적으로 크로스도메인을 막는다고 생각하면 편한 것 같다.  
요번에 내가 번역 및 공부한 것 외에 국내 블로거가 올린 것을 참고용으로 올린다.

  
  http://enterkey88.tistory.com/128
  

