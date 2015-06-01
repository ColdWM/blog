---
layout: post
title:  "DB에서 이전, 다음 iD정보 가져오기"
date:   2015-06-01 21:40:00
categories: sql
---


### DB에서 이전, 다음 iD정보 가져오기

사실 정확히는 그냥 이전, 다음 데이터 가져오기라고 할 수 있다.  
굳이 ID 정보만 가져올 필요는 없으니 말이다.  

게시판 글을 읽다보면 요즘에는 '이전글' '다음글'에 바로 이동할 수 있는 기능이 거의 대부분 있다.  
웹 프로그래밍을 해봤다면 거의 대부분 이러한 경우 그 글의 ID를 통해 정보를 가져오기 마련이다.  

그렇다면 어느 한 글의 이전, 다음 ID를 쿼리로 가져오는 방법을 알아보자.  

LEAD함수와 LAG함수를 이용하면 되는데
LEAD함수는 현재 row보다 이후에 조회된 데이터들을 가져온다.  
LAG는 당연히 반대로 이전에 조회된 데이터들을 가져온다.

- LEAD(expression, offset[, default]) OVER ([<partition_by_clause>] <order_by_clause>)
여기서 expression은 반환할 컬럼명 또는 반환식, offset은 얼마나 뒤 또는 앞에 있는 데이터를 가져올 지,  
default는 결과값이 null일 경우 정할 값이다.

LAG 역시 마찬가지. 단지 앞의 데이터를 가져올 뿐이다.


- 예제

```sql
	SELECT 	 /*+ USE_IDX */ post_id 
		     , LAG(post_id, 1) over (ORDER BY post_id) prev_post_id
		     , LEAD(post_id, 1) over (ORDER BY post_id) next_post_id
		  FROM post_table
```


