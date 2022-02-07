안녕하세요. 😀 오늘은 JAVA의 자료형에서 문자와 문자열에 대해 포스팅해보도록 하겠습니다.

### **들어가기 전에...**

저번 [함수와 변수 포스팅](https://velog.io/@yunyoseob/%ED%95%A8%EC%88%98%EC%99%80-%EB%B3%80%EC%88%98)에서 변수를 포스팅했을 때, 데이터의 종류로 기초 자료형과 참조 자료형에 대해 다루어 보았습니다.

> **기초 자료형 : primitive type**

```
숫자
	정수
    	Byte	byte	1byte(8bit)
        Short	short	2byte(16bit)
        Integer int		4byte(32bit)
        Long	long	8byte(64bit)
	실수
    	Float	float	4byte(32bit)
        Double	double	8byte(64bit)
    문자
    	Character	char	2byte(16bit)
        - 양의 정수로, 16bit이며 문자를 다루기 때문에 음수를 가질 수 없다.
   논리
   		Boolean		boolean 1byte(8bit)
```

> **참조 자료형 : reference type**

```
객체
	문자열
    배열
    인터페이스
```

기초 자료형과 참조 자료형의 차이는 기초자료형은 변수가 값을 직접 가르키는 반면,
참조 자료형은 변수가 값을 직접 가르키지 않고, 객체를 가리킵니다. 
- 해당 객체안에 데이터를 담고 있습니다.

> **알아두면 좋은 사항 : JAVA에서 JVM에서 컴파일할 때, int 밖에 모릅니다.**

### 형변환

기초자료형에서 숫자로 사용되는 데이터 타입은 서로 데이터를 주고 받을 수 있습니다.
그러나, 각 자료형의 byte와 bit는 다릅니다.
따라서, 자료형을 변환할 때, 이 점을 신경써서 변환해야 할 필요가 잇습니다.

> **묵시적 형변환 vs 명시적 형변환**

기초 자료형을 byte 크기 순으로 작은 순서부터 큰 순서까지 나열하면 다음과 같습니다.

**byte - char - short - int - float - double**

왼쪽에서 오른쪽으로 자료형을 변환하는 것은 byte가 작은 자료형을 byte가 큰 작은 자료형으로 변환하는 것이기 때문에 **자료형 변수 = 변수;** 이런 식으로 사용해도 큰 문제가 생기지 않습니다. 이러한 형변환을 묵시적 형변환이라고 합니다.

반대로, 오른쪽에서 왼쪽으로 자료형을 변환하는 것은 byte가 큰 자료형을 byte가 작은 자료형으로 변환하는 것이기 때문에 캐스팅 연산자를 써주어야 합니다. 이렇게 캐스팅 연산자를 사용하여, 형변환을 하는 것을 명시적 형변환이라고 합니다.

> **형변환 예시**

```
클래스와 메소드 생략...

// 묵시적 형변환 예시
char ch1='A';
int intCh1=ch1;

// 명시적 형변환 예시
int i=32;
char chi=(char)i;
```
- 명시적 형변환의 경우, (char)와 같은 캐스팅 연산자를 사용해 주어야 합니다.

## 문자와 문자열

오늘 주로 포스팅할 내용은 기초 자료형인 문자 char와 참조 자료형인 문자열 String입니다.

프로그램을 구현할 때 대부분 문자열을 활용하기 때문에, 가장 중요한 자료형이라고 볼 수 있습니다.

> **String은 char의 집합이자 배열이다.**

예시로, "velog"라는 단어가 있을 때, 'v','e','l','o','g'은 char이지만, char들을 조합하면 "velog"라는 String이 완성됩니다. 따라서, String은 char의 집합이지 배열이라고 볼 수 있습니다.

> **참고 : charAt**

String의 문자열을 한 글자씩 char 문자형으로 String 글자 중 원하는 위치의 글자를 출력할 수 있습니다.


|Modifier and Type|Method and Description|
|---|---|
|char|charAt(int index) : Returns the char value at the specified index.|



### 배열

배열이란 데이터를 순차적으로 관리하는 객체입니다.

- 순차적으로 관리한다는 것은 index별로 관리한다는 것과 같습니다.

배열의 종류로는 1차원 배열, 2차원 배열, 가변 배열 등등이 있습니다.

> **1차원 배열 3가지 출력 방법**

```
데이터형 참조변수[] 배열연산자 = new 데이터형 [배열이 들어갈 공간] 배열연산자;
데이터형 참조변수[] = new 데이터형[]{};
데이터형 참조변수[]={};
```

> **1차원 배열 출력 실습 코드**

```
package a.b.c.ch1;

public class Array_practice{
	public void array_test(){
		// 1번째 방법
		char cArray[]={'v','e','l','o','g'};
		// char 데이터 타입 배열 만들기
		// [] 형식이 아니라 {} 형식으로 한 다음
		// cArray[n]을 호출하면 n 인덱스에 해당하는 value가 출력된다.
		System.out.println("cArray[0] : >>> "+cArray[0]+"\n");
		System.out.println("cArray[1] : >>> "+cArray[1]+"\n");
		System.out.println("cArray[2] : >>> "+cArray[2]+"\n");
		System.out.println("cArray[3] : >>> "+cArray[3]+"\n");
		System.out.println("cArray[4] : >>> "+cArray[4]+"\n");
		// 배열에서 인덱싱할 때는 []을 사용한다.
		
		// 2번째 방법
		String velog=new String(cArray);
		// cArray 배열을 String 객체로 선언 []이 아닌 ()으로 쓴다.
		System.out.println("velog.charAt(0) : >>> "+velog.charAt(0)+"\n");
		System.out.println("velog.charAt(1) : >>> "+velog.charAt(1)+"\n");
		System.out.println("velog.charAt(2) : >>> "+velog.charAt(2)+"\n");
		System.out.println("velog.charAt(3) : >>> "+velog.charAt(3)+"\n");
		System.out.println("velog.charAt(4) : >>> "+velog.charAt(4)+"\n");
		// velog는 String 변수 이므로, charAt(int)를 통해
		// 출력한다. 
		// String에서 인덱싱 할 때는 ()를 사용한다.
		
		// 3번째 방법
		String velog_2=new String("velog");
		// String안에 배열을 집어넣는게 아니라 velog라는 글자 자체를 집어 넣는다.
		System.out.println("velog_2.charAt(0) : >>> "+velog_2.charAt(0)+"\n");
		System.out.println("velog_2.charAt(1) : >>> "+velog_2.charAt(1)+"\n");
		System.out.println("velog_2.charAt(2) : >>> "+velog_2.charAt(2)+"\n");
		System.out.println("velog_2.charAt(3) : >>> "+velog_2.charAt(3)+"\n");
		System.out.println("velog_2.charAt(4) : >>> "+velog_2.charAt(4)+"\n");
		
		// 4번째 방법
		String velog_3="velog";
		// new String이 아닌 글자 자체를 String 변수로 할당하는 방법
		System.out.println("velog_3.charAt(0) : >>> "+velog_3.charAt(0)+"\n");
		System.out.println("velog_3.charAt(1) : >>> "+velog_3.charAt(1)+"\n");
		System.out.println("velog_3.charAt(2) : >>> "+velog_3.charAt(2)+"\n");
		System.out.println("velog_3.charAt(3) : >>> "+velog_3.charAt(3)+"\n");
		System.out.println("velog_3.charAt(4) : >>> "+velog_3.charAt(4)+"\n");
	} // end of array_test method
	public static void main(String args[]){
		// 함수가 static 수정자 키워드가 없으므로 객체를 생성하여 출력
		new Array_practice().array_test();
		
	} // end of main method
} // end of Array_practice class
```

위와 같은 코드를 입력하고 컴파일 후 실행하면 다음과 같은 결과가 출력됩니다.

![](https://images.velog.io/images/yunyoseob/post/ae47f058-ebc1-45a0-84ff-c041b629d9ad/velog.PNG)

## String 클래스를 초기화 하는 방법

> **String 클래스를 초기화 하는 방법은 "", null이 있습니다.**

String을 초기화 하는 첫 번째 방법은 ""입니다.

```
String str0="";
```

위의 코드로 빈문자열로 초기화 할 수 있습니다.

> **유의사항**

문자열 String이 아닌 문자 Char의 경우, char str=' ';으로 빈문자열로 초기화 합니다.

추가적으로 char에서는 ' '와 같이 작은 따옴표를 사용하고, String에서는 " "와 같이 큰 따옴표를 사용합니다.


String을 초기화 하는 두 번째 방법은 null입니다. null은 String의 default 값으로 데이터가 없다는 의미입니다. String을 null로 초기화 할 때와, ""으로 초기화 할 때의 차이를 비교해보고,

Array_practice 예제에서 String은 "velog"로 띄어쓰기 없이 charAt 명령어를 통해 각 char를 출력했었는데, velog에 띄어쓰기를 추가한다면 어떠한 일이 벌어지는지도 코드를 통해 실습해보도록 하겠습니다.


> **String 클래스 초기화 실습 및 띄어쓰기가 포함된 String 실습 코드**

```
package a.b.c.ch1;

public class Str_practice_2{
	public void stringTest(){
		System.out.println("stringTest method 시작");
		// String 세 가지 실험
		// 빈문자열로 초기화 하는 방법
		
		// 첫 번째 방법
		String str0="";

		// 두 번재 방법
		String str1=null;

		// 띄어쓰기와 글자 섞어서 쓰기
		String str2=" ve l og";

		System.out.println("str0.length() >>> "+str0.length()+"\n");
		System.out.println("str2.length() >>> "+str2.length()+"\n");
        
		// 공식문서를 보면 length()는 public int length()임.
		// 따라서, int 변수 = 변수.length();로 지정해줄 수도 있음.
		int str0_0=str0.length();
		int str2_0=str2.length();

		System.out.println("int 변수 = 변수.length() 지정 str0.length() >>> "+str0_0+"\n");
        
		System.out.println("int 변수 = 변수.length() 지정 str2.length() >>> "+str2_0+"\n");
		
		// length() 쓰지않고 그냥 출력해보기
		System.out.println(" 큰 따옴표 초기화 >>> "+str0+"\n");
		System.out.println(" null 초기화 >>> "+str1+"\n");
		System.out.println("ve l og >>> "+str2+"\n");

		// 마지막으로 charAt로 한 글자 분리해서 살펴보기
		System.out.println("ve l og  분리해서 보기 >>> "+str2.charAt(1)+"\n");

	} // end of stringTest method
	public static void main(String args[]){
		new Str_practice_2().stringTest();
	} // end of main method

} // end of Str_practice_2 class
```
- 참고 : 변수.length()는 string 변수의 길이를 출력하여 줍니다.

위의 코드를 실행했을 경우, 다음과 같은 결과가 출력됩니다.

![](https://images.velog.io/images/yunyoseob/post/c5815e71-7236-4e77-983e-5b8006665e94/image.png)

**Q. str2에 대입한 velog는 5글자인데 왜 length()는 8이라고 출력할까요?**

**A. String str2=" ve l og";에서 사람이 볼 때는 5글자이지만, 컴퓨터 입장에선 띄어쓰기까지 글자수로 계산하기 때문입니다. (왜 String str0=" "; 초기화가 아닌 String str0=""; 초기화인지 아시겠죠?)**


### NullPointer Exception error

> **null로 초기화 한 변수 length() 출력 오류**

코드를 보다보면, ""으로 초기화한 변수는 str0.length() 명령어가 있는데,

null으로 초기화한 변수는 str1.length() 명령어가 없는 것을 확인 할 수 있습니다.

```
System.out.println("str1.length() >>> "+str1.length()+"\n");
```

str0.length() 명령어 아래 위의 코드를 추가하여 실행하면, 어떤 일이 발생할까요?

![](https://images.velog.io/images/yunyoseob/post/37357c63-80e2-407d-8af3-8c6c679519d8/image.png)

javac 명령어로 컴파일은 되지만, 실행이 되지 않습니다.

> **null로 초기화한 변수 int 변수 = 변수.length() 출력 오류**

[java의 API](https://docs.oracle.com/javase/8/docs/api/)를 보면 length()는 public int length()인 것을 볼 수 있습니다.

|Modifier and Type|Method and Description|
|---|---|
|int|length() : Returns the length of this string.|

따라서, int 변수 = 변수.length();으로 지정해줄 수도 있습니다.

```
int str0_0=str0.length();
```
위의 코드에서 ""으로 초기화한 변수의 길이를 출력하는 것을 확인 할 수 있었습니다.

마찬가지 이유로 **int str1_0=str1.length();** 명령어를 사용하여 null으로 초기화한 변수의 길이를 출력시키면 NullPointerException 에러로 실행 불가합니다.

> **length() 명령어 없이 출력해보기**

마지막으로, length() 명령어 없이 출력하면

![](https://images.velog.io/images/yunyoseob/post/049b6914-c196-443d-bd87-5a8988bf3258/image.png)

아무 문제 없이 잘 출력 되는 것을 확인 할 수 있습니다.

""초기화의 경우 아무것도 출력되지 않았고, null로 초기화 할 경우 null이 출력되는 것을 확인 할 수 있었습니다. 

```
System.out.println("ve l og  분리해서 보기 >>> "+str2.charAt(1)+"\n")
```

마지막으로, " ve l og"는 분리해서 2번째 글자를 출력하면 e가 아닌 v가 나오는 것을 볼 수 있습니다.


**이상으로 JAVA 자료형 : 문자와 문자열 포스팅을 마치도록 하겠습니다. 😁**
