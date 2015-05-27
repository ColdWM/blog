## Factory Method 패턴 ##

이번 스터디 정리는 Factory Method 패턴이다.  
factory는 말 그대로 공장이란 의미를 갖고 있다.  
Template Metho패턴으로 인스턴스를 생성하는 공장을 구성한 것으로,  
인스턴스를 만드는 방법을 상위 클래스에서 결정하나, 구체적인 클래스 이름까지는 결정하지 않는 패턴이다.

즉, 인스턴스 생성을 위한 framework와 실제 인스턴스 생성의 클래스를 분리해서 생각할 수 있다.  

![Factory Method Pattern](http://upload.wikimedia.org/wikipedia/commons/e/ed/Factory_Method_UML_class_diagram.png "출처: http://stackoverflow.com/questions/5739611/differences-between-abstract-factory-pattern-and-factory-method")



### 예제 ###

Java 언어로 배우는 디자인 패턴 입문 책에 있는 예제로 설명을 하겠다.  
ID카드를 만드는 공장을 생각해보자.

Product 클래스와 Factory 클래스가 framework역할을 하고, IDCard 클래스와 IDCardFactory 클래스가 구체적인 내용 구현을 담당한다.

#### Product 클래스 ####

framework 패키지의 Product 클래스는 '제품'을 표현한 클래스이다.  
여기선 추상 메소드 use만이 선언되어있다.  
구체적인 구현은 전부 하위 클래스에게 맡긴다.  

위 그림에서 Product 역할을 한다.  

``` java  
	package framework;  
	public abstract class Product {
		public abstract void use();
	}
```

#### Factory 클래스 ####

여기선 Template Method 패턴을 사용한다.
추상 메소드 createProduct에서 '제품'을 **만들고**, 만든 제품을 추상 메소드 registerProduct에서 **등록**한다.  
Product와 마찬가지로 구현은 하위 클래스가 담당한다.  

여기서 Template Method 패턴이 사용된 부분은 인스턴스를 생성할 때이다.  

위 그림에서 Creator역할을 한다.  

``` java
package framework;
public abstract class Factory {
	public final Product create(String owner) {
		Product p = createProduce(owner);
		registerProduct(p);
		return p;
	}
	protected abstract Product createProduct(String owner);
	protected abstract void registerProduct(Product product);
}
```

#### IDCard 클래스 ####

앞서 말했듯 Product 클래스에 있는 use 메소드를 구현하는 하위 클래스이다.  

ConcreteProduct 역할이다. 

```java  
package idcard;
import framework.*;
public class IDCard extend Product {
	private String owner;
	IDCard(String owner) {
		System.out.println(owner + "의 카드를 만듭니다.");
		this.owner = owner;
	}
	public void use() {
		System.out.println(owner + "의 카드를 사용합니다.");
	}
	public String getOwner() {
		return owner;
	}
}
```


#### IDCardFactory 클래스 ####

Factory 클래스의 하위 클래스. createProduct와 registerProduct의 두 가지 메소드를 구현한다.  
createProduct는 IDCard의 인스턴스를 생성(제품을 **만드는** 일)을 하고,  
registerProduct는 IDcard의 owner를 owners필드에 추가해서 **등록**하는 기능을 하고 있다.  

ConcreteCreator 역할이다.

```java
package idcard;
import framework.*;
import java.util.*;
public class IDCardFactory extends Factory {
	private List owners = new ArrayList();
	protected Product createProduct(String owner) {
		return new IDCard(owner);
	}
	protected void registerProduct(Product product) {
		owners.add(((IDCard)product).getOwner());
	}
	public List getOwners() {
		return owners;
	}
}
```


#### Main 클래스 ####

Factory Method 패턴을 이제 구현해보자

``` java
import framework.*;
import idcard.*;
public class Main {
	public static void main(String[] args) }
		Factory factory = new IDCardFactory();
		Product card1 = factory.create("홍길동");
		Product card2 = factory.create("이순신");
		Product card3 = factory.create("강감찬");
		card1.use();
		card2.use();
		card3.use();
	}
}

```

실행 결과는 다음과 같다.

	홍길동의 카드를 만듭니다.  
	이순신의 카드를 만듭니다.  
	강감찬의 카드를 만듭니다.  
	홍길동의 카드를 사용합니다.  
	이순신의 카드를 사용합니다.  
	강감찬의 카드를 사용합니다.  


#### 정리 ####

이 패턴에서 중요한 점은 Creator다. new를 사용해서 실제의 인스턴스를 생성하는 대신,  
인스턴스 생성을 위한 메소드를 호출해서 구체적인 클래스 이름에 의한 속박에서 **상위 클래스를 자유롭게** 만들어준다.

framework 패키지에서 idcard패키지를 import하지 않는다는 점을 통해 이를 확인할 수 있다.  
새로운 클래스를 만들어도 framework내용을 수정할 필요가 없다.  
즉, framework패키지는 idcard패키지에 **의존하고 있지 않다**는 점이다.

