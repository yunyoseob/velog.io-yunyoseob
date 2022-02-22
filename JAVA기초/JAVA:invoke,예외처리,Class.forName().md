안녕하세요. 🙂 오늘은 JAVA : invoke, 예외처리, Class.forName()에 대해 알아보도록 하겠습니다.

## invoke

invoke는 사전적 의미는 다음과 같습니다.

![](https://images.velog.io/images/yunyoseob/post/da320189-7906-4a45-a91a-d4dbe6b42002/image.png)

java에서 invoke는 호출하는 것을 의미합니다. 

### 코드를 통해 살펴보는 invoke

```java
package a.b.c.prac1;

public class Invoke_p {
	public Invoke_p() {
		System.out.println("저는 Invoke_p() 기본 생성자입니다.");
		aM();
	}
	
	void aM(){
		System.out.println("저는 aM() 함수입니다.");
		bM();
	}
	
	void bM(){
		System.out.println("저는 bM() 함수입니다.");
		cM();
	}
	
	void cM(){
		System.out.println("저는 cM() 함수입니다.");
	}
	public static void main(String[] args) {
		new Invoke_p();
	}

}
```

다음과 같은 코드가 있을 시, 호출 순서는 다음과 같습니다.

|호출순서|
|---|
|main method에서 Invoke_p() 생성자 호출|
|Invoke_p() 생성자에서 aM() method 호출|
|aM() method에서 bM() method 호출|
|bM() method에서 cM() method 호출|

- 만일 이 때, cM() method에서 aM() method를 호출하면, 무한 루프로 돌게 됩니다.

> **출력결과**

```javascript
1. 저는 Invoke_p() 기본 생성자입니다.
2. 저는 aM() 함수입니다.
3. 저는 bM() 함수입니다.
4. 저는 cM() 함수입니다.
```

> **🤔 만약, 이 때, aM() 함수 invoke를 aaM() 함수 invoke로 바꾸면 어떻게 될까요?**

```javac
Exception in thread "main" java.lang.Error: Unresolved compilation problem: 
	The method aaM() is undefined for the type Invoke_p
 ```
 
 에러가 나게 됩니다. 이 때, 에러가 출력되는 순서는 호출 순서의 역순으로 진행됩니다.
 
 |에러 순서|
 |----|
 |1. Invoke_p() 기본생성자에서 aaM() 함수를 호출하는 과정의 에러를 출력|
 |2. Invoke_p() 기본생성자 호출 과정의 에러를 출력|
 
>  **🤔 bM() 함수 invoke를 bbM() 함수 invoke, cM() 함수 invoke를 ccM() 함수 invoke로 바꾸어보기**
 
 **bM() invoke => bbM() invoke**
 
 |에러 순서|
 |----|
 |1. aM() 함수에서 bbM() 함수를 호출하는 과정의 에러를 출력|
 |2. Invoke_p() 기본생성자에서 aM() 함수를 호출하는 과정의 에러를 출력|
 |3. Invoke_p() 기본생성자 호출 과정의 에러를 출력|
 
 **cM() invoke => ccM() invoke**
 
 |에러 순서|
 |----|
 |1. bM() 함수에서 ccM() 함수를 호출하는 과정의 에러를 출력|
 |1. aM() 함수에서 bM() 함수를 호출하는 과정의 에러를 출력|
 |2. Invoke_p() 기본생성자에서 aM() 함수를 호출하는 과정의 에러를 출력|
 |3. Invoke_p() 기본생성자 호출 과정의 에러를 출력|


다시 한 번 호출 순서를 보도록 하겠습니다.

|호출순서|
|---|
|main method에서 Invoke_p() 생성자 호출|
|Invoke_p() 생성자에서 aM() method 호출|
|aM() method에서 bM() method 호출|
|bM() method에서 cM() method 호출|

**invoke의 순서의 역순대로 에러가 출력되는 것을 알 수 있습니다.**

# 예외처리

> **코드를 통해 살펴보는 덧셈 실습 코드**

```java
package a.b.c.prac1;

public class Exception_p {

	public static void main(String[] args) {
		String s0=args[0];
		String s1=args[1];
		
		int x=Integer.parseInt(s0);
		int y=Integer.parseInt(s1);
		
		int z=x+y;
		
		System.out.println("x + y ="+z);
	}
}
```

eclipse에서 코드 화면에서 우클릭 후, Run As => Run Configurations 클릭한 뒤,

상단의 {Name : Exception_p}, Main 버튼 클릭 후, {Main : Class a.b.c.prac1.Exception_p}입력 후, Arguments의 Program argument에 값 4와 6을 입력하고 실행(Run)해보도록 하겠습니다.

> eclipse Arguments에서 4와 6 입력

![](https://images.velog.io/images/yunyoseob/post/f78735bc-42b4-422c-9627-0587d8159334/image.png)

**출력 결과 : x + y =10**


정상적으로 잘 출력 되는 것을 확인 할 수 있습니다. 그런데 만약 이 때, 4와 육을 입력하면 어떻게 될까요?

> eclipse Arguments에서 4와 육 입력

![](https://images.velog.io/images/yunyoseob/post/53bfb5ff-7909-4a88-83cb-8868d8573fe8/image.png)

**출력 결과: Exception in thread "main" java.lang.NumberFormatException: For input string: "육"**

에러가 나는 것을 볼 수 있습니다.

## Exception

🤔 위의 코드 출력 결과의 **java.lang.NumberFormatException**의 의미와 해당 과정을 예외처리해서 정상적으로 출력하고 싶으면 어떻게 해야 할까요??

[Java™ Platform Standard Ed. 8](https://docs.oracle.com/javase/8/docs/api/) 공식 api를 가서, java.lang => Exception을 클릭하시면 다음과 같은 화면을 볼 수 있습니다..

![](https://images.velog.io/images/yunyoseob/post/f66b2c05-86f8-4655-9373-6b113b8dfaa2/image.png)

Exception의 부모클래스인 Throwable 클래스로 가면 다음과 같은 화면을 보실 수 있습니다.

![](https://images.velog.io/images/yunyoseob/post/7288c707-9f8d-4ff1-9b23-5fe76d4257fc/image.png)

> **Throwable Class**

Throwable Classs는 크게 Error 클래스와  Exception 클래스로 나눌 수 있습니다. Error 클래스는 실행을 중단하는 최상위 클래스이고, Exception 클래스는 예외를 처리하는 최상위 클래스입니다.

> **✔ 예외처리에 대해 조금 더 알아보기**

java는 javac 클래스이름.java 명령어를 통해 컴파일 하는 과정과 java NameSpace로 실행하는 과정이 있습니다. 컴파일 하는 과정에서 생기는 오류를 Checked Exception이라고 하고, 컴파일하는 과정에서 문제가 없었으나, 실행과정에서 생기는 오류를 Unchecked Exception이라고 합니다.

|구분|Checked Exception|Unchecked Exception|
|---|---|--|
|처리 여부|반드시 예외를 처리해야 함|명시적인 처리를 강제하지 않음|
|확인 시점|컴파일 단계|실행 단계|
|예외발생시 트랜잭션 처리|roll-back 하지 않음|roll-back 함|
|대표 예외|Exception 클래스를 상속받은 하위클래스 중  Runtime Exception을 제외한 모든 예외 클래스 (IOException, SQLException)|RuntimeException 하위 예외 클래스 (NullPointerException, IllegalArgumentException, IndexOutOfBoundException, SystemException)|


> **NumberFormatException**

NumberFormatException 클래스를 java.lang의 Exceptions에서 찾아보면, 다음과 같은 화면을 볼 수 있습니다.

![](https://images.velog.io/images/yunyoseob/post/8f5bef22-ef59-40f4-843a-7b589b20fbad/image.png)

위의 코드는 문자 상수(문자 숫자)를 int형 자료로 변환하는 과정에서 NumberFormatException클래스로 가서, 출력 결과가 나타나고, 실행이 중단 된 것입니다. 

### try,catch,finally

이러한 에러는 try, catch, finally 키워드를 통해 예외처리방법으로 중단시키지 않고, 실행할 수 있습니다.

```java
package a.b.c.prac1;

public class Exception_p {

	public static void main(String[] args) {
		try {
		String s0=args[0];
		String s1=args[1];
		
		int x=Integer.parseInt(s0);
		int y=Integer.parseInt(s1);		
		int z=x+y;		
		System.out.println("x + y ="+z);
		}catch(Exception e){
        	System.out.println("에러 내용  : "+e);
			System.out.println("잘못 입력한 값  : "+e.getMessage());
		}finally {
		System.out.println("\n finish try && catch");
		}
		System.out.println("\n 더하기 프로그램을 종료합니다.");
	}
}
```

> **이전 코드를 위의 코드와 같이 바꾸었을 때 결과**

```javascript
에러 내용  : java.lang.NumberFormatException: For input string: "육"
잘못 입력한 값  : For input string: "육"

 finish try && catch

 더하기 프로그램을 종료합니다.
```

> **예외처리문을 통해 에러내용은 출력하되, 프로그램 실행은 시키도록 할 수 있습니다.**

```java
try{
	 // 실행시키고자하는 내용
   }catch(Exception e){
     // 예외처리된, Exception 자식 클래스이름과 함께 에러 내용을 보고 싶으면 >>> e
     // 단순히, 잘못 입력한 부분만 보고 싶을 때는 >>> e.getMessage()
     }finally{
   		// try-catch문이 끝나고 실행시키고 싶은 내용
   }
```

- finally 키워드는 대부분 생략이 가능합니다.

try문의 구현부에는 실행하고자 하는 내용, catch(Exception e)는 예외 클래스의 최상위 클래스인 Exception 클래스에서 참조변수를 지정한 뒤, 참조변수를 출력하여 specified detail message를 확인하거나, 

참조변수.getMessage() 명령어를 입력하여, Exception의 부모 클래스인 Throwable의 getMessage() 메서드를 통해 detail message를 확인 할 수 있습니다.

## Throw, Throws

> **Throw, Throws 실습 코드**

```java
package a.b.c.prac1;

// 사용자 정의 예외 클래스
@SuppressWarnings("serial")
class IDFormatException extends Exception{	
	public IDFormatException(String s) {
		super(s);
	}
}

// 사용자 정의 클래스
class IDFormatTest{	
		private String userID;	
		public String getUserID(){
			return userID;
		}	
		public void setUserID(String userID) throws IDFormatException{
			boolean aBool= userID==null;
			System.out.println("userID==null >>> "+aBool);
			if (userID==null){
				IDFormatException ide=new IDFormatException("아이디는 null일 수 없습니다.");
				throw ide;
			}else if (userID.length() < 8 || userID.length() >20){
				throw new IDFormatException("아이디는 8~20자 이하 입니다.");
			}
			this.userID = userID;	
		} 
} 
	
public class Throw_p1 {
	public static void main(String[] args) {
		IDFormatTest idt=new IDFormatTest();
		
		String userID = null;
		try {
			idt.setUserID(userID);
		}catch(IDFormatException i){
			System.out.println("i.getMessage() >>> : "+i.getMessage());	
		}
		
		userID="1234567";
		try {
			idt.setUserID(userID);
		}catch(IDFormatException i){
			System.out.println("i.getMessage() >>> : "+i.getMessage());
		}
		System.out.println("\n try-catch 끝");
	} 
} 
```

> **출력 결과**

```javascript
userID==null >>> true
i.getMessage() >>> : 아이디는 null일 수 없습니다.
userID==null >>> false
i.getMessage() >>> : 아이디는 8~20자 이하 입니다.

 try-catch 끝
```

> **해당 코드에서 throw와 throws의 의미와 역할**

**throws**

먼저, throws는 예외출력이 발생할 시 예외를 처리하는 클래스로 가서 예외를 처리하라는 의미로 사용됩니다.

**✔ throws Exception : Exception 클래스로 예외 내용을 내보내세요.**

위의 코드에서는 예외출력 사항을 IDFormatException 클래스로 내보내라고 지정하였습니다.
- @SuppressWarnings("serial")은 사전에 정해진 내용을 수정할 때 생기는 특정 경고가 나타나지 않도록 하는 Annotation입니다.
- Annotation 종류가 기술되어 있는 포스팅 자료 보기 >>>  [JAVA : @Override, super](https://velog.io/@yunyoseob/JAVA-Override-super)

**throw**

throw는 중단하라는 의미입니다.

**✔ throw : 중단하세요!!!!!**

> **위의 코드에서 throw 설명(userID가 null)**

|번호|설명|
|--|--|
|1|main 함수에서 IDFormatTest 클래스의 기본 생성자를 인스턴스 하여 호출한 뒤, 해당 클래스에 idt라는 참조변수에 선언합니다.|
|2|userID를 null로 초기화 한 뒤, idt.setUserID(userID) 명령어를 입력합니다.|
|3|아무값도 setUserID에 null값이 들어왔기 때문에, boolean aBool이 true로 콘솔창에 출력됩니다. (userID==null >>> true)|
|4|setUserID 메서드 안에서 매개변수로 들어온 인수값이 없을 경우, throws 키워드로 인해 에러가 날 경우 IDFormatException 클래스로 이동합니다.|
|5|IDFormatException의 매개변수가 있는 생성자를 "아이디는 null일 수 없습니다."라는 내용과 함께 인스턴스 합니다. 이 때, "아이디는 null일 수 없습니다."라는 내용은 super 키워드에 따라 부모클래스인 Exception으로 넘어갑니다.|
|6|throw 명령어에 따라 중단됩니다.|
|7|명령이 중단됨에 따라, try 문에서 예외처리 되어 catch문으로 넘어가는데, 이 때, IDFormatException 클래스에 i변수를 선언하여, i.getMessage()를 출력시킵니다. 이전 과정에서, "아이디는 null일 수 없습니다."로 Exception으로 보냈기 때문에, "i.getMessage() >>> : 아이디는 null일 수 없습니다."로 출력됩니다.|

> **참고 사항**

```javascript
throw new IDFormatException("오류 메시지"); 

==
  
IDFormatException ide = new IDFormatException("오류 메시지");
throw ide;
```

**쉽게 말해, throws는 예외일 때, "throws A일 때, A클래스로 가세요."라면, throw는 "당장 중지하세요~"의 의미로 받아들일 수 있다. throw에 의해 중단됨에 따라 try문에서 실행중이라면 catch문으로 넘어가게 된다.**

## Class.forName()

[Java™ Platform Standard Ed. 8](https://docs.oracle.com/javase/8/docs/api/) 공식 api를 가서, java.lang => Class로 간 다음 Ctrl+f를 눌러 forName을 검색하면 다음과 같은 결과가 나옵니다.

|Modifier and Type|Method and Description|
|---|---|
|static Class<?>|forName(String className) : Returns the Class object associated with the class or interface with the given string name.|

해당 내용에서 forName을 클릭하면, 다음과 같은 내용이 나옵니다.

```java
public static Class<?> forName(String className)
                        throws ClassNotFoundException

                    
Returns the Class object associated with the class or 
interface with the given string name. 
Invoking this method is equivalent to:
```

 해당 내용을 보면 throws ClassNotFoundException이 있습니다. 따라서, 해당 클래스에서 throw ClassNotFoundException 코드를 작성하지 않을 경우, Unhandled exception type ClassNotFoundException 경고가 나타납니다.
 
 > **Class.forName은 Class를 찾기 위해 사용하는 메서드입니다.**
 **+ 반드시 찾고자하는 Class가 이미 컴파일 되어있어야 찾을 수 있습니다!!**
 
 Class.forName을 메서드를 통해 클래스를 찾는 방법은 다음과 같습니다.
 
 ```java
 Class 참조변수1 = Class.forName("찾을 클래스의 NameSpace");
 
 NameSpace : 패키지이름.클래스이름
 ```
 
✔ Class.forName으로 Class를 찾은 이후, 해당 클래스의 자원을 쓰기 위해서는 newInstance()메서드를 통해 인스턴스해야 합니다.
 
 ```java
 찾을클래스 참조변수2 = (찾을클래스)참조변수1.newInstance();
 ```
 
그러나, 해당 명령어를 입력하면, 다음과 같은 경고가 나타납니다.
 
 ```javascript
 Unhandled exception type InstantiationException
 Unhandled exception type IllegalAccessException
 ```
 
이유는 Class 클래스에서 newInstance를 검색하여 찾아보면 다음과 같은 내용이 있기 때문입니다.

```javascript
public T newInstance()
              throws InstantiationException,
                     IllegalAccessException
```

이럴 경우, 예시로 A Class의 b method가 있다면, b method() 옆에 throws 명령어를 통해, 각 Exception들을 입력한 뒤 구현부를 작성하고, 

```java
public class A{
	public void b throws ClassNotFoundException,
    					 InstantiationException,
                         IllegalAccessException{
... 이하 생략                        
```

main 함수 옆에도 마찬가지로 throws 명령어를 통해 각 Exception들을 입력하고, 
main함수 안에서 new A.b(); 명령어 실행시 경고와 에러없이 정상적으로 작동합니다. 

```java
public static void main(String[] args) throws ClassNotFoundException,
											  InstantiationException,
                                              IllegalAccessException{
...이하 생략                                              
```

> **🤔 꼭 이렇게 작성해야 할까?**

### Class.forName() 실습 코드

사실 오늘 포스팅한 try, catch문을 잘 활용하면, 매번 throws로 번거롭게 작성할 필요없이, Class.forName() 코드를 활용할 수 있습니다.

Class.forName() 실습 코드를 마지막으로 이번 포스팅을 마치도록 하겠습니다.

> **사용자 정의 클래스**

```java
package a.b.c.prac1;

public class ForNameSample {
	// 기본 생성자
	ForNameSample(){
		System.out.println("ForNameSample 기본 생성자 ");
		aM();
	}
	
	void aM(){
		System.out.println("ForNameSample 클래스의 aM() 메서드");
		bM();
	}
	
	void bM(){
		System.out.println("ForNameSample 클래스의 bM() 메서드");
		cM();
	}
	
	void cM(){
		System.out.println("ForNameSample 클래스의 cM() 메서드");
	}
	

	public static void main(String[] args) {
		new ForNameSample();
	}
}
```

> **java.util.Date**

![](https://images.velog.io/images/yunyoseob/post/6c1d79ce-e697-4480-946e-5d8448232002/image.png)

> **java.util.ArrayList**

![](https://images.velog.io/images/yunyoseob/post/37352817-706f-4035-8ea8-fa1a157cd4e9/image.png)

> **마지막으로 실습할 ForName_p1 사용자 정의 클래스**

```java
package a.b.c.prac1;

import java.lang.reflect.Method;

public class ForName_p1 {
	public void classForName(){
		try {
			Class cl = Class.forName("a.b.c.prac1.ForNameSample");
			System.out.println("\n 1. cl >>> : "+cl);
			ForNameSample fs=(ForNameSample)cl.newInstance();
			System.out.println("\n 2. ForNameSample fs >>> : "+fs);
			System.out.println("\n 3. fs.aM()");
			fs.aM();
			System.out.println("\n 4. fs.bM()");
			fs.bM();
			System.out.println("\n 5. fs.cM()");
			fs.cM();
		
			// 클래스에 선언된 메소드 찾기
			Method m[]=cl.getDeclaredMethods();
			for (int i=0; i<m.length; i++){
				String findM=m[i].getName();
				System.out.println("\n m["+i+"].getName() >>> :: "+findM);
			}
		
			Class d=Class.forName("java.util.Date");
			java.util.Date dd=(java.util.Date)d.newInstance();
			System.out.println("\n 6. dd >>> : "+dd);
		
			Class aList=Class.forName("java.util.ArrayList");
			java.util.ArrayList aList_1=(java.util.ArrayList)aList.newInstance();

			
			System.out.println("\n 7. aList_1 >>> : "+aList_1);
			}catch(Exception e){
				System.out.println("\n 8. 에러 >>> : "+e);
			}
		}

	public static void main(String[] args) {
		new ForName_p1().classForName();
	}
}
```

> **출력 결과**

```java
 1. cl >>> : class a.b.c.prac1.ForNameSample
ForNameSample 기본 생성자 
ForNameSample 클래스의 aM() 메서드
ForNameSample 클래스의 bM() 메서드
ForNameSample 클래스의 cM() 메서드

 2. ForNameSample fs >>> : a.b.c.prac1.ForNameSample@15db9742

 3. fs.aM()
ForNameSample 클래스의 aM() 메서드
ForNameSample 클래스의 bM() 메서드
ForNameSample 클래스의 cM() 메서드

 4. fs.bM()
ForNameSample 클래스의 bM() 메서드
ForNameSample 클래스의 cM() 메서드

 5. fs.cM()
ForNameSample 클래스의 cM() 메서드

 m[0].getName() >>> :: main

 m[1].getName() >>> :: aM

 m[2].getName() >>> :: bM

 m[3].getName() >>> :: cM

 6. dd >>> : Wed Feb 23 01:56:12 KST 2022

 7. aList_1 >>> : []
 ```
 
 #### **간단한 코드해설**
 
> **Class cl=Class.forName("NameSpace");**
 
 - ()안에 찾고자 하는 클래스의 NameSpace(=패키지이름.클래스이름)을 입력하고, Class 클래스의 참조변수 cl을 선언합니다. 
 
> **ForNameSample fs=(ForNameSample)cl.newInstance();**

- 찾고자하는 클래스에 참조변수를 생성합니다. 이 때,  cl은 클래스의 참조변수이므로, 클래스 형변환(다운캐스팅)을 통해 newInstance() 메서드를 통해 객체를 생성합니다. (객체를 생성하는 방법은 new, static, 상속 이외에도 더 있습니다.)

> **Method m[]=cl.getDeclaredMethods();**

- Class의 getDeclaredMethods() 메서드를 통해 Method m[] 함수의 배열에 대입합니다.
- 추가 설명 : Returns an array containing Method objects reflecting all the declared methods of the class or interface represented by this Class object, including public, protected, default (package) access, and private methods, but excluding inherited methods.

> **String findM=m[i].getName();**

- Method m배열의 i번째 함수이름를 String findM에 대입합니다.


> **Class.forName() 3줄 정리 : 결국 핵심은 Class.forName()은 컴파일이 된 클래스들중에서 찾고자 하는 클래스를 찾아, newInstance()로 생성자를 생성할 수 있다. 이럴 경우, package가 다른 클래스를 찾아 생성자를 만들어, 해당 클래스의 자원을 사용할 수 있다.**

**이상으로 JAVA : invoke, 예외처리, Class.forName() 포스팅을 마치도록 하겠습니다. 😀**
