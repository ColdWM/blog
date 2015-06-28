---
layout: post
title:  "SQL Functions"
date:   2015-06-28 23:30:00
categories: sql
---


### SQL Functions

그간 DB 쿼리를 짜면서 이용한 함수들 중 자주 이용하여  
기억에 남는 3개를 정리해보고자 한다.

- DECODE  

DECODE는 if, else if,...., else를 요약한 것과 비슷하다.  
DECODE(a, b, c, d, e, f) 를 JAVA 예제로 들면  
```java
if(a == b) {
  return c;
else if (a == d) {
  return e;
} else {
  return f;
}
```
이런 식으로 동작하는 함수이다.  

- NVL  

NVL은 null 값을 비교하여 결과값을 리턴해주는 함수다.  
NVL(a, b) 라면 a가 null 이면 b를 리턴해주고 그게 아니라면 a를 리턴한다.  
NVL2도 있는데 다른 점은 NVL2(a, b, c) 와 같은 형식으로 작성하고,  
null이 아니면 b, null이면 c를 리턴하게 된다.  

- DATEDIFF  

날짜 차이를 integer값으로 리턴해주는 함수다.  
아무래도 조건에 날짜가 들어가게 되는 경우가 많은데 그 때 유용하다.  

```sql
DATEDIFF('20150121', '20150101')
-- 결과는 -20이 나오게 된다.
```




