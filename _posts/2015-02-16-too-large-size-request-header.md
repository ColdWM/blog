---
layout: post
title:  "Too large data in request header"
date:   2015-02-16 14:00:00
categories: java web
---


### Request 헤더에 너무 많은 데이터를 넣었을 때
  
  
  

최근의 겪었던 문제.

한 row 에 20개 정도의 데이터 & 780개 가량의 row를 한번에 보낼 때 계속

에러가 나는 경우를 겪었다…


갑자기 null 값이 보내지면서 DB 테이블의 NOT NULL 을 위반했다던가 기존에 쓰던

함수가 갑자기 모든 parameter를 null로 보낸다던가 하는 에러가 뜨면서

대체 어디가 잘못되었던 것일까..하고 한참을 고생했는데

같이 알아봐주신 책임님이 톰캣 설정을 떠올리시고 해결했다.


톰캣 설정에서 server.xml에서

connector 부분에 maxParameterCount 나 maxPostSize를 따로 세팅 안 해주면

너무 많은 값을 한 번의 요청에 넣으면 null값을 보냅니다.


해당 관련 자세한 정보는


http://tomcat.apache.org/tomcat-6.0-doc/config/ajp.html


여기서 보실 수 있습니다.

에시로는...

	 <Connector connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443" maxParameterCount="50000"/>
	 
와 같이 server.xml 에 넣어주면 됩니다.
