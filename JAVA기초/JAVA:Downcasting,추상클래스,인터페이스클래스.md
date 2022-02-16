안녕하세요 🙂 오늘은 JAVA : Downcasting, 추상클래스를 포스팅하도록 하겠습니다.

## 들어가기전에..

클래스의 종류는 다음과 같습니다.

|**클래스이름**|**사용예시**|
|---|---|
|일반 클래스|public class 클래스이름{함수이름(){}}|
|추상 클래스|public abstract class 클래스이름{ 추상키워드 abstract 함수이름();}|
|인터페이스 클래스|public interface 인터페이스클래스이름{함수이름();}|

[JAVA : 상속, 생성자, 정보의 은닉화](https://velog.io/@yunyoseob/JAVA-%EC%83%81%EC%86%8D-%EC%83%9D%EC%84%B1%EC%9E%90-%EC%A0%95%EB%B3%B4%EC%9D%98-%EC%9D%80%EB%8B%89%ED%99%94) 포스팅에서도 언급했듯이, 사용자 정의 클래스는 java.lang.Object 클래스를 상속하여 만듭니다. 또한, 상속에서 자식클래스는 부모클래스의 자원을 다 사용할 수 있으나, 부모클래스는 자식클래스의 자원을 쓰기 위해 일정 규칙이 필요합니다.

## Downcasting

Downcasting은 부모클래스의 참조변수로는 자기자신 클래스의 자원만 사용이 가능한데, 자식의 자원을 사용하고 싶을 경우, 부모 클래스의 참조변수를 자식 클래스로 다운캐스팅하여 사용해야 합니다.

> **Downcasting을 하는 이유**

![](https://images.velog.io/images/yunyoseob/post/9cca0e9a-da46-4326-9726-f508f1b3d2a0/%EC%A7%81%EA%B3%84%ED%98%88%EC%97%B0%EC%9D%98_%ED%98%B8%EC%B9%AD.jpg) 

예시로, 김해 김씨 3대손에서 김해 김씨 1,2대손의 자원을 쓴다고 합시다. 이 때, 자식은 부모와 상속 관계이므로, 김해 김씨 3대손을 메모리에 올리면, 자동으로 김해 김씨 1,2대손이 메모리에 올라갑니다. 


**🤔 만약 김해 김씨 3대손을 메모리에 올렸는데, 전국에 있는 모든 김해 김씨의 자원을 쓰기 위해 준비해야 한다면?**

무려 142개파에 있는 모든 김해 김씨 자손들의 자원을 사용하기 위해 준비해야 할 것입니다.

이는 매우 비효율적이므로, JAVA에서는 특정 규칙에 따라 자손의 자원을 쓸 수 있도록 하였습니다.

**✔ 따라서, JAVA에서 조상이 후손을 사용하려면, DownCasting을 사용해야합니다.**

이를 DownCasting 실습 코드를 통해 살펴보도록 하겠습니다.

### DownCasting 실습 코드

```java
package a.b.c.ch2;

class Parents extends java.lang.Object{
	Parents(){
		System.out.println("\n 4 or 9. Make Parents Constructor");
	} 

	void Parents_method(){
		System.out.println("\n 7 or 12. Parents Method");
	} 
} 

class Child extends Parents{
	Child(){
		System.out.println("\n 5 or 10. Make Child Constructor");
	} 

	void Child_method(){
		System.out.println("\n 8 or 13. Child Method");
	} 
} 


public class Inherit_p_3{
	void Inherit_p_3_method(){
		System.out.println("\n 3. Inherit_p_3_method");
	} 

	public static void main(String args[]){
		System.out.println(" \n 1. Start main method ");

		Inherit_p_3 rv=new Inherit_p_3();
		System.out.println(" \n 2. Inherit_p_3 rv >>> : "+rv);
		rv.Inherit_p_3_method();

		// First Experiment
		// Child Class reference variable = new Child Class();
		Child rv_c=new Child();
		System.out.println(" \n 6. Child rv_c >>> : "+rv_c);
		rv_c.Parents_method();
		rv_c.Child_method();

		// Second Experiment
		// Parents Class reference variable = new Parents Class();
		Parents rv_p=new Child();
		System.out.println(" \n 11. Parents rv_p >>> "+rv_p);
		rv_p.Parents_method();
		// rv_p.Child_method();

		// Second Experiment issue
		// How to use rv_p.Parnets_Method() ??

		// Class Casting method 1
		Child rv_ca=(Child)rv_p;
		rv_ca.Child_method();
        
		// Class Casting method 2
		Object obj=rv_p;
		Object obj_1=obj;
		Child rv_ca2 = (Child)obj_1;
		rv_ca2.Child_method();

		// Class Casting method 3
		Object obj_2=(Object)rv_p;
		// == Object obj_2=rv_p;
		Child rv_ca3=(Child)obj_2;
		rv_ca3.Child_method();
	}
}
```
> **First Experiment**

위의 코드가 있을 때, 주석 First Experiment 아래에서 Child rv_c=new Child(); 로 자식클래스 생성자를 인스턴스해서 자식클래스 참조변수로 선언할 경우, 6번까지 아무문제 없이 실행됩니다.

> **Second Experiment**

그러나, 주석 Second Experiment에서는 Parents rv_p=new Child(); 로 자식클래스 생성자를 인스턴스해서 부모클래스 참조변수로 선언할 경우, 부모클래스 참조변수에서 자식 클래스의 함수를 사용하지 못 합니다.

```
Java Compile issue

		error: cannot find symbol
		symbol:   method Child_method()
		location: variable rv_p of type Parents
		1 error
```        

이유는 생성자는 자식클래스 생성자로 생성해서 부모 생성자와 자식 생성자를 다 만들었는데, 참조변수를 부모 클래스에서 만들었기 때문에, 부모 클래스의 함수는 쓸 수 있는데, 자식 클래스의 함수를 사용하지 못하기 때문입니다.

### DownCasting 3가지 방법

따라서, 3가지 방법의 DownCasting을 사용하여 부모 클래스의 참조변수가 자식 클래스의 함수를 사용할 수 있게 하도록 하였습니다.

> **첫 번째 DownCasting 방법**

```java
		// Class Casting method 1
		Child rv_ca=(Child)rv_p;
		rv_ca.Child_method();
```
첫 번째 방법은 아래와 같습니다.

```javascript
자식클래스 자식클래스에서 만든 참조변수 = (자식클래스이름)부모클래스에서 만든 참조변수;
자식클래스에서 만든 참조변수.자식클래스의 함수();

```

부모클래스에서 만든 참조변수 앞에 (자식클래스이름)을 붙여준 다음 이를 자식클래스에서 참조변수를 만들어 자식클래스의 함수를 실행하였습니다.

> **두 번째 DownCasting 방법**

```java
		// Class Casting method 2
		Object obj=rv_p;
		Object obj_1=obj;
		Child rv_ca2 = (Child)obj_1;
		rv_ca2.Child_method();
```

**😓 두 번째와 세 번째 방법은 굉장히 어려운 방법이여서, 필자의 주관적인 견해가 반영되어있습니다. 이를 참고해서 읽어주시기 바랍니다.**

```javascript
조상클래스 조상클래스에서 만든 참조변수 = 부모클래스에서 만든 참조변수;
조상클래스 조상클래스에서 만든 다른 참조변수 = 조상클래스에서 만든 참조변수;
자식클래스 자식클래스에서 만든 참조변수 = (자식클래스이름) 조상클래스에서 만든 다른 참조변수;
```

1. 먼저, 부모클래스에서 만든 참조변수를 조상클래스에서 참조변수로 선언하여줍니다.

- Object는 java.lang.Object 클래스로, java.lang은 기본적으로 JAVA에 내장되어 있기 때문에 생략이 가능합니다.

2. 여기서 두 번째 줄에 조상클래스에서 만든 참조변수는 부모클래스에서 만든 참조변수를 조상클래스에서 만든 참조변수로 선언하여 준 참조변수입니다.

3. 마지막 줄에 (자식클래스이름)을 사용한 이유는 조상클래스에서 만든 다른 참조변수가 첫 번째 줄 우항에 부모클래스에서 만든 참조변수이기 때문입니다.

- 후손의 함수를 쓸 때는 (자식클래스이름)을 사용해야 합니다.

> **세 번째 DownCasting 방법**

```java
		// Class Casting method 3
		Object obj_2=(Object)rv_p;
		// == Object obj_2=rv_p;
		Child rv_ca3=(Child)obj_2;
		rv_ca3.Child_method();
```
세 번째 방법은 아래와 같습니다.

```javascript
조상클래스 조상클래스에서 만든 참조변수 = (조상클래스)부모클래스에서 만든 참조변수;
자식클래스 자식클래스에서 만든 참조변수 = (자식클래스이름)조상클래스에서 만든 참조변수;
```

1. 먼저, 부모클래스에서 만든 참조변수를 조상클래스에서 참조변수로 선언하여줍니다.

이 때, (Object)를 쓰는 이유는 소스코드를 작성하는 프로그래머가 눈으로 확인하기 위함이라는 개인적인 추측을 합니다. 

- Object obj_2=rv_p;으로 해도 자식클래스 Child의 함수를 사용하는데 아무문제가 없었기 때문입니다.

2. 조상클래스에서 만든 참조변수에 (자식클래스이름)을 써준뒤, 이를 자식클래스에서 참조변수로 선언하여 줍니다. 

- 이 때 조상클래스에서 만든 참조변수는 부모클래스에서 만든 참조변수를 대입하여 선언했기 때문에 자식클래스의 함수를 사용하기 위해 (자식클래스이름)을 써줘야 합니다.

> **3가지 DownCasting 결과**

```javascript
8 or 13. Child Method
```

3가지 방법 전부 자식 클래스에 있는 함수가 실행되어 위의 코드가 정상적으로 출력되는 것을 볼 수 있습니다.

> **그냥 처음부터 자식클래스 자식클래스에서 만든 참조변수 = new 자식클래스이름(); 하면 안 되나요?**

물론 그래도 원하는 값을 출력하는데에는 큰 문제가 없습니다. 다만, 위에서 DownCasting을 해야하는 이유에 대해 포스팅 했듯, 자원을 사용하기 위해 준비해야 하는 양이 다르고, 이를 위해 전력이라는 비용이 더 많이 소모됩니다.

따라서, DownCasting 규칙을 통해 **부모클래스 부모클래스에서 만든 참조변수 = new 자식클래스이름();** 으로 소스코드를 작성해야 전력 비용을 더 아낄 수 있습니다. 😀


## 추상 클래스

> **추상 클래스는 변수와 추상함수, 일반함수로 구성되어 있는 클래스를 의미합니다.**

추상 클래스는 일반 클래스와 다르게 블록이 없는 함수들이 존재합니다.

추상 클래스에서 추상 메서드(추상 함수)는 상속관계의 다른 클래스에서 작업한 메서드의 결과를 가지고 와서, 적용시킵니다.

- 추상 클래스의 키워드는 abstract 입니다.

> **간단한 코드 실습**

```java
package a.b.c.ch2;

abstract class Abstract_1{
	abstract int add();
	abstract String eat();
	int add_1(){
		return 1;
	} 
} 

class Abstract_2 extends Abstract_1{
	int add(){
		return 1+2;
	} 

	String eat(){
		return "class Abstract_2의 String eat() method";
	} 
} 

public class Abstract_p{
	public static void main(String args[]){
		System.out.println("\n 1. Abstract_p main 함수 시작");
		Abstract_p rv= new Abstract_p();
		System.out.println("\n 2. Abstract_p rv >>> : "+rv);

		Abstract_2 rv_1 = new Abstract_2();
		System.out.println("\n 3. Abstract_2 rv_1 >>> : "+rv_1);
		int add=rv_1.add();
		System.out.println("\n 4. Abstract_2 add() method >>> : "+add);
		String eat=rv_1.eat();
		System.out.println("\n 5. Abstract_2 eat() method >>> : "+eat);
        int add_1=rv_1.add_1();
		System.out.println("\n 6. Abstract_1 add_1() method >>> : "+add_1);
	} 
} 
```

**4번 출력 내용 >>> 3** 
**5번 출력 내용 >>> class Abstract_2의 String eat() method**
**6번 출력 내용 >>> 1**

4~6번 출력내용이 나오는 이유는 다음과 같습니다.

```javascript
추상클래스인 Abstract_1의 추상 메서드인 add()와 eat()은 추상클래스와 상속관계에 있는 일반 클래스인 Abstract_2에서의 일반 메서드인 add(){}와 eat(){}의 결과를 가져옵니다.

추상클래스인 Abstract_1의 일반 메서드인 add_1(){}는 결과값을 출력시킵니다.
```
### 추상 클래스 코드 실습

> **A_Computer 추상 클래스**

```java
package a.b.c.ch2;

public abstract class A_Computer {

	public abstract void display();
	public abstract void typing();

	public void turnOn() {
		System.out.println("전원을 켭니다.");
	}
	public void turnOff() {
		System.out.println("전원을 끕니다.");
	}
}
```

> **A_Computer 추상클래스와 상속관계인 A_DeskTop 클래스**

```java
package a.b.c.ch2;

public class A_DeskTop extends A_Computer{

	@Override
	public void display() {
		System.out.println("DeskTop display()");
	}

	@Override
	public void typing() {
		System.out.println("DeskTop typing()");		
	}
}
```

> **A_Computer 추상클래스와 상속관계인 A_NoteBook 추상클래스**

```java
package a.b.c.ch2;

public abstract class A_NoteBook extends A_Computer{

	@Override
	public void display() {
		System.out.println("NoteBook display()");
	}
}
```

> **A_NoteBook 추상클래스와 상속관계인 A_MyNoteBook 클래스**

```java
package a.b.c.ch2;

public class A_MyNoteBook extends A_NoteBook{

	@Override
	public void typing() {
		System.out.println("MyNoteBook typing()");		
	}
}
```

> **main함수가 있는 A_ComputerTest 클래스**

```java
package a.b.c.ch2.abc;

import a.b.c.ch2.A_DeskTop;
import a.b.c.ch2.A_MyNoteBook;

public class A_ComputerTest {

	public static void main(String args[]) {
		
		A_DeskTop ad = new A_DeskTop();
		ad.display();
		ad.turnOn();
		ad.turnOff();

		A_MyNoteBook am = new A_MyNoteBook();
		am.display();
		am.typing();
		am.turnOn();
		am.turnOff();

	}
}
```

java 파일만 무려 5개나 됩니다.

> **java 파일 관계 시각화**

![](https://images.velog.io/images/yunyoseob/post/505628ce-6533-4108-a5a4-4f9127d2f2ab/image.png)

- 관계 시각화의 경우 UML 다이어그램으로 관계를 시각화 할 수 있으나 추상 클래스 설명에 집중하기 위해 이번 포스팅에서는 다루지 않습니다.😂

> **실행 방식 해설**

![](https://images.velog.io/images/yunyoseob/post/edb20987-b6ac-4fef-aee7-2c5e26bb4b05/image.png)

![](https://images.velog.io/images/yunyoseob/post/81176af2-a86f-4faf-bd68-1706848c88e8/image.png)

> **출력 결과**

```javascript
DeskTop display()
전원을 켭니다.
전원을 끕니다.
NoteBook display()
MyNoteBook typing()
전원을 켭니다.
전원을 끕니다.
```

> **추가적으로 추상 클래스 쓰는 사례 : final**

추상 클래스는 new 키워드로 인스턴스가 되지 않습니다. 따라서, final 키워드를 작성하여 코드를 만든 경우, 해당 클래스를 추상클래스로 지정하여, 이를 외부에서 import한 뒤, new 키워드로 생성자를 인스턴스 하지 못하게 할 수 있습니다.

```javascript
추상클래스이름 참조변수 = new 추상클래스이름();
// error: 추상클래스이름 is abstract; cannot be instantiated
```

## 인터페이스 클래스

마지막으로 인터페이스 클래스에 대해 간단하게 포스팅한 뒤, 이번 포스팅은 마치도록 하겠습니다. 

> **유의사항**

**1. class 클래스이름 => 클래스이름 뒤에 Impl를 붙여줘야 합니다.**

**2. class 클래스이름+Impl 뒤에 implements 키워드를 쓰고 interface 인터페이스클래스이름을 작성하여 줍니다.**

**3. 2번을 작성하여 주었으면, interface 인터페이스클래스이름{}을 작성한 후, 구현부(함수블록{} 안의 내용)에 블록이 없는 함수를 작성하여 줍니다.**

**4. 2번과 3번은 인터페이스 클래스의 한 세트입니다.**

```javascript
class 클래스이름 + Impl implements 인터페이스클래스이름
interface 인터페이스클래스이름{ 블록이 없는 함수(); }
```

### 인터페이스 클래스 코드 실습

마지막으로 인터페이스 클래스 코드를 실습하고, 이번 포스팅을 마무리 하도록 하겠습니다. 😀

```java
package a.b.c.ch2;

// 첫 번째 implements
class Interface_B_Impl implements Interface_B{
	public void inter_b(){
		System.out.println("Interface_B_Impl.inter_b() 함수 실행");		
	} 
}

interface Interface_B{
	public void inter_b();
} // Interface_B interface


// 두 번째 implements
class Interface_A_Impl implements Interface_A{
	public void inter_a(){
		System.out.println("Interface_A_Impl.inter_a() 함수 실행");
	} 
} 

interface Interface_A{
	public void inter_a();
} 

public class Interface_p{
	public static void main(String args[]){
		// 부모 인터페이스 클래스 선언 참조변수 = new 자식클래스();
		Interface_A ia=new Interface_A_Impl();
		ia.inter_a();
        Interface_B ib=new Interface_B_Impl();
		ib.inter_b();

		/*
		사용을 지양
		// 자식클래스선언 참조변수 = new 자식클래스();
		Interface_A_Impl iai = new Interface_A_Impl();
		iai.inter_a();
        
        Interface_B_Impl ib=new Interface_B_Impl();
		ib.inter_b();
        */
		
	} 
} 
```

### 인터페이스 클래스 코드 실습 해설

> **Interface_A ia=new Interface_A_Impl();**

Interface_A_Impl() 생성자를 new 키워드를 통해 인스턴스하고 이를 Interface_A 인터페이스클래스에서 참조변수를 만듭니다.

> **ia.inter_a();**

interface Interface_A에서 추상 메서드인 inter_a를 class Interface_A_Impl implements Interface_A에서 시그니처함수를 찾아 "Interface_A_Impl.inter_a() 함수 실행"를 출력합니다.

> **Interface_B ib=new Interface_B_Impl();**

interface Interface_B에서 추상 메서드인 inter_b를 class Interface_B_Impl implements Interface_B에서 시그니처함수를 찾아 "Interface_B_Impl.inter_b() 함수 실행"을 출력합니다.

```java
		/*
		사용을 지양
		// 자식클래스선언 참조변수 = new 자식클래스();
		Interface_A_Impl iai = new Interface_A_Impl();
		iai.inter_a();
        
        Interface_B_Impl ib=new Interface_B_Impl();
		ib.inter_b();
        */
```

해당 코드를 사용을 지양이라고 쓰고 주석처리한 이유는 DownCasting에서의 new 인스턴스 연산자로 자식클래스 생성자를 만든 뒤, 자식클래스에서 참조변수를 만들지 않고 부모클래스에서 참조변수를 만드는 이유와 같습니다.

**이상으로 JAVA : Downcasting, 추상클래스, 인터페이스클래스 포스팅을 마치도록 하겠습니다. 😀**
