---
layout: post
title:  "Generic Type으로 return시 주의점"
date:   2015-05-20 09:40:00
categories: java
---


### Generic Type으로 return시 주의점
  
일주일 전에 이클립스에서 무난하게 빌드 성공을 한 프로젝트를 보고서  
더이상 체크할 게 없다고 생각하고 개발 및 운영 브랜치에 그대로 머지한 일이 있었다.  

그런데 후에 개발 서버를 빌드/배포하는데 빌드 과정에서 에러가 났다.

분명 에러가 날 일이 없었는데 어찌된 일인가 싶었는데  
책임님께서 java에서 어떤 함수가 원시 타입(int, boolean, char 등...)을 return할 경우  
return을 generic 함수로 하면 서버에서 빌드 시엔 에러가 난다고 말씀해주셨다.

코드를 고치고 나서 좀 더 공부를 해봤는데 정확히는  
Maven에서 빌드할 때 에러가 나는 문제였다.

```java
  public int getValue() {
  return otherValue();
  }
  
  public T<T> otherValue(){
    // some code...
  }
```

위 코드의 경우  
return otherValue()를 해줄 때 에러가 난다.

이를 회피하는 방법으로는 다음과 같다.  

```java
  public Integer getValue() {   //wrapper class 사용 
  return otherValue();
  }

  public int getValue() {   
  return (Integer)otherValue(); // type casting
  }
  
  public int getValue() {   
  return <Integer>otherValue(); // generic type 명시
  }
```

해당 원인에 대해서는 maven의 오류라는 말도 있고
이클립스가 에러를 캐치하지 못한다는 말도 있고...
의견이 좀 나뉘는 듯 싶다.
