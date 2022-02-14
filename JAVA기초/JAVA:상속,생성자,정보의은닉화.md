안녕하세요 🙂 오늘은 JAVA에서 상속, 생성자, 정보의 은닉화(Encapsulation, information hiding)에 대해 포스팅해보도록 하겠습니다.

Java는 객체 지향 프로그래밍(Object Oriented Programming)입니다. JAVA는 미리 만들어진 프로그램 또는 클래스를 가지고, 새로운 프로그램 또는 클래스를 만듭니다.

이 때, JAVA에서 빌트인 클래스(미리 만들어진 프로그램 또는 클래스)의 최고 우두머리는 java.lang.Object 클래스로, 사용자 정의 클래스는 java.lang.Object 클래스를 상속하여 만듭니다.

## 상속

![](https://images.velog.io/images/yunyoseob/post/7fc387d6-20f5-4fd9-b5d1-b52687d6d5f2/%EA%B0%80%EC%A1%B1.jpg)

- 사진 출처: [위키백과 가족](https://ko.wikipedia.org/wiki/%EA%B0%80%EC%A1%B1)

인간사회에서 상속은 부모가 자식에게 넘겨주는 것을 의미합니다. 

JAVA와 같은 객체 지향 언어에서 상속의 개념은 인간사회와 비슷하지만, 차이는 자식은 부모의 재산을 다 사용할 수 있습니다. (단, 부모가 자식에서 상속을 해주면 부모는 자식의 재산을 부모 맘대로 사용할 수 없습니다.)

> **Q. 객체 지향에서 상속을 하는 이유는?**

부모의 자원을 자식이 사용하기 위해서입니다. 해당 사진에서 증조부/증조모는 자바에서 java.lang.Object 클래스입니다. 해당 클래스의 자식인 조부/조모는 java.lang.Object 클래스에 있는 모든 자원을 다 쓸 수 있습니다.


> **JAVA에서 상속 기능을 하는 키워드 : extends, implements**

|키워드|의미|
|--|--|
|**extends**|클래스 상속할 때 사용하는 키워드|
|**implements**|인터페이스를 상속 할 때 사용하는 키워드|

> **실습 코드**

[예전 HelloJava 출력하기 포스팅](https://velog.io/@yunyoseob/HelloJava-%EC%B6%9C%EB%A0%A5%ED%95%98%EA%B8%B0)에서 처음으로 HelloJava 출력할 때 당시 코드는 아래와 같았습니다.

```java
public class HelloJava{

        public static void main(String args[]){

                System.out.println("Hello Java");
        }
}
```

HellaJava 클래스는 사실 extend java.lang.Object 명령어를 통해 java.lang.Object에서 상속받은 클래스인데, 생략 된 코드입니다.

- extends 키워드로 클래스를 상속하면 상속해준 클래스가 먼저 올라갑니다.

```java
public class HelloJava extends java.lang.Object{

        public static void main(String args[]){

                System.out.println("Hello Java");
        }
}
```

해당 코드를 컴파일 후 실행시키면, 처음 코드와 마찬기지로 "Hello Java"가 출력됩니다. 여기서, javap HelloJava로 클래스 파일을 역컴파일 하면 다음과 같은 결과가 출력됩니다.

```java
Compiled from "HelloJava.java"
public class HelloJava {
  public HelloJava();
  public static void main(java.lang.String[]);
}
```

여기서, 3번째 줄에 public HelloJava()를 생성자라고 합니다.

> **생성자란 클래스를 메모리에 올릴 때, JVM이 사용하는 함수로 자바 소스에 생성자의 코드 블럭이 있으면 해당 생성자를 사용하고, 코드블럭이 없으면 JVM 생성자를 만들어 사용합니다.**

## 생성자(Constructor)

HelloJava의 역컴파일 과정에서 출력된 public HelloJava()와 같은 생성자를 기본 생성자(Default Contructor)라고 합니다. JVM은 자바 소스에 생성자의 코드 블럭이 없으면 기본 생성자를 생성하여 멤버필드를 초기화 합니다.

> **생성자의 모습**

```java
클래스이름(){

}
```

> **생성자 실습 코드**

```java
package a.b.c.ch2;

class Const_p{
	String s;
	int i;
}

public class Object_p_2{	
	// 실험1 : 생성자가 없는 경우

	// 실험2 : 매개변수가 없는 기본 생성자 만들기
	Object_p_2() {
		System.out.println("매개변수가 없는 기본 생성자");
	}

	// 실험3 : 매개변수가 있는 기본 생성자 만들기
	Object_p_2(String s) {
		System.out.println("매개변수가 있는 기본 생성자 \n");
		System.out.println("Object_p_2(String s)의 s >>> : "+s);
	}

	public static void main(String args[]){

		System.out.println("Hello Java");

		Object_p_2 rv = new Object_p_2();
		System.out.println("참조변수 주소값 >>> : "+rv);

		Object_p_2 rv = new Object_p_2("실험3의 매개변수 입력");
		System.out.println(" 실험3의 참조변수 >>> : "+rv);

		Const_p rv = new Const_p();
		System.out.println("rv 참조변수 주소값 >>> : "+rv);
		System.out.println("rv.s >>> : "+rv.s);
		System.out.println("rv.i >>> : "+rv.i);
	} 
} 

```

다음과 같이 실험1 : 생성자가 없는 경우, 실험2 : 매개변수가 없는 기본 생성자 만들기, 실험3 : 매개변수가 있는 기본 생성자 만들기를 각각 실험(하나의 실험을 할 때 나머지 실험은 주석처리 후 실행)하면 결과는 다음과 같습니다.

✔ **실험 1: 생성자가 없는 경우 역컴파일**

```java

Compiled from "Object_p_2.java"
public class a.b.c.ch2.Object_p_2 {
public a.b.c.ch2.Object_p_2();
public static void main(java.lang.String[]);
}
```

javap 역컴파일을 해보면 기본생성자를 JVM이 생성하였고, JVM이 기본생성자를 만들어서 멤버필드를 초기화 하였습니다.


✔ **실험2 : 매개변수가 없는 기본 생성자 만들기**

생성자가 생성이 되면서 "매개변수가 없는 기본 생성자"가 출력됩니다.

마찬가지로, javap 역컴파일을 해보면 기본 생성자가 생긴 것을 확인 할 수 있습니다.

```java

public class a.b.c.ch2.Object_p_2 {
java.lang.String s;
int i;
a.b.c.ch2.Object_p_2();
public static void main(java.lang.String[]);
}
```

✔ **실험3 : 매개변수가 있는 생성자 만들기**

매개변수가 있는 생성자를 만들고, 역컴파일 하면 기본 생성자가 아닌 새로운 생성자가 생깁니다.

```java

Compiled from "Object_p_2.java"
public class a.b.c.ch2.Object_p_2 {
java.lang.String s;
int i;
a.b.c.ch2.Object_p_2(java.lang.String);
public static void main(java.lang.String[]);
}
```

✔ **다른 클래스의 생성자 확인**

마지막으로 Object_p_2 클래스가 아닌 Const_p 클래스의 객체를 만들어서 출력하면, String의 초기값인 null과 int의 초기값인 0이 출력됩니다. 이 과정을 역컴파일하여 확인하면, 다음과 같습니다.

```java
Compiled from "Object_p_2.java"
public class a.b.c.ch2.Object_p_2 {
  public a.b.c.ch2.Object_p_2();
  public static void main(java.lang.String[]);
}
```

main함수가 있는 클래스에서 기본 생성자를 생성후, new 키워드를 통해 참조변수 주소값을 a.b.c.ch2.Const_p@15db9742으로 객체를 생성하여, String의 초기값과 int의 초기값을 출력합니다.

### 생성자를 만드는 규칙

|번호|규칙설명|
|---|---|
|1|클래스 이름 ( ) { }|
|2|( ) 소괄호에 매개변수를 사용할 수 있다.|
|3|{ } 블럭에서 클래스를 인스턴스 하면서 맨 먼저 해야할 함수(동작)을 선언한다.|
|4|생성자는 멤버변수를 초기화 한다.|

> **생성자 실습코드 : 회원가입 프로그램 코드**

✔ **a.b.c.ch2.scr.MemberScr**

```java
package a.b.c.ch2.scr;

// a.b.c.ch2.vo.MemberVO 에 있는 클래스를 
// a.b.c.ch2.scr.MemberScr 클래스에서 사용하려고 불러온다.
import a.b.c.ch2.vo.MemberVO;

// 회원가입 프로그램
public class MemberScr {
	
	public static void main(String args[]) {
		MemberVO mvo=new MemberVO();
		System.out.println("mov 참조변수 주소값 >>> : "+mvo);

		MemberVO mvo_1 = new MemberVO("HGD", "HGD00", "홍길동", "010-1234-5678","사랑시 행복구");
		System.out.println("mvo_1 참조변수 주소값  >>> : " + mvo_1);
	}
}
```

✔ **a.b.c.ch2.vo.MemberVO**

```java
package a.b.c.ch2.vo;

// 회원가입 프로그램에서 회원정보를 나르는 클래스 

public class MemberVO {

	 public String mid;
	 public String mpw;
	 public String mname;
	 public String mhp;
	 public String maddr;

	public MemberVO() {
		System.out.println("mid >>> : " + mid);
		System.out.println("mpw >>> : " + mpw);
		System.out.println("mname >>> : " + mname);
		System.out.println("mhp >>> : " + mhp);
		System.out.println("maddr >>> : " + maddr);			
	}

	public MemberVO(String mid, String mpw, String mname, String mhp, String maddr) {
		System.out.println("mid >>> : " + mid);
		System.out.println(" mpw >>> : " + mpw);
		System.out.println(" mname >>> : " + mname);
		System.out.println(" mhp >>> : " + mhp);
		System.out.println(" maddr >>> : " + maddr + "\n");		
	}

}
```

다음과 같은 두 개의 클래스를 서로 연동하여 사용하고자 할 때, 컴파일을 명령어는 다음과 같이 입력하여야 합니다.

```java
// 컴파일 명령어

javac -d . MemberVO.java MemberScr.java
```

```java
// 실행 명령어

java a.b.c.ch2.scr.MemberScr
```
> **출력 결과**

```java
mid >>> : null
mpw >>> : null
mname >>> : null
mhp >>> : null
maddr >>> : null
mov 참조변수 주소값 >>> : a.b.c.ch2.vo.MemberVO@15db9742
mid >>> : HGD
 mpw >>> : HGD00
 mname >>> : 홍길동
 mhp >>> : 010-1234-5678
 maddr >>> : 사랑시 행복구

mvo_1 참조변수 주소값  >>> : a.b.c.ch2.vo.MemberVO@6d06d69c
```

매개변수가 없는 생성자에서는 String의 default값인 null이 출력이 되며, 매개변수가 있는 생성자에서는 매개변수가 잘 출력된 것을 확인 할 수 있습니다.

> **만약, MemberVO 클래스의 멤버변수의 접근제한자가 public이 아니라 private라면??**

MemberScr 클래스에서 MemberVO 클래스의 변수를 출력시킬 수 없습니다. 가령 MemberVO 클래스의 멤버변수의 접근제한자를 public에서 private로 바꾸고  MemberScr 클래스에서

```java
MemberVO mvo=new MemberVO();
System.out.println("mvo.mid >>> : "+mvo.mid);
```

다음과 같은 내용을 출력시키면

```java
MemberScr.java:21: error: mid has private access in MemberVO
```

다음과 같은 에러가 출력됩니다. 그 이유는 public은 다른 패키지에서도 사용이 가능하나, private는 class 블록 밖에서 사용하지 못하는 접근제한자이기 때문입니다.

## 정보의 은닉화

정보의 은닉화는 information hiding이라고도 하며, Encapsulation이라고도 불립니다.
정보의 은닉화는 다른 객체에게 자신의 정보를 숨기고 자신의 연산만을 통해 접근을 허용하는 것으로, 클래스 외부에서 특정 정보에 접근을 막는다는 의미입니다.

- 출처 : [해시넷 : 정보은닉](http://wiki.hash.kr/index.php/%EC%A0%95%EB%B3%B4%EC%9D%80%EB%8B%89)

이전 코드에서 public이 아닌 private로 접근제한자를 수정 후, 다른 패키지에 있는 클래스의 변수를 출력시킬 때, 에러가 나타나는 것을 확인 할 수 있었습니다.

이는 다른 객체에서 접근 허용을 막고, 자신의 연산만으로 접근이 가능하게 만들었기 때문입니다.

> **그렇다면 어떻게 접근할 수 있을까?**

답은 public 생성자를 통해서 접근하게 만들 수 있습니다. 해당 내용은 실습 코드를 통해 보도록 하겠습니다.


> **실습 코드**

```java
package a.b.c.ch2;

// n번은 콘솔창 출력 순서
class EncapVO{
	private String sval;
	private int ival;
	
	// 생성자 1
	public EncapVO(){
		System.out.println("\n 2번 EncapVO의 private sval >>> : "+sval);
		System.out.println("\n 3번 EncapVO의 private ival >>> : "+ival);
		System.out.println("\n 4번 EncapVO의 private this.sval >>> : "+this.sval); 
		System.out.println("\n 5번 EncapVO의 private this.ival >>> : "+this.ival);
	}
	
	// 생성자 2
	public EncapVO(String sval, int ival){
		System.out.println("\n 9번 EncapVO(String sval, int ival) 매개변수에 인수를 대입한 이후 >>> : "+sval);
		System.out.println("\n 10번 EncapVO(String sval, int ival) 매개변수에 인수를 대입한 이후 >>> : "+ival);
		System.out.println("\n 11번 EncapVO(String sval, int ival) 매개변수가 아닌 멤버변수 >>> : "+this.sval);
		System.out.println("\n 12번 EncapVO(String sval, int ival) 매개변수가 아닌 멤버변수 >>> : "+this.ival);

		this.sval=sval;
		this.ival=ival;

		System.out.println("\n 13번 EncapVO(String sval, int ival) 매개변수를 멤버변수 sval, ival에 대입한 이후 >>> : "+this.sval);
		System.out.println("\n 14번 EncapVO(String sval, int ival) 매개변수를 멤버변수 sval, ival에 대입한 이후 >>> : "+this.ival);
		}


	public void setSval(String sval){
		this.sval=sval;
	}

	public String getSval(){
		return this.sval;
	}

	public void setIval(int ival){
		this.ival=ival;
	}
	public int getIval(){
		return this.ival;
	}
} 

public class Encap_p{
	public static void main(String args[]){
		System.out.println("\n 1번 main 함수 시작 \n");
		
		// 생성자 1 Test
		EncapVO rv=new EncapVO();
		System.out.println("\n 6번 Encap_p의 참조변수 주소 >>> : "+rv);
		System.out.println("\n 7번 rv.getSval() >>> : "+rv.getSval());
		System.out.println("\n 8번 rv.getIval() >>> : "+rv.getIval());

		// 생성자 2 Test
		EncapVO rv_2=new EncapVO("This Year", 2022);
		System.out.println("\n 15번 rv_2의 참조변수 주소 >>> : "+rv_2);
		System.out.println("\n 16번 rv_2.getSval() >>> : "+rv_2.getSval());
		System.out.println("\n 17번 rv_2.getIval() >>> : "+rv_2.getIval());

		rv_2.setSval("Last Year");
		rv_2.setIval(2021);
		System.out.println("\n 18번 this.sval은 null이였는데, this.sval=Last Year이 되었으므로 >>> "+rv_2.getSval());
		System.out.println("\n 19번 this.ival은 0이였는데, this.ival=2021이 되었으므로 >>> "+rv_2.getIval());
	} 
} 
```

> **출력결과**

![](https://images.velog.io/images/yunyoseob/post/00516d45-04d4-48ef-9fcc-e65a81fe05f6/image.png)

> **this**

해당 코드를 보시면, this가 있는 것을 보실 수 있습니다. this 키워드는 해당 클래스 내에 현재 변수 값을 지칭하는 키워드 입니다. 가령, 현재 클래스의 변수가 String sval;이면 String의 초기값인 null이 출력되며, 현재 클래스의 변수가 int ival;면, int의 초기값인 0이 출력됩니다.

**만약, 이 때, this.sval="This Year";, this.ival=2022를 대입한다면, 대입 이후, 현재 클래스의 변수는 This Year와 2022가 됩니다.**

> **코드 출력 해설**

|출력순서|설명|
|---|---|
|1번|main 함수의 시작을 의미합니다.|
|2번|new 키워드로 객체를 생성하였습니다. (생성자 1, 매개변수X), String의 초기값을 출력하였기 때문에 null이 출력되었습니다.|
|3번|int의 초기값을 출력하였기 때문에 0이 출력되었습니다.|
|4번|this.sval은 현재 String에 선언한 변수값인데, 초기화 상태이기 때문에, null이 출력됩니다.|
|5번|this.ival은 현재 int에 선언한 변수값이 초기화 상태이기 때문에, 0이 출력됩니다.|
|6번|new 키워드로 생성한 객체의 참조변수 주소값이 출력합니다.|
|7번|현재 String sval이 초기값인 상태이므로, null값이 출력됩니다. (4번 결과와 같습니다.)|
|8번|현재 int ival이 초기값인 상태이므로, 0이 출력됩니다. (5번 결과와 같습니다.)|
|9번|new 키워드로 객체를 생성하였습니다. (생성자 2, 매개변수O), 매개변수 Stinrg sval에 인수인 This Year가 대입이 되어서, This Year가 출력됩니다.|
|10번|매개변수 int ival에 인수인 int 2022가 대입이 되어서, 2022가 출력됩니다.|
|11번|클래스에 private String sval은 아직 어떤 값도 대입되지 않아, 초기값인 null이 출력됩니다.|
|12번|클래스에 private int ival은 아직 어떤 값도 대입되지 않아, 초기값인 0이 출력됩니다.|
|13번|this.sval=sval; 명령어로 현재 클래스의 String sval에 함수에 들어온 String sval을 대입하여 출력했으므로, This Year가 출력됩니다.|
|14번|this.ival=ival; 명령어로 현재 클래스의 int ival에 함수에 들어온 int ival을 대입하여 출력했으므로, 2022가 출력됩니다.|
|15번|new 키워드로 객체를 생성한 뒤, 참조변수의 주소를 출력합니다.|
|16번| 9번부터 14번 과정이 끝났기 때문에 this.sval=This Year 대입이 완료된 상태입니다. 따라서, This Year가 출력됩니다.|
|17번| 9번부터 14번 과정이 끝났기 때문에 this.ival=2022 대입이 완료된 상태입니다. 따라서, 2022가 출력됩니다.|
|18번|this.sval이 초기값이였는데, this.sval=Last Year 대입을 한 뒤, this.sval을 리턴하였으므로, Last Year가 출력됩니다.|
|19번|this.ival이 초기값이 였는데, this.ival=2021 대입을 한 뒤, this.ival을 리턴하였으므로, 2021이 출력됩니다.|

**이상으로 JAVA : 상속, 생성자, 정보의 은닉화 포스팅을 마치도록 하겠습니다. 😃**
