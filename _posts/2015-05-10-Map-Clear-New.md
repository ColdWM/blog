---
layout: post
title:  "Map에서 clear와 new Map"
date:   2015-05-11 21:40:00
categories: java
---


### Map에서 clear와 new Map
  
한 달 전에 나는 List안에 Map 형태인
List&lt;Map&lt;String, String&gt;&gt;를
루프문을 돌리면서 list의 첫번째 Map부터 마지막 Map까지 조건에 맞는 값만
비어있는 다른 List&lt;Map&lt;String, String&gt;&gt;에 넣을 일이 있었다.

예시로 예를 들자면...

```java
List<HashMap<String, String>> targetList = someList;
List<HashMap<String, String>> resultList = new List<HashMap<String, String>> ();
HashMap<String, String> targetMap = new HashMap<String, String>();
for (HashMap<String, String> target : targetList) {
	targetMap.clear();
	targetMap.put("key1", target.get("key1"));
	targetMap.put("key2", target.get("key2"));
	.
	.
	.
	
	resultList.add(targetMap);
}
```

각 target의 각 key값에 맞는 value가 하나하나 resultList에 들어가고있다고 생각을 했었는데...
값이 제대로 안 뜨는 일이 생겼다.

알고보니 clear로는 참조값이 그대로여서 resultList에 add된 값들도 바뀌고있던 것이었다.
new Map으로 해줄 경우 참조값이 달라지기 때문에 같은 현상은 일어나지 않는다.
