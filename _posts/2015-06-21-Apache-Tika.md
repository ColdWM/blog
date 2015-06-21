---
layout: post
title:  "Apache Tika"
date:   2015-06-21 22:30:00
categories: java apachetika
---


### 파일 형식 알아내기 

업로드하는 기능을 만들 때 보통 파일의 형식을 정해주곤 한다.  
그림파일, 동영상 파일, 압축 파일 기타 여러가지.  

이 때 업로드하는 파일의 형식을 확인하는 것이 기본적인 보안이다.  

가장 간단한 방법은 자바스크립트로 업로드 시에  
압축 파일의 확장자를 검사하는 것이다.  

하지만 이 방식은 한가지 문제점이 있다.  

만약, 업로더가 jpg파일을 avi파일로 확장자만 바꾼다면
업로드는 정상적일지라도 그 이후의 동작에서 에러가 날 수 있다. 
따라서, 파일의 내부를 검사할 필요가 있다.  

이를 처리해주는 것이 바로 apache tika이다.  

```java
import java.io.IOException;
import java.net.URL;
 
import org.apache.tika.Tika;
 
public class TikaDemo {
 
    public static void main(String[] args) {
        Tika tika = new Tika();
        try {
            String mimeType = tika.detect(new URL("http://tika.apache.org/tika.png"));
            System.out.println(mimeType);
        } catch(IOException e) {
            System.err.println(e.getMessage());
        }
    }
 
}
```

mimetype으로 파일의 내부를 알 수 있다.  
이 mimetype은 정해진 형식이 있다. [링크](http://www.sitepoint.com/web-foundations/mime-types-complete-list/) . 

위 링크에서처럼 확장자와 mimetype이 다르다면  
확장자를 임의로 바꾼 파일이라는 뜻이 된다.  



