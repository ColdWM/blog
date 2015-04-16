---
layout: post
title:  "서로 다른 조건을 동시에 COUNT하기"
date:   2015-04-15 09:30:00
categories: db
---


### 서로 다른 조건을 동시에 COUNT하기
  
최근에 쿼리를 작성하다가 서로 다른 조건일 경우 동시에 COUNT 후
값을 출력해야되는 경우가 생겼다.

물론, 작성한 쿼리는 업무 이해를 잘못하면서 생긴 쿼리라 사라지긴했지만...
잊지 않기 위해서 & 공유하고자 여기에 작성해본다.

test_table이라는 테이블 안에 temp라는 column이 0 또는 1의 값으로만 이루어져있다고 가정하자.

temp|
----|
0 |
1 |
0 |
0 |
1 |

이걸 0이나 1만 따로 COUNT하는 것은 간단하다.

```sql
  SELECT COUNT(*)
    FROM test_table
    WHERE temp=0 --또는 1
```

근데 0과 1이 몇개가 있는지 동시에 알고 싶다면
WHERE 조건에서 어떻게 해야할 지 난감하게 된다.

이 문제는 DECODE 와 SUM 함수로 해결이 가능하다.
알다시피 DECODE는 if~else 구문 역할을 해주므로 조건절의 역할을 해준다.
SUM은 COUNT의 역할을 대체해준다고 생각하면 된다.

```sql
  SELECT
    SUM( DECODE (temp, 0, 1, 0) ) AS tempValue0,
    SUM( DECODE (temp, 1, 1, 0) ) AS tempValue1
  FROM test_table
```

위 쿼리를 실행하면 밑의 테이블처럼 결과가 나올 것이다.

tempValue0 | tempValue1
-----------|------------
3 |2
