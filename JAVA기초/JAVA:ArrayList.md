안녕하세요. 😊 오늘은 JAVA : ArrayList에 대해 포스팅 해보도록 하겠습니다.

**필자의 JAVA Version**

```java
javac -version

// javac 1.8.0_202

java -version

// java version "1.8.0_202"
// Java(TM) SE Runtime Environment (build 1.8.0_202-b08)
// Java HotSpot(TM) 64-Bit Server VM (build 25.202-b08, mixed mode)
```

## ArrayList

[java™ Platform Standard Ed. 8 api](https://docs.oracle.com/javase/8/docs/api/)에서 좌측 상단에 Packages에서 java.util클릭 후, 좌측 하단 Classes아래 ArrayList를 클릭하시면 다음과 같은 화면을 보실 수 있습니다.

![](https://images.velog.io/images/yunyoseob/post/f74bebb0-094b-45b4-98af-ab2f62a5e64a/ArrayList.JPG)

ArrayList는 배열입니다. 그러나, 이전에 포스팅 했던 [Array 배열](https://velog.io/@yunyoseob/JAVA-%EB%B0%B0%EC%97%B4%EA%B3%BC-%EC%A1%B0%EA%B1%B4%EB%AC%B8if%EB%AC%B8)과는 차이가 있습니다.

### Array

> **이전 배열 포스팅 할 때, 다뤘던 JAVA의 배열의 특징**

- 이전 배열 포스팅 >>> [JAVA 배열과 조건문(if)](https://velog.io/@yunyoseob/JAVA-%EB%B0%B0%EC%97%B4%EA%B3%BC-%EC%A1%B0%EA%B1%B4%EB%AC%B8if%EB%AC%B8)

✔ **JAVA에서 배열이란, 같은 데이터형을 순차적으로 나열해 놓은 것**

|번호|특징|
|---|---|
|1.|자바에서 배열은 데이터 형이 같아야 한다.|
|2.|자바에서 배열은 배열의 갯수를 정해 놓고 사용한다.|
|3.|자바에서 배열은 객체이다. (참조 자료형이다.)|
|4.|자바에서 배열은 1차원 배열, 2차원 배열(다차원 배열을 지원한다.)|
|5.|자바에서 배열의 연산자는 [] 대괄호(bracket)이다.|

✔ **배열의 선언 및 초기화**

**1차원 배열[]** 

```java
자료형 배열참조변수[] = new 자료형[배열의 갯수];
자료형[] 배열참조변수 = new 자료형[배열의 갯수];
```

**2차원 배열[][]**

```java
자료형 배열참조변수[][]= new 자료형[배열의 갯수][배열의 갯수];
자료형[][] 배열참조변수 = new 자료형[배열의 갯수]배열의 갯수;
자료형[] 배열참조변수[] = new 자료형[배열의 갯수]배열의 갯수;
```

> **배열 실습 코드**

```java
public class ArrayList_prac {

	public static void main(String[] args) {
		int iArr[] = new int[3];		
		System.out.print(iArr[0]);
		System.out.print(iArr[2]);
        
        int jArr[] = {1,2,3};
		System.out.print(jArr[2]);
	}

}
```
- 출력 결과 : 003


✔ **jArr[] 배열에 문자열 데이터 넣어보기**

```java
int jArr[] = {1,2,"삼"};
System.out.print(jArr[2]);

/*
ArrayList_prac.java:10: error: incompatible types: String cannot be converted to int
        int jArr[] = {1,2,"삼"};
                          ^
1 error
*/

```
- javac 컴파일부터 되지 않습니다.

### ArrayList

ArrayList는 크기를 따로 정해놓지 않고, 데이터를 입력한 다음, 사용해도 출력이 가능합니다.

```java
import java.util.ArrayList;

public class ArrayList_prac {

	public static void main(String[] args) {
		ArrayList lArr=new ArrayList();
		lArr.add(1);
		lArr.add(2);
		lArr.add("삼");
		lArr.add(1.0);
		lArr.add(false);
		lArr.add('c');
		lArr.add(1234l);
		lArr.add(1.000f);
		lArr.add(2.000d);
		
		for (int l=0; l<lArr.size(); l++) {
			System.out.print(lArr.get(l)+", ");
		}
	}
}
```

- 출력결과 : 1, 2, 삼, 1.0, false, c, 1234, 1.0, 2.0,

ArrayList는 문자열 뿐만 아니라, 기초자료형, 참조자료형 모두 지원이 됩니다.

또한, 배열의 크기를 정하는 방식에서 기존의 Array와 차이가 존재합니다.


> **Array와 ArrayList의 배열 크기 설정 차이**

![](https://images.velog.io/images/yunyoseob/post/bf2e6c1c-19af-4a95-ae40-0a5be4ef7e68/image.png)

Array는 배열의 크기를 사전에 정해놓고 사전에 정의해놓은 배열의 크기규칙에 맞춰 사용해야합니다. 

그러나, ArrayList는 초기에 10개로 세팅해놓은 다음, 값이 추가되면 10개씩 배열의 크기를 늘려줍니다.

![](https://images.velog.io/images/yunyoseob/post/40a63edc-aeaa-4aa4-be78-7a8769430fd1/image.png)


### ArrayList 코드 실습

마지막으로 ArrayList를 코드 실습을 마지막으로 이번 포스팅을 마치도록 하겠습니다. 😊

> **HelloVO.java**

```java
package a.b.c.ch3;

public class HelloVO {
	
	private String mid;
	private String mpw;
	private String mname;
	
	public HelloVO() {
		//super();
	}

	public HelloVO(String mid, String mpw, String mname) {
		//super();
		this.mid = mid;
		this.mpw = mpw;
		this.mname = mname;
	}
	
	public String getMid() {
		return mid;
	}
	public String getMpw() {
		return mpw;
	}
	public String getMname() {
		return mname;
	}
	public void setMid(String mid) {
		this.mid = mid;
	}
	public void setMpw(String mpw) {
		this.mpw = mpw;
	}
	public void setMname(String mname) {
		this.mname = mname;
	}
	
}
```

> **ArrayList_p.java**

```java
package a.b.c.prac1;

import java.util.ArrayList;

import a.b.c.ch3.HelloVO;

public class ArrayList_p{
	public void arrayListTest_1(){
		ArrayList<HelloVO> aList = new ArrayList<HelloVO>();
		System.out.println("\n 1st for keyword \n");
		
		for (int i=0; i<3; i++) {
			HelloVO hvo = new HelloVO();
			System.out.println("\n i >>> : "+i+", hvo 참조변수 주소값 >>>"+hvo);
			
			hvo.setMid("VELOG_ID"+i);
			hvo.setMpw("VELOG_PW"+i);
			hvo.setMname("JAVA_SERIES"+i);
			
			System.out.println("aList.size() >>> : "+aList.size());
			System.out.println("aList >>> : "+aList);
			aList.add(hvo);
			System.out.println("\n After input hvo in ArrayList \n");
			System.out.println("aList.size() >>> : "+aList.size());
			System.out.println("aList >>> : "+aList);
		}
		
		System.out.println("\n 2nd for keyword \n");
		
		for (int i=0; i<aList.size(); i++) {
			System.out.println("\n aList.get("+0+") >>> : "+aList.get(i));
			
			HelloVO _hvo =aList.get(i);
			System.out.print(_hvo.getMid()+" ");
			System.out.print(_hvo.getMpw()+" ");
			System.out.println(_hvo.getMname());
		}
		
	}

	public static void main(String[] args) {
		System.out.println("Hello");
		new ArrayList_p().arrayListTest_1();		
	}

}
```

### 실습 코드 해설

> **HelloVO.java**

HelloVo class는 private String mid, mpw, mnname의 변수가 있다. 해당 변수는 클래스 밖으로 나가지 못하는데, public 생성자와 this키워드, 세터메소드와 게터메소드를 통해, 외부에서 해당 변수를 사용할 수 있습니다.

이를 위해, 매개변수가 없는 생성자와 매개변수(String mid, String mpw, String mname)가 있는 생성자를 만들어주고, 세터메소드와 게터메소드를 만들어주었습니다.

> **ArrayList_p.java**

```java
new ArrayList_p().arrayListTest_1();
```

ArrayList_p 클래스에 기본생성자를 만들고, arrayListTest_1 메서드를 실행시킵니다.

```java
ArrayList<HelloVO> aList=new ArrayList<HelloVO>();
```
ArrayList<HelloVO\> 생성자를 new 키워드로 인스턴스 합니다.
  
이 때 배열은 초기화 되어 배열의 size는 0, 배열은 []입니다.
  
- <\>는 제너레이션으로, ArrayList<HelloVO\> 데이터는 HelloVO만 사용하라고, 제너레이션을 선언한 것입니다. 

```java
for (int i=0; i<3; i++) {
	HelloVO hvo = new HelloVO();
```

- for문으로 반복문이 돌면서 한 바퀴 돌 때마다 HelloVO() 생성자를 new키워드로 인스턴스합니다.

```java
hvo.setMid("VELOG_ID"+i);
hvo.setMpw("VELOG_PW"+i);
hvo.setMname("JAVA_SERIES"+i);
```

- 이후, VELOG_ID, VELOG_PW, JAVA_SERIES에 현재 반복되고 있는 숫자 i를 붙여서 HelloVO의 this.변수들에 대입하여 줍니다.

```java
aList.add(hvo)
```

- 참조변수 hvo의 주소값을 참조변수 aList에 추가하여 줍니다.

```java
for (int i=0; i<aList.size(); i++) {
	System.out.println("\n aList.get("+0+") >>> : "+aList.get(i));
			
	HelloVO _hvo =aList.get(i);
	System.out.print(_hvo.getMid()+" ");
	System.out.print(_hvo.getMpw()+" ");
	System.out.println(_hvo.getMname());
}
```

- 이번에는 aList의 index에 저장되어 있는 참조변수의 주소값을 HelloVO 클래스에 _hvo라는 참조변수로 선언한 뒤, 해당하는 생성자의 자원을 출력시킵니다. 


                   
        
> **출력 결과**

```java
Hello

 1st for keyword 


 i >>> : 0, hvo 참조변수 주소값 >>>a.b.c.ch3.HelloVO@15db9742
aList.size() >>> : 0
aList >>> : []

 After input hvo in ArrayList 

aList.size() >>> : 1
aList >>> : [a.b.c.ch3.HelloVO@15db9742]

 i >>> : 1, hvo 참조변수 주소값 >>>a.b.c.ch3.HelloVO@6d06d69c
aList.size() >>> : 1
aList >>> : [a.b.c.ch3.HelloVO@15db9742]

 After input hvo in ArrayList 

aList.size() >>> : 2
aList >>> : [a.b.c.ch3.HelloVO@15db9742, a.b.c.ch3.HelloVO@6d06d69c]

 i >>> : 2, hvo 참조변수 주소값 >>>a.b.c.ch3.HelloVO@7852e922
aList.size() >>> : 2
aList >>> : [a.b.c.ch3.HelloVO@15db9742, a.b.c.ch3.HelloVO@6d06d69c]

 After input hvo in ArrayList 

aList.size() >>> : 3
aList >>> : [a.b.c.ch3.HelloVO@15db9742, a.b.c.ch3.HelloVO@6d06d69c, a.b.c.ch3.HelloVO@7852e922]

 2nd for keyword 


 aList.get(0) >>> : a.b.c.ch3.HelloVO@15db9742
VELOG_ID0 VELOG_PW0 JAVA_SERIES0

 aList.get(0) >>> : a.b.c.ch3.HelloVO@6d06d69c
VELOG_ID1 VELOG_PW1 JAVA_SERIES1

 aList.get(0) >>> : a.b.c.ch3.HelloVO@7852e922
VELOG_ID2 VELOG_PW2 JAVA_SERIES2
```

**이상으로 JAVA : ArrayList 포스팅을 마치도록 하겠습니다. 🙂**
