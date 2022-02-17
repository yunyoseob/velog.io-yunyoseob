안녕하세요 😊 오늘은 JAVA : 인터페이스클래스를 코드 실습 포스팅하도록 하겠습니다.

## 들어가기전에..

저번 포스팅 [JAVA : Downcasting, 추상클래스, 인터페이스클래스](https://velog.io/@yunyoseob/JAVA-Downcasting-%EC%B6%94%EC%83%81%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%ED%81%B4%EB%9E%98%EC%8A%A4)에서 마지막에 인터페이스클래스에 대해서 간단한 설명 후, 인터페이스 클래스 코드실습을 마지막으로 포스팅을 마쳤습니다.

인터페이스 클래스는 자바 기초에서 중요한 내용인 만큼 오늘은 이에 대해 추가 포스팅을 진행해보도록 하겠습니다.

## 인터페이스클래스 

|인터페이스 특징|
|---|
|**생성자를 가질 수 없다.**|
|**new 연산자로 인스턴스 할 수 없다.**|
|**함수는 굳이 abstract 키워드를 사용하지 않는다.**|
|**변수는 모두 상수이다.**|
|**static 함수와 default함수 사용이 가능하다**|

### 인터페이스 실습 예제 1

5개의 java 파일로 코드 실습을 진행해보도록 하겠습니다. 😊

> **Exam_Inter_1_Class.java**

```java
package a.b.c.ch2.aaaa;

public class Exam_Inter_1_Class implements Exam_Inter_1, Exam_Inter_3{

	@Override
	public /*abstract 키워드 생략*/ void aM(){
		System.out.println("Exam_Inter_1 인터페이스에서 오버라이딩 해서 aM() {}  블럭을 만들고 재정의 하는 함수이다.");				
	}

	
	@Override
	public /* abstract */ void bM(){
		System.out.println("Exam_Inter_1 인터페이스에서 오버라이딩 해서 bM() {}  블럭을 만들고 재정의 하는 함수이다.");		
	}

	@Override
	public /* abstract */ void cM() {
		System.out.println("Exam_Inter_1 인터페이스에서 오버라이딩 해서 cM() {}  블럭을 만들고 재정의 하는 함수이다.");
	}

	@Override
	public void dM(){
		System.out.println("Exam_Inter_2 인터페이스에 있는 추상함수이다.");
		System.out.println("Exam_Inter_1 인터페이스에 extends 키워드로 인터페이스 상속을 해주었다.");
		System.out.println("Exam_Inter_1 인터페이스에 dM() 함수를 오버라이딩 해주었다.");
		System.out.println("Exam_Inter_1_Class 클래스에서 오버라이딩해서 재정의 했다.");
	}
	
	@Override
	public void eM(){
		System.out.println("Exam_Inter_3 인터페이스에 있는 추상함수이다.");
	}
}
```

> **Exam_Inter_1.java**

```java
package a.b.c.ch2.aaaa;

public interface Exam_Inter_1 extends Exam_Inter_2{

	public /* abstract 키워드 생략 */ void aM();
	public abstract void bM();
	public abstract void cM();
}
```
> **Exam_Inter_2.java**

```java
package a.b.c.ch2.aaaa;

public interface Exam_Inter_2 {

	public void dM();
}
```

> **Exam_Inter_3.java**

```java
package a.b.c.ch2.aaaa;

public interface Exam_Inter_3 {

	public void eM();
}
```

> **Exam_Inter_1_Test.java**

```java
package a.b.c.ch2;

import a.b.c.ch2.aaaa.Exam_Inter_1;
import a.b.c.ch2.aaaa.Exam_Inter_3;
import a.b.c.ch2.aaaa.Exam_Inter_1_Class;

public class Exam_Inter_1_Test {

	public static void main(String args[]) {


		Exam_Inter_1 ei1 = new Exam_Inter_1_Class();
		System.out.println("ei1 참조변수 주소값 >>> : " + ei1);

		Exam_Inter_3 ei3=new Exam_Inter_1_Class();

		ei1.aM();
		ei1.bM();
		ei1.cM();
		ei1.dM();
		ei3.eM();
	}
}
```

### 인터페이스 실습 예제 1 그림으로 보는 구성과 결과

> **main 함수가 있는 클래스 이외의 클래스**

![](https://images.velog.io/images/yunyoseob/post/b3ab40f3-509e-4419-abba-2cec715496ef/image.png)

> **작동 방식**

![](https://images.velog.io/images/yunyoseob/post/b5c61e69-8b11-4e0e-bc05-5b5e9d67e8d2/image.png)

> **출력 결과**

```javascript
ei1 참조변수 주소값 >>> : a.b.c.ch2.aaaa.Exam_Inter_1_Class@15db9742
Exam_Inter_1 인터페이스에서 오버라이딩 해서 aM() {}  블럭을 만들고 재정의 하는 함수이다.
Exam_Inter_1 인터페이스에서 오버라이딩 해서 bM() {}  블럭을 만들고 재정의 하는 함수이다.
Exam_Inter_1 인터페이스에서 오버라이딩 해서 cM() {}  블럭을 만들고 재정의 하는 함수이다.
Exam_Inter_2 인터페이스에 있는 추상함수이다.
Exam_Inter_1 인터페이스에 extends 키워드로 인터페이스 상속을 해주었다.
Exam_Inter_1 인터페이스에 dM() 함수를 오버라이딩 해주었다.
Exam_Inter_1_Class 클래스에서 오버라이딩해서 재정의 했다.
Exam_Inter_3 인터페이스에 있는 추상함수이다.
```

### 인터페이스 실습 예제 2

이번에는 각국의 인사말을 인터페이스 클래스에서 상속받아 출력시키는 예제를 진행해보도록 하겠습니다.

> **MessageInterface.java**

```java
package a.b.c.ch2;

public interface MessageInterface{
	public void sayHello(String name);
} 
```

> **MessageKorImpl.java**

```java
package a.b.c.ch2;

public class MessageKorImpl implements MessageInterface{
	@Override
	public void sayHello(String name){
		System.out.println("안녕하세요, "+name+"!!");
	}
} 
```

> **MessageEngImpl.java**

```java
package a.b.c.ch2;

public class MessageEngImpl implements MessageInterface{
	@Override
	public void sayHello(String name){
		System.out.println("Hello, "+name+"!!");	
	}
}
```

> **MessageTest.java**

```java
package a.b.c.ch2;

public class MessageTest{
	public static void main(String[] args){
	MessageInterface eme=new MessageEngImpl();
	eme.sayHello("velog");

	MessageInterface emk=new MessageKorImpl();
	emk.sayHello("벨로그");
	}
}
```

### 인터페이스 실습 예제 2 그림으로 보는 구성과 결과

> **main 함수가 있는 클래스 이외의 클래스**

![](https://images.velog.io/images/yunyoseob/post/d65745e4-7cf9-40bf-ad1e-d0717848ed48/image.png)

> **작동 방식**

![](https://images.velog.io/images/yunyoseob/post/4470c48d-998b-4c12-9794-d3ce1ec56a9f/image.png)

> **출력결과**

```javascript
Hello, velog!!
안녕하세요, 벨로그!!
```

**이상으로 이번 JAVA : 인터페이스클래스(코드실습) 포스팅을 마치도록 하겠습니다. 😀**
