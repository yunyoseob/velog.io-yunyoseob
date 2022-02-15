안녕하세요 😀 오늘은 JAVA에서 Anotation중 @Override와 super에 대해 포스팅해보도록 하겠습니다.

## 들어가기 전에..

저번 포스팅 [JAVA : 상속, 생성자, 정보의 은닉화](https://velog.io/@yunyoseob/JAVA-%EC%83%81%EC%86%8D-%EC%83%9D%EC%84%B1%EC%9E%90-%EC%A0%95%EB%B3%B4%EC%9D%98-%EC%9D%80%EB%8B%89%ED%99%94)에서 생성자에 대해 다뤘던 것 기억 나시나요?

생성자는 워낙 중요한 내용이여서, 추가적인 내용을 더 포스팅해보도록 하겠습니다.

> **생성자란 new 키워드를 사용해서 어떤 클래스에 대한 오브젝트(인스턴스)를 생성할 때 자동적으로 호출되어 실행되는 특수한 메소드입니다. 생성자는 오브젝트 생성시 한 번만 수행되므로 주로 멤버 변수의 초기화 작업 등에 이용됩니다.**

> **생성자는 기본적으로 메소드이기 때문에 메소드의 특징을 그대로 가지고 있습니다.**

|**생성자(Constructor) 작성 규칙**|
|----------|
|**생성자의 이름은 클래스의 이름과 동일하게 붙입니다.**|
|**(클래스의 이름은 대문자로 시작하는 것이 관례이므로, 생성자는 메소드임에도 불구하고 대문자로 시작하게 됩니다.)**|
|**생성자의 리턴형은 지정하지 않습니다. (void 또한 쓰면 안 됩니다.)**|
|**오버로드된 형태로 여러 개의 생성자를 작성할 수 있습니다.**|

**✔ 생성자의 특징**

**1. 생성자를 만드는 이유는 멤버변수를 초기화 하기 위함입니다. 생성자에는 매개변수가 있는 생성자가 있고, 매개변수가 없는 생성자가 있습니다.**

**2. 생성자를 따로 설정하지 않으면 자바가상머신(JVM)이 기본 생성자를 만듭니다.**

- 해당 과정은 javap NameSpace로 확인 할 수 있습니다.
- new라는 키워드는 생성자를 만들 거라고 JVM에게 알려주는 키워드 입니다.
- 생성자를 만드는 일은 JVM이 합니다.
- 생성자는 멤버변수를 초기화 하는 역할을 합니다.

**3. 매개변수가 있는 생성자의 경우, 매개변수(Parameter)에 알맞게 인수(Arguments)를 넣어줘야 합니다.**

# @Override

> **Annotation**

@Override는 Annotation중 하나입니다. Annotation은 @ 기호와 함게 사용하며 @Annotation 이름으로 표현합니다. JAVA에서 제공하는 Annotation은 컴파일러에게 특정한 정보를 제공해주는 역할을 합니다. 

- 예시로, 시그니처가 다르다면 컴파일 오류를 발생시켜, 프로그래머의 실수를 막아줍니다.
- 시그니처의 예시로 함수의 시그니처는 **접근제한자 수정자 리턴형 함수이름**까지 같은 함수를 의미합니다.
- 생성자의 경우, 생성자의 시그니처가 같고 매개변수가 달라야 생성자 오버로딩(constructor overloading)이 되어, overload 선언된 생성자를 호출할 수 있습니다.

**Annotation 종류**

|**애노테이션**|**설명**|
|---|---|
|@Override|재정의된 메서드라는 정보 제공|
|@FunctionalInterface|함수형 인터페이스라는 정보 제공|
|@Deprecated|이후 버전에서 사용되지 않을 수 있는 변수, 메서드에 사용됨.|
|@SuppressWarnings|특정 경고가 나타나지 않도록 함|

### 코드 실습을 통해 보는 상속 구조

@Override는 상속 구조에 있어서, 컴파일러에게 재정의된 메서드라는 정보를 제공해주는 애노테이션 입니다.

저번 포스팅 [JAVA : 상속, 생성자, 정보의 은닉화](https://velog.io/@yunyoseob/JAVA-%EC%83%81%EC%86%8D-%EC%83%9D%EC%84%B1%EC%9E%90-%EC%A0%95%EB%B3%B4%EC%9D%98-%EC%9D%80%EB%8B%89%ED%99%94)에서 상속에 대해 다뤘었는데, 코드 예시를 통해 상속구조를 추가적으로 포스팅해보도록 하겠습니다. 😊

> **상속 실습 코드**

```java

package a.b.c.ch2;

class Dead_Great_Grand_Parents{
	Dead_Great_Grand_Parents(){
		System.out.println("\n 10. Dead_Great_Grand_Parents 생성자"); 
	}
	void p_0(){
		System.out.println("\n 11. p_0 함수");
	} 
} 

class Great_Grand_Parents{
	Great_Grand_Parents(){
		System.out.println("\n 2. Great_Grand_Parents 생성자");
	} 
	void p_1(){
		System.out.println("\n 8. p_1 함수");
	}
} 

class Grand_Parents extends Great_Grand_Parents{
	Grand_Parents(){
		System.out.println("\n 3. Grand Parents 생성자");
	} 
	void p_2(){
		System.out.println("\n 7. p_2 함수");
	} 
}

class Parents extends Grand_Parents{
	Parents(){
		System.out.println("\n 4. Parents 생성자");
	}
	void p_3(){
		System.out.println("\n 6. p_3 함수");
	}
}

public class Inheritance_p{
	public static void main(String args[]){
		System.out.println("\n 1. Inheritance_p main 함수 시작");
		Parents papa = new Parents();
		System.out.println("\n 5. rv 참조변수 주소값 >>> : "+papa);
		papa.p_3();
		papa.p_2();
		papa.p_1();
		// papa.p_0();
		// father가 상속 못 받았음. 따라서, 에러가 출력됨.
		//  error: cannot find symbol
		//  location: variable papa of type Parents

		System.out.println("\n 9. Dead_Great_Grand_Parents 소환하기");
		Dead_Great_Grand_Parents dead = new Dead_Great_Grand_Parents();
		dead.p_0();		
	} 
} 
```
>**출력결과와 설명**

![](https://images.velog.io/images/yunyoseob/post/8b480e49-a024-4a98-a4a2-3b787621970f/image.png)

다음과 같은 코드가 있을 때, Parents 클래스는 Grand_Parents 클래스에 상속을 받고, Grand_Parents 클래스는 Great_Grand_Parnets에 상속을 받습니다. Great_Grand_Parents는 최고 조상인 java.lang.Object에서 상속을 받습니다. 

반면, Dead_Great_Grand_Parents 클래스는 그 어떤 클래스도 상속을 해주고 있지 않고, 최고 조상인 java.lang.Object에서만 상속을 받고 있습니다.

따라서, 1번부터 8번까지는 상속만 잘 받으면, 아무 문제 없이 잘 출력됩니다.

```java
Parents papa = new Parents();
papa.p_0();
```
그러나 위의 코드를 실행할 경우, father가 Dead_Great_Grand_Parents에게 상속 못 받았기 때문에 다음과 같은, 에러가 출력됩니다.

```
error: cannot find symbol
location: variable papa of type Parents
``` 

따라서, 9번부터 11번까지는 다음과 같이 따로 객체를 생성하여, 함수를 실행시켜야 합니다.

```java
Dead_Great_Grand_Parents dead = new Dead_Great_Grand_Parents();
dead.p_0();
```

## 상속 구조에서 @Override

JAVA는 위의 상속 실습 코드처럼 사용하고자 하는 리소스를 상속을 받아 실행합니다.

따라서, 자식 클래스에서 해당 내용이 없으면 부모 클래스로 가서 해당 내용을 찾고, 부모 클래스에 없으면 조부모 클래스로, 조부모 클래스에도 없으면, 조상 클래스인 java.lang.Object에서 해당 내용을 찾아 컴파일을 하고 실행을 합니다.

![](https://images.velog.io/images/yunyoseob/post/ac8befab-a59e-4135-a983-084127ffaf78/image.png)

여기서, @Override는 조상까지 찾아가서 실행시키지말고, 재정의한 부분부터 코드를 진행하라고 정해줄 때 사용하는 Annotation입니다.

- 가령, 부모 클래스에서 재정의를 하였으면, 자식, 부모, 조부모, 조상까지 찾으러 올라가지 말고, 부모 클래스에서 재정의를 했으니, 부모 클래스에서 찾아 실행하라는 의미입니다.

## 코드 실습을 통해 보는 @Override

> **부모 클래스의 코드**

```java
package a.b.c.ch2.aa;

public class Class_A extends java.lang.Object{
	public Class_A(){
		System.out.println("Class_A() 생성자 >>> : ");
		}
	public Class_A(String s){
		System.out.println("Class_A(String s 생성자 >>> : "+s);
	}
	public void class_a_1(){
		System.out.println("Class_A().class_a_1() 함수 >>> : ");
		
	} 
	public String class_a_2(){
		System.out.println("Class_A().class_a_2() 함수 >>> : ");
		return "class_a_2() 함수 >>> : ";
	} 
}
```

부모 클래스에는 4가지의 리소스가 있습니다. 

```
1. 매개변수가 없는 생성자
2. 매개변수가 있는 생성자
3. 리턴값이 없는 함수
4. 리턴값이 있는 함수
```

자식 클래스는 부모 클래스에서 상속받아, 부모 클래스의 있는 자원을 쓰도록 할 건데, 이 때, @Override를 통해 조상 클래스로 부터 대대손손 내려오는 내용을 재정의하도록 하겠습니다.

> **자식 클래스의 코드**

```java

package a.b.c.ch2.aa;

import a.b.c.ch2.aa.Class_A;

// Class_A라는 부모에게서 상속받은
// Inherit_p_1라는 자식 클래스이다.
public class Inherit_p_1 extends Class_A{
	
	// 실험 1
	public String toString(){
		return "Class_A().toString() 함수 >>> : ";
	}

	// 실험 2
	@Override
	public String toString(){
		return "Inherit_p_1에서 Override로 재정의됐습니다.";
	} // java.lang.Object 조상에 있는 클래스의 함수를
		// 후손인 Inherit_p_1 클래스가 재정의 
		
	// 실험 3
	@Override
	public void class_a_1(){
		System.out.println("Hi");
	} 

	public static void main(String args[]){
		Inherit_p_1 rv=new Inherit_p_1();
		System.out.println("\n 1. Inherit_p_1 rv=new Inherit_p_1();에서 참조변수 rv의 주소값 >>> : "+rv);
		System.out.println("\n 2. rv.toString() >>> : "+rv.toString());
		System.out.println("\n 3. rv.getClass().getName() >>> : "+rv.getClass().getName());
		rv.class_a_1();
	}
} 
```

### 실험 1만 진행

- **실험 2,3은 전부 주석처리**

> **출력 결과**

![](https://images.velog.io/images/yunyoseob/post/5f6745bd-70dc-4c53-a30e-e7e18e995dd9/image.png)

실험 1만 진행시키면, 부모클래스의 Class_A() 생성자가 생성되어,  **Class_A() 생성자**가 출력됩니다.

> **✔ 1번 출력 해설**

그 이후, 1번 Inherit_p_1 rv=new Inherit_p_1();에서 참조변수 rv의 주소값은 Class_A().toString() 함수 >>> :가 나옵니다.  

이유는 원래 java.lang.Object에서 주소값이 설정되면 Inherit_p_1@15db9742으로 나와야 하는데, Inherit_p_1에서 public String toString()함수를 따로 만들었기 때문입니다.

> **✔ 2번 출력 해설**

rv.toString()은 **Class_A().toString() 함수 >>> :**가 출력된다. 이유는 참조변수의 주소값을 Inherit_p_1에서 public String toString(){} 함수를 통해 출력시켰기 때문입니다.

> **✔ 3번 출력 해설**

rv.getClass().getName()은 **a.b.c.ch2.aa.Inherit_p_1**가 출력됩니다. getClass().getName()은 Name Space를 출력하여 줍니다.

> **✔ rv.class_a_1()**

**Class_A().class_a_1() 함수 >>> :**가 출력됩니다. 이유는 부모 클래스인 Class_A의 public void class_a_1() 함수를 호출했기 때문입니다.

### 실험 2만 진행
- **실험 1,3은 전부 주석처리**

> **출력 결과**

![](https://images.velog.io/images/yunyoseob/post/da2973e5-781d-425b-b4d2-651f7a397dc8/image.png)

> **✔ 1번 출력 해설**

**Inherit_p_1에서 Override로 재정의됐습니다.** 가 출력됩니다. 이유는 실험1과 동일합니다.

> **✔ 2번 출력 해설**

마찬가지로, **Inherit_p_1에서 Override로 재정의됐습니다.** 가 출력됩니다.

> **✔ 3번 출력 해설**

실험1과 마찬가지로 **a.b.c.ch2.aa.Inherit_p_1**가 출력됩니다.

> **✔ rv.class_a_1()**

실험1과 마찬가지로 **Class_A().class_a_1() 함수 >>> :**가 출력됩니다.

### 실험 3만 진행
- **실험 1,2는 전부 주석처리**

> **출력 결과**

![](https://images.velog.io/images/yunyoseob/post/fc50c831-1113-4089-bb39-fac97603bc3a/image.png)

> **✔ 1번 출력 해설**

따로 해당 클래스에서 public String toString() 함수를 사용하지 않았기 때문에, 조상인 java.lang.Object에서 해당 함수가 실행 되었고, **a.b.c.ch2.aa.Inherit_p_1@15db9742**가 출력되었습니다.

> **✔ 2번 출력 해설**

마찬가지로, **a.b.c.ch2.aa.Inherit_p_1@15db9742**가 출력됩니다.

> **✔ 3번 출력 해설**

실험 1,2와 동일하게 **a.b.c.ch2.aa.Inherit_p_1** (Name Space)가 출력됩니다.

> **✔ rv.class_a_1()**

실험 1,2와 다르게 Hi가 출력됩니다. 이유는 부모 클래스에서 public void class_a_1()함수를 재정의 하였기 때문입니다. (@Override)

# super

super는 부모 클래스에서 특정 함수를 실행하고 싶을 때 사용하는 키워드입니다. Class_A라는 부모 클래스로 부터 또 하나의 자식 클래스 코드를 만들어 실습을 해보도록 하겠습니다.

> **자식 클래스의 코드**

```java
package a.b.c.ch2.aa;

import a.b.c.ch2.aa.Class_A;

// Class_A라는 부모에게서 상속받은
// Inherit_p_2라는 자식 클래스이다.
public class Inherit_p_2 extends Class_A{
	public Inherit_p_2(){
		super();
		System.out.println("\n 1. Inherit_p_2() 생성자 >>> : "+super.class_a_2());
	} 
	public Inherit_p_2(String s){
		super(s);
		System.out.println("\n 2. Inherit_p_2(String s) 생성자 >>> : "+s);
	}

	@Override
	public String toString(){
		return "Hello";
	}

	@Override
	public void class_a_1(){
		System.out.println("Hi");
	}

	public static void main(String args[]){
		Inherit_p_2 rv= new Inherit_p_2();
		System.out.println("\n 3. Inherit_p_2 rv= new Inherit_p_2(); 에서 참조변수 주소값 >>> : "+rv);
		System.out.println("\n 4. rv.toString() >>> : "+rv.toString());
		System.out.println("\n 5. rv.getClass().getName() >>> : "+rv.getClass().getName());
		rv.class_a_1();

		Inherit_p_2 rv_1=new Inherit_p_2("NiceToMeetYou");
		System.out.println("\n 6. Inherit_p_2 rv_1 = new Inherit_p_2(NiceToMeetYou); 에서 참조변수 주소값 >>> : "+rv_1);

	}
} // Inherit_p_2 class
```

> **출력 결과**

![](https://images.velog.io/images/yunyoseob/post/12f9802c-94f5-48ef-8ef4-aa35b2429b01/image.png)

super는 부모 클래스에 특정 자원을 실행하고 싶을 때 사용합니다. super();는 생성자 블록 내에 주석을 제외한 첫 줄로 써야 합니다.

만약, 부모클래스인 Class_A에서 class_a_2()를 사용하고 싶으면, 생성자 내에서 super.class_a_2()으로 자원을 가져오면 됩니다.

### 코드 해설

> **Inherit_p_2 rv= new Inherit_p_2();**

Inherit_p_2 rv= new Inherit_p_2();으로 객체를 생성한 결과 super 키워드를 통해, Class_A의 매개변수가 없는 생성자를 생성 후, class_a_2()의 함수를 가져오므로,

```
Class_A() 생성자 >>> :
Class_A().class_a_2() 함수 >>> :
```

위의 내용이 출력됩니다.

> **1. Inherit_p_2() 생성자 >>> :**

super.class_a_2()가 출력된 이후, class_a_2의 리턴값인 **"class_a_2() 함수 >>> : "**가 출력됩니다.

> **3. Inherit_p_2 rv= new Inherit_p_2(); 에서 참조변수 주소값 >>> :**

Class_A(부모클래스)의 자식클래스인 Inherit_p_2에서 @Override로 public String toString() 함수를 재정의 하였습니다. 해당 함수의 리턴값이 "Hello"이기 때문에, Hello가 출력됩니다. 4번 결과는 3번 결과와 동일합니다.

> **5. rv.getClass().getName()**

Name Space인 a.b.c.ch2.aa.Inherit_p_2가 출력됩니다.


> **2. Inherit_p_2(String s) 생성자 >>> :**

**Inherit_p_2 rv_1=new Inherit_p_2("NiceToMeetYou");**

이번에는 매개변수가 있는 생성자에 NiceToMeetYou를 입력 후, 출력시켜보도록 하겠습니다.

public Inherit_p_2(String s)인 매개변수가 있는 생성자로 들어가므로, NiceToMeetYou가 출력됩니다. 

- **1,2,3,4,5번 순서대로 출력이 안 되는 이유는 생성자가 다르기 때문입니다.**

> **6. Inherit_p_2 rv_1 = new Inherit_p_2(NiceToMeetYou); 에서 참조변수 주소값 >>> :**

자식 클래스에서 public String toString() 함수를 재정의 하고, 리턴값을 Hello로 정했으므로, Hello가 출력됩니다.

**이상으로, JAVA : @Override, super 포스팅을 마치도록 하겠습니다. 😁**
