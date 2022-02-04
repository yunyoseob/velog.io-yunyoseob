안녕하세요. 😊 오늘은 JAVA 키워드 중에 new에 대해 포스팅해보도록 하겠습니다.

### 들어가기 앞서서..

이전에 [JAVA 기초 : Keywords 1편](https://velog.io/@yunyoseob/JAVA-%EA%B8%B0%EC%B4%88-Keywords-1%ED%8E%B8)에서 static 키워드에 대해 다뤘던 것 기억나시나요? 

> **static 키워드는 변수 또는 함수의 자료형 앞에 기술해서 사용하며, 프로그램이 시작할 때 생성되고, 프로그램이 시작할 때, static 키워드가 붙어있는 자원을 자바 가상머신이 해당 자원을 메모리에 올려줍니다.**

예시로, 다음과 같은 코드가 있을 때,

```
package a.b.c.ch1;

public class Example{
	static int i;
    
    public static void main(String args[]){
    	System.out.println("int i >>>"+i);   
    }
}
```

실행하면 int의 디폴트 값인 0이 정상적으로 출력됩니다.

> **그런데, 만약 static int i를 int i로만 선언해주면 어떻게 될까요?**

```
Example.java:6: error: non-static variable i cannot be referenced from a static context
        System.out.println("int i >>>"+i);
                                       ^
1 error
```

자바 컴파일 과정에서 다음과 같은 에러가 나는 것을 확인 할 수 있습니다.

이럴 경우, new라는 키워드를 사용하여 다음과 같이 코드를 작성하면,

```
package a.b.c.ch1;

public class Example{
	int i;
    public static void main(String args[]){
		Example rv=new Example();
    	System.out.println("int i >>>"+rv.i);   
    }
}
```

int의 디폴트값인 0이 정상적으로 출력이 됩니다.

> **왜 new라는 키워드를 사용하면 static을 사용하지 않고도 출력이 가능해지는 걸까요?**

## new

자바에서 자바 프로그램을 메모리에 올리는 여러 방법이 있지만, 

이전에 포스팅 했던, static 키워드가 있고, 오늘 포스팅할 new 키워드가 있습니다.

> **new 키워드**

new 키워드의 경우 자바 가상 머신(JVM)이 new 키워드를 보면, new 뒤에 있는 클래스이름을 보고, 해당하는 클래스를 메모리에 올립니다.

이전 코드를 살펴보면

```
Example rv=new Example();
```

이 부분이 new 키워드를 사용하여 Example이라는 클래스를 메모리에 올린 겁니다.

> **new 키워드 사용방법**

new키워드의 사용방법은 다음과 같습니다.


**1. 클래스 이름을 선언한다.**
**2. 참조 변수를 선언한다.**
**3. = 대입 연산자를 선언한다.**
**4. new 키워드를 선언한다.**
**5. 생성자를 선언한다. (클래스 이름에 () 소괄호를 붙여서만든다.**

> **클래스이름 변수(참조변수, reference variable) = new 클래스이름();**

## static vs new 쉬운 설명 : 톨게이트 예시

static 명령어를 사용하면, 클래스 내 함수에서 쉽게 출력이 가능한데,

new 명령어를 사용하면, 

```
클래스이름 참조변수 = new 클래스이름();
System.out.println(참조변수.출력하고자하는변수);
```

이런 식으로 복잡하게 출력을 해야 합니다.

이를 제 개인적인 생각으로 쉽게 풀어서 톨게이트 사례로 설명하면 다음과 같습니다.

> **톨게이트 예시**

예시로, 서울에서 운전을 해서 급하게 부산을 가야할 일이 생겼다고 합시다.

부산을 가기위해 경부고속도로를 타고 가려는데, 고속도로에 들어가려면 톨게이트를 통과해야만

고속도로를 이용할 수 있습니다.

![](https://images.velog.io/images/yunyoseob/post/02c7653c-9cba-4ed1-bf9a-83635437eec0/image.png)

이 때, 하필 톨게이트 직원들이 전부 파업해서 하이패스로만 고속도로에 들어갈 수 있다고 가정하면,

static은 이 때, 내 차에 있는 하이패스 리더기라고 볼 수 있습니다.

자바가상머신에 컴파일을 할 때, static이 있으면, 고속도로를 바로 이용할 수 있는 것입니다.

> **그런데 만약 하이패스 리더기가 차에 없다면??**

경부고속도로를 이용해서 부산에 가려고 하는데, 하필 이 때, 하이패스 리더기 수리를 맡겨서
없다면 어떻게 해야 할까요?

![](https://images.velog.io/images/yunyoseob/post/c32fa8b0-b3f2-4ab1-b7f9-64ce871dbe4f/image.png)

고속도로를 이용하지 못하기 때문에, 국도를 이용해 부산에 가야 할 것입니다.

여기서 포인트는, 

- 첫 번째로 고속도로와 국도는 다르다는 것입니다.

- 두 번째로 고속도로로 가던 국도로 가던 결국 부산에 갈 수 있다는 것입니다.

|static|new|
|---|---|
|고속도로|국도|


## static vs new 어려운 설명 : 객체와 메모리 할당

앞의 톨게이트 예시가 이해가 되었다면, 본격적으로 static과 new에 대해서 설명해보도록 하겠습니다. 😊

### 객체

먼저, static과 new에 대해 이해하려면 객체를 알아야 합니다.

객체란 소프트웨어 공학 용어로, '의사나 행위가 미치는 대상'이며 유무형의 사물을 의미합니다.

> **객체를 코드로 구현한 것이 클래스입니다.**

예를 들어 나라는 사람이 있다고 하면,


```
나 : 🤵

운동하는 나: ⛹️

서 있는 나: 🧍

저글링 하는 나: 🤹
```

나라는 인물은 한 명이지만, 어떤 것을 하느냐에 따라 또 다른 나라는 존재가 있습니다.

여기서, 운동하는 나, 서 있는 나, 저글링 하는 나 모두 객체에 해당합니다.

```
클래스이름 참조변수 = new 클래스이름();
System.out.println(참조변수.출력하고자하는변수);
```

위의 코드에서 new 클래스이름(); 은 new라는 키워드를 통해 새로운 객체를 생성해주라는 의미입니다.


이 때, 좌항에 있는 참조변수는 메모리에 생성된 인스턴스를 가리키는 변수를 의미합니다.

해당 코드를 수행하고나서

```
System.out.print(참조변수);
```

코드를 실행하게 되면 **클래스이름@~~~~~** 이런식으로 출력되는데,

**~~~~~** 이 부분이 참조 변수의 주소값(참조값)을 의미합니다.

> **클래스와 객체 관련 용어 정리**

용어가 어려우신 분들을 위해 용어와 설명을 정리하면 다음과 같습니다.

|용어|설명|
|---|---|
|객체|객체 지향 프로그램의 대상, 생성된 인스턴스|
|클래스|객체를 프로그래밍하기 위해 코드로 만든 상태|
|인스턴스|클래스가 메모리에 생성된 상태|
|멤버 변수|클래스의 속성, 특성|
|메서드|멤버 변수를 이용하여 클래스의 기능을 구현|
|참조 변수|메모리에 생성된 인스턴스를 가리키는 변수|
|참조 값|생성된 인스턴스의 메모리 주소 값|

> **메모리의 구조**

[TCP SCHOOL.com 의 메모리의 구조 포스팅 자료](http://www.tcpschool.com/c/c_memory_structure)를 인용하면,

프로그램이 실행되기 위해서는 프로그램이 메모리에 로드 되어야 하며, 프로그램에서 사용되는 변수들을 저장할 메모리가 필요합니다.

![](https://images.velog.io/images/yunyoseob/post/39e403df-7d40-4e30-a8ad-6a6df70de822/image.png)

- 사진 출처: [TCP SCHOOL.com의 메모리의 구조 포스팅 자료](http://www.tcpschool.com/c/c_memory_structure)

함수를 호출하면 그 함수만을 위한 메모리 공간이 할당되는데, 이 메모리 공간을 스택(stack)이라고 부릅니다. 

- 함수 내부에서만 사용하는 변수를 지역 변수라고 하며, **스택 메모리**에 생성됩니다.

new 클래스이름()을 선언하면, 객체가 생성되는데, 해당 객체에서 멤버 변수를 출력하려면, 이 변수를 저장할 공간이 있어야 합니다. 이 때 사용하는 메모리가 **힙 메모리**입니다.

> **코드를 통해 메모리 공간 살펴보기**


```
package a.b.c.ch1;


public class Exam_ClassTest {

	// 멤버 변수 
	int iVal;

	// 스태틱 변수, 클래스 변수 
	static int iValStatic;

	public static void main(String args[]) {
		System.out.println("main() 함수는 콘솔어플리케이션 시작점이다.");
		System.out.println("함수 블럭안에서는 인터프리트 방식으로 수행된다.");

		// 함수 블럭 내부에서 선언한 지역 변수
		int i = 10;
		System.out.println("i >>> : " + i);

		// static 변수 호출하기 
		System.out.println("iValStatic >>> : " + iValStatic);
		
		// static 키워드가 붙지 않은 iVal 멤버 변수 사용법
		// iVal 멤버변수를 메모리에 올려야 한다. 
		Exam_ClassTest ec = new Exam_ClassTest();
		System.out.println("Exam_ClassTest 사용자정의 클래스의 변수(참조변수) ec >>> : \n" + ec);
		System.out.println("ec.iVal >>> : " + ec.iVal);

		Exam_ClassTest ec_1 = new Exam_ClassTest();
		System.out.println("Exam_ClassTest 사용자정의 클래스의 변수(참조변수) ec_1 >>> : \n" + ec_1);
		System.out.println("ec_1.iVal >>> : " + ec_1.iVal);

		System.out.println(  "스태틱변수는 참조변수로 참조해서 사용하면 안 된다. \n"
						   + "ec_1.iValStatic >>> : " + ec_1.iValStatic);
	} 
} 
```

가령, 위의 코드를 실행한다면,

![](https://images.velog.io/images/yunyoseob/post/c79a7fbe-12be-40e7-b9bb-0b38c42ffe92/image.png)

메모리에 사진과 같이 저장됩니다.

이 때, Exam_ClassTest()를 **생성자**라고 하는데, 이 생성자가 해당 클래스 내부에 선언한 멤버변수를 디폴트 값으로 초기화 합니다.

> **생성자가 메모리에 올라가면(인스턴스 되면) 해당 클래스에 있는 멤버변수를 디폴트 값으로 초기화 한다.**

**저번 시간에 함수와 변수 포스팅을 할 때, 변수의 경우 변수의 유효범위를 인지하는 게 중요하다고 한 이유가 바로 이런 메모리 구조 때문이였습니다.**

만약, 위의 코드에서 main함수 아래에, iVal을 출력시키면 출력이 되지 않습니다.

```
main 함수 안..

System.out.println("iValStatic >>> : " + iValStatic);
```

- error: non-static variable iVal cannot be referenced from a static context

이유는, iVal은 **클래스 변수(스태틱 변수)**가 아니라 **멤버 변수**이기 때문입니다. 이럴 경우, 출력하려면 객체를 만들어 준 뒤, 생성한 객체에서 **참조변수이름.출력할값**을 출력해야 합니다. 

또한, 함수(메서드) 내에서 변수를 선언한 뒤, 함수(메서드) 밖에서 실행하게 될 경우,

함수 내에서 선언한 변수는 **지역 변수**이기 때문에, 출력이 되지 않습니다.

> **메모리 구조를 통해 이를 설명하면, 지역 변수는 스택 메모리에서 생성됩니다. 함수가 할 일을 다 하고 결과 값을 반환하게 되면, 함수(메서드)에 할당했던 메모리 공간(스택 메모리)을 해제하기 때문에, 지역 변수는 함수 블록 밖에서 출력할 수 없습니다.**

**함수의 경우도 return의 유무와 public의 유무, static의 유무가 중요합니다.**

1. 함수 앞에 static이 있고, return 값이 없는 경우라면, **클래스이름.함수이름();** 으로 출력이 되나, static은 있는데, return 값이 있는 경우라면, **변수타입 새로운변수=클래스이름.함수이름();**으로 새로운변수를 지정해준뒤, 출력해야 합니다.

2. 함수 앞에 static, return이 없는 경우라면, new 키워드를 통해 객체를 생성해준 뒤, **참조변수이름.함수이름();**로 출력시키면 되나, static은 없는데, return이 있는 경우라면, new 키워드를 통해 객체를 생성해준 뒤, **변수타입 새로운변수=참조변수이름.함수이름();**로 새로운 변수를 지정해준 뒤, 출력해야 합니다.

3. 마지막으로, System.out.println()으로 출력할 때도, 리턴이 없는 경우, println()에서 소괄호 안에 입력하면 출력이 되지 않습니다. 반면, 리턴이 있는 경우에는, **변수타입 새로운변수=클래스이름.함수이름();** 혹은 **변수타입 새로운변수=참조변수이름.함수이름();** 으로 새로운 변수를 지정해주고, println()에서 소괄호 안에 새로운 변수를 입력하면 출력이 가능합니다.

> **참고하기 좋은 코드**

```
package a.b.c.ch1;

public class ClassTest_practice_3{
	//멤버 변수
	// 상수
	public static final int ID_NUM=1;

	// 스태틱 변수, 클래스 변수
	static int id_val=11;
	// public이라는 외부에서 사용할 수 있는
	// 접근제한자 키워드가 없다.
	
	// 전역 변수
	public int iVal_G;

	// static이라는 메모리에 할당하는 수정자 키워드가 빠져있다.

	// 멤버 변수
	int iVal;
	// public이라는 접근제한자 키워드도 없고,
	// static이라는 수정자 키워드 없다.

	//사용자 정의 함수
	public void aMethod(){
		System.out.println("aMethod() 등장 두둥");
	} // end of aMethod method
	// return이 없다. 따라서, 리턴형 키워드인 void를 사용했다.
	// static이라는 수정자 키워드가 없다.

	public static void aaMethod(){
		System.out.println("aaMethod() 등장 두둥");
	} // end of aaMethod method
	// return이 없다. 따라서, 리턴형 키워드인 void를 사용했다.

	public int bMethod(){
		System.out.println("bMethod() 돌아가는 중~");
		return 1+1;
	} // end of bMethod method
	// return이 있다.
	// 유의해야 할 점은 bMethod 앞에 있는 int와
	// return으로 출력되는 1+1의 데이터 타입이
	// 모두 int로 동일해야 한다.
	// static이라는 수정자 키워드가 없다.

	public static int bbMethod(){
		System.out.println("bbMethod() 돌아가는 중~");
		return 10+10;
	} // end of bbMethod method
	// return이 있다.
	// bbMethod앞에 int와 return으로 출력되는 10+10의
	// 데이터 타입이 모두 int로 동일해야 한다.

	// main 함수 등장
	public static void main(String args[]){
		// static이 있는 친구들
		// 멤버변수 중에 상수 불러오기 (static 있음)
		System.out.println("ClassTest_practice_3.ID_NUM >>> "+ClassTest_practice_3.ID_NUM+"\n");
		// 스태틱 변수 불러오기
		System.out.println("ClassTest_practice_3.id_val >>> "+ClassTest_practice_3.id_val+"\n");
		// aaMethod 불러오기(return이 없어서 println안에 가져다 못 씀)
		System.out.println("ClassTest_practice_3.aaMethod는 리턴이 없어서 println에 가져다 못 씀. 불러오기 \n");
		ClassTest_practice_3.aaMethod();
		// bbMethod 불러오기
		int x=ClassTest_practice_3.bbMethod();	
		System.out.println("ClassTest_practice_3.bbMethod >>> "+x+"\n");

		// static이 없는 친구들을 위해 객체 생성해주기 (인스턴스 생성)
		ClassTest_practice_3 ec=new ClassTest_practice_3();
		System.out.println("ClassTest_practice_3 ec 주소 >>> "+ec+"\n");
		// 전역 변수 불러오기 (static 없음)
		System.out.println("ClassTest_practice_3 ec.iVal_G >>> "+ec.iVal_G+"\n");
		// 멤버 변수 불러오기 (static 없음)
		System.out.println("ClassTest_practice_3 ec.iVal >>> "+ec.iVal+"\n");
		// aMethod 불러오기 (static 없음, return도 없음)
		System.out.println("ClassTest_practice_3 ec.aMethod는 리턴이 없어서 println에 가져다 못 씀. 불러오기 \n");
		ec.aMethod();
		// bMethod 불러오기 (static 없음, 근데 return은 있음)
		int y=ec.bMethod();
		// bMethod 리턴값이 int형이므로 동일하게 x도 int라는 데이터를 담는 변수라는 상자에 할당하여 준다.
		System.out.println("ClassTest_practice_3 ec.bMethod는 리턴이 없어서 println에 가져다 못 씀. 불러오기 \n");
		System.out.println("ClassTest_practice_3 ec.bMethod >>> "+y+"\n");
	} // end of main method
	
} // end of ClassTest_practice_3 class 

```


**마치며..**


**이번 포스팅에서 static이라는 수정자 키워드의 유무에 따라 메모리에 할당하는 방법에도 차이가 있는 것을 살펴봤고, new라는 키워드를 통해 객체를 생성하여 출력하는 방법도 알아보았습니다. JAVA의 API를 자세히 살펴보면, java.lang.클래스이름에 대한 세부적인 설명에서 static이라는 수정자가 있는 경우도 있고, 없는 경우도 있습니다. static 수정자의 유무에 따라서 메모리에 할당할 때, 적절히 대응하여 잘 사용해야 컴파일을 할 때 오류가 없을 것입니다. 이번 포스팅은 여기서 마치도록 하겠습니다. 😊**

