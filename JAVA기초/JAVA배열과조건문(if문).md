안녕하세요. 😊 오늘은 JAVA에서 배열과 제어문중에 조건문(if문)에 대해 포스팅하도록 하겠습니다.

### 들어가기 전에...

저번 [JAVA 자료형: 문자와 문자열](https://velog.io/@yunyoseob/JAVA-%EC%9E%90%EB%A3%8C%ED%98%95-%EB%AC%B8%EC%9E%90%EC%99%80-%EB%AC%B8%EC%9E%90%EC%97%B4)에서 문자와 문자열을 다룰 때, 배열을 잠시 다뤘었는데요.

이번에는 배열에 대해 좀 더 깊이 탐구해보는 시간을 갖도록 하겠습니다.

## 배열

자바에서 배열은 array라고 지칭합니다. 

자바에서의 배열의 특징은 다음과 같습니다.

> **자바에서 배열의 특징**

1. 자바에서 배열은 같은 데이터형(타입)을 순차적으로 나열해 놓은 것이다.
2. 자바에서 배열은 데이터 형이 같아야 한다. 
3. 자바에서 배열은 배열의 갯수를 정해 놓고 사용한다.
4. 자바에서 배열은 객체이다(참조 자료형이다).
5. 자바에서 배열은 1차원 배열, 2차원 배열(다차원 배열을 지원한다).
6. 자바에서 배열의 연산자는 [] 대괄호이다.


> **1차원 배열 3가지 출력 방법**

```
데이터형 참조변수[] 배열연산자 = new 데이터형 [배열이 들어갈 공간] 배열연산자;
데이터형 참조변수[] = new 데이터형[]{};
데이터형 참조변수[]={};

```
저번 포스팅에서 1차원 배열 3가지 출력 방법을 살펴보았었는데요.

차원이 늘어날 경우, []를 더 추가하여 작성합니다.

예시로 2차원 배열의 출력방법은 다음과 같습니다.

> **2차원 배열 출력 방법**

```
자료형 배열참조변수[][] = new 자료형[배열의 갯수][배열의 갯수];
자료형[][] 배열참조변수 = new 자료형[배열의 갯수]배열의 갯수;
자료형[] 배열참조변수[] = new 자료형[배열의 갯수]배열의 갯수;
```

> **차원별 배열 실습 코드**

```
package a.b.c.ch1;

public class Array_practice_2{
	public void dim_Array(){
		int iReferenceVariable[]= new int[3];
		System.out.println("참조변수 주소 값 >>> : "+iReferenceVariable);
        
		int iVal0=iReferenceVariable[0];
		int iVal1=iReferenceVariable[1];
		int iVal2=iReferenceVariable[2];
		System.out.println("iVal0 >>> : "+iVal0+"\n");
		System.out.println("iVal0 >>> : "+iVal1+"\n");
		System.out.println("iVal0 >>> : "+iVal2+"\n");

		double iReferenceVariable_1[][]= new double[1][3];
		System.out.println(" iReferenceVariable_1 참조변수 주소 값 >>> : "+iReferenceVariable_1);
		double iVal0_0=iReferenceVariable_1[0][0];
		double iVal0_1=iReferenceVariable_1[0][1];
		double iVal0_2=iReferenceVariable_1[0][2];
		System.out.println("iVal0_0 >>> : "+iVal0_0+"\n");
		System.out.println("iVal0_1 >>> : "+iVal0_1+"\n");
		System.out.println("iVal0_2 >>> : "+iVal0_2+"\n");


		double dReferenceVariable[][]=new double[3][2];
		double dVal0_0=dReferenceVariable[0][0];
		double dVal0_1=dReferenceVariable[0][1];
	
		double dVal1_0=dReferenceVariable[1][0];
		double dVal1_1=dReferenceVariable[1][1];

		double dVal2_0=dReferenceVariable[2][0];
		double dVal2_1=dReferenceVariable[2][1];

		System.out.println("dVal0_0 >>> : "+dVal0_0+"\n");
		System.out.println("dVal0_1 >>> : "+dVal0_1+"\n");

		System.out.println("dVal1_0 >>> : "+dVal1_0+"\n");
		System.out.println("dVal1_1 >>> : "+dVal1_1+"\n");

		System.out.println("dVal2_0 >>> : "+dVal2_0+"\n");
		System.out.println("dVal2_1 >>> : "+dVal2_1+"\n");
	} // end of one_dim_Array method

	public static void main(String arg[]){
		new Array_practice_2().dim_Array();
	} // end of main method
} // end of Array_practice_2 class
```

**코드 실행 결과**

![](https://images.velog.io/images/yunyoseob/post/7a96fb67-9a4d-46fb-bdf0-30a316276a19/image.png)

**코드 해설과 결과 리뷰**

> 1차원 배열

먼저 처음에 int 형 1차원 배열로 크기는 3으로 선언했습니다. int는 기초자료형인데 이것을 배열로 선언하면 객체로 변합니다. 

참조변수 주소값의 왼쪽 대괄호 한 개는 1차원 배열이라는 의미입니다. 뒤에 I는 int형 배열이라는 의미입니다. 출력결과 int의 default 값인 0이 나오는 것을 확인할 수 있었습니다.

- 유의해야 할 점은 iReferenceVariable는 method가 아니라 참조변수이므로, iReferenceVariable[0]; 와 같은 방식으로 출력하면 안 됩니다.

> 2차원 배열

2차원 배열의 경우 처음 케이스의 경우 1*3 행렬로 1행 3열로 크기를 지정하였고, 2차원 배열을 선언할 때는 double을 자료형으로 선언하였습니다.

참조변수 주소값의 왼쪽 대괄호 두 개는 2차원 배열이라는 의미이고, 뒤에 D는 double형 배열이라는 의미입니다.

코드 출력 결과는 행이 1행이기 때문에, 1차원 배열과 유사하나 0이 아닌 0.0이 3개가 출력된 것을 확인 할 수 있습니다.

한 편, 2차원 배열의 2번째 케이스의 경우, 3*2행렬로 3행 2열 크기를 지정하였고, 마찬가지로 2차원 배열을 선언할 때는 double을 자료형으로 선언하였습니다.

코드 출력 결과 0.0이 6개가 출력된 것을 확인 할 수 있었습니다.


```
byte bArr[]=new byte[10];
```
예시로, byte 배열을 만든다고 하면, 배열에 크기를 할당하는 방법은 이제 알게 되었습니다.
그런데, 배열에 데이터를 집어넣고자 한다면 어떻게 해야 할까요?

> **배열에 데이터를 입력하는 방법**

첫 번째 방법은 배열의 값을 선언과 동시에 초기화 하는 방법입니다.
```
byte bArr_1[]= new byte[]{1,2,3}
```

두 번째 방법은 배열의 값을 선언 과 동시에 초기화 하면서 new 연산자와 데이터타입 생략하는 방법입니다.
```
byte bArr_2[] = {1, 2, 3};
```

마지막 방법은 배열 자료형을 선언 후에 입력하는 방법입니다.
```
byte bArr_3[];
bArr_3=new byte[]{1,2,3}
```

- 유의해야 할 점은 byte bArr_3[]; 선언을 하면 두 번째줄 코드에 new byte[]를 생략할 수 없다는 것입니다.

> **String args[]**

블로그 처음 부분에 콘솔창에 처음으로 [HelloJava 출력하는 포스팅](https://velog.io/@yunyoseob/HelloJava-%EC%B6%9C%EB%A0%A5%ED%95%98%EA%B8%B0)에서 코드 기억나시나요?? 😃

```
public class HelloJava{

        public static void main(String args[]){

                System.out.println("Hello Java");
        }
}

```

여기서, 다른 부분을 전부 설명했으나, 당시에 String args[]에 대한 설명은 하지 않았었는데,

배열을 알면 String args[]에 의미도 알 수 있습니다.

아까 배열에 데이터를 입력하는 예시에서는 String의 경우, String str[]={"velog"}; 와 같은 형식으로 입력 할 수 있을 것입니다.

여기서 중요한 점은 []와 배열이름은 순서가 바뀌어도 상관이 없다는 것입니다. 즉,

```
자료형 [] 배열이름
```
==
```
자료형 배열이름 []
```
둘 다 같은 의미입니다. 따라서, String args[] 명령어에 만약 velog라는 입력이 들어가면

```
String args[] = new String[]{"velog"};

or

String args[]={"velog"};
```

코드가 입력이 되는 것입니다.

## 조건문(if)

오늘 포스팅할 두 번째 내용은 조건문입니다. 자바에는 어떤 작업을 특정 조건에 맞게 수행하거나 반복하도록 제어할 수 있는 제어문이 있습니다. 제어문은 조건문과 반복문이 있습니다.

> **제어 흐름은 Flow Control이라고 하며, if, switch, for, while, do while이 있습니다.**

조건문 중에 if문을 사용하는 방법은 다음과 같습니다.

```
if (){
}
else{
}
```

> **if문 코드 예시**

```
package a.b.c.ch1;

public class If_practice{
	public static void main(String args[]){
		int x=1;
		int y=2;

		boolean xyBool=x<y;
		System.out.println(xyBool);
		
		if (xyBool){
			System.out.println("true");
		} // end of xyBool keyword

		if (x < y) {
			System.out.println("true");
		}

		if (1 < 2) {
			System.out.println("true");
		}
    }
}
```

코드를 실행하면, true가 3번 출력됩니다.
    
### 조건문을 사용할 때 유의해야 할 사항

여기서 유의해야할 사항은 if뒤 소괄호 안에 내용은 true여야 출력이 된다는 것입니다.

> **if 뒤에 소괄호 안에 내용은 true만 출력한다.**

```
// 클래스와 메소드 생략...
if (true){
	System.out.println("true");
    
if (false){
	System.out.println("false");
    }
```

위와 같은 코드가 있을 때, 콘솔창에 입력하면 true만 출력됩니다.

이는 if문에서 가장 핵심적인 내용입니다. 이유는 해당 코드를 컴파일하고 실행했을 때, 그 어떤 에러도 출력되지 않고, 실행도 됐는데, false가 출력되지 않았기 때문입니다.

```
if (x < y) {
			System.out.println("true");
}            
```            

> **코드가 1만줄이고, if문이 100개 정도 되며, 변수가 200개 정도 있다고 할 때, 컴파일과 실행 다 되는데 나와야 하는 내용이 나오지 않는다면?**

if문 뒤에 소괄호 안에 있는 내용이 false여서 출력이 안 된 것이 아닌지 전부 확인해봐야 할 것입니다. 그런데, 어느 세월에 1만줄의 코드를 언제 읽으며, 100개의 if문을 언제 검토하며, 200개의 변수들을 검토하며 true인지 false인지 확인할 수 있을까요?? 아마, 확인하는데 **피땀눈물😢**을 흘리게 될 것입니다.


### boolean와 else

이러한 문제를 해결하기 위해, if문을 쓰기 앞서서, boolean 키워드를 사용하고, else문을 사용합니다. 먼저, boolean부터 살펴보도록 하겠습니다.

if문 코드 예시에서는

```
		boolean xyBool=x<y;
		System.out.println(xyBool);
		
		if (xyBool){
			System.out.println("true");
		} // end of xyBool keyword
```        

위의 코드가 boolean 연산을 사용한 if문 활용 예시입니다.

```
boolean xyBool=x<y;
-> boolean xyBool=x>y;
```

로 바꾼 것과

```
x<y -> y>x
```
로 바꾼 것을 비교하여 출력해보도록 하겠습니다.

```
// 클래스와 메서드 생략...
		int x=1;
		int y=2;

		boolean xyBool=x>y;
		System.out.println("xyBool >>> : "+xyBool);
		
		if (xyBool){
			System.out.println("false");
		} // end of xyBool keyword

		if (x > y) {
			System.out.println("false");
		}

```
if 문 소괄호 안에 내용이 전부 false이므로, 아무것도 출력되지 않는데,

xyBool >>> : false 내용은 출력됩니다.

이를 통해 xyBool연산이 false여서 if문의 내용이 출력되지 않았다는 것을 유추할 수 있습니다.

### boolean 연산과 if와 else문으로 사칙연산 해보기

> **else : if문 소괄호의 내용이 아닐 경우, else에서 출력할 수 있습니다.**

boolean 연산과 if, else문을 활용하여 사칙연산을 한 코드와 코드 해설을 끝으로 이번 포스팅을 마치도록 하겠습니다.

> **실습 코드**

```
package a.b.c.ch1;

public class FlowControl{

	public int add(int x, int y) {		
		return x + y;
	}

	public int subtract(int x, int y) {		
		return x - y;
	}

	public int multiply(int x, int y) {		
		return x * y;
	}

	public int divide(int x, int y) {		
		return x / y;
	}

	public static void main(String args[]) {
		int argsLength = args.length;
		boolean aBool = argsLength == 2;
		System.out.println("aBool >>> : " + aBool);
		
		if (aBool){
			String s0 = args[0];
			String s1 = args[1]; 
			
			int x = Integer.parseInt(s0);
			int y = Integer.parseInt(s1);

			FlowControl ef4 = new FlowControl();
			System.out.println("ef4 참조변수 주소값 >>> : " + ef4);
			
			int add = ef4.add(x, y);
			System.out.println("add >>> : " + add);
			
			int subtract = ef4.subtract(x, y);
			System.out.println("subtract >>> : " + subtract);
			
			int multiply = ef4.multiply(x, y);
			System.out.println("multiply >>> : " + multiply);
			
			int divide = ef4.divide(x, y);
			System.out.println("divide >>> : " + divide);

		}else{
			System.out.println("연산할 수를 잘 입력하시오 >>> : ");
		}
	}
}
```

> **코드 실행**

해당 코드를 실행 할 때, java a.b.c.ch1.FlowControl으로 입력하면,

```
aBool >>> : false
연산할 수를 잘 입력하시오 >>> :
```

와 같은 결과가 출력됩니다. 그 이유는 String args[]에 2개의 수가 입력이 되어야
더하기, 빼기, 곱하기, 나누기 함수에서 인수를 받아 결과값을 return 할 수 있기 때문입니다.

따라서, 2개의 수가 입력되지 않을 시 생기는 오류인지 확인하기 위해
```
		int argsLength = args.length;
		boolean aBool = argsLength == 2;
		System.out.println("aBool >>> : " + aBool);
        if (aBool){
        	... 생략 ...
        }
        else{
        	System.out.println("연산할 수를 잘 입력하시오 >>> : ");
        }
```
코드를 입력하였고, 그 결과 두 개의 인수값을 받아오지 못 했기 때문에 

```
aBool >>> : false
연산할 수를 잘 입력하시오 >>> :
```

다음과 같은 결과가 나온 것으로 해석 할 수 있습니다. 이 때, 콘솔창에서 java a.b.c.ch1.FlowControl 1 2로 입력하면,

```
ef4 참조변수 주소값 >>> : a.b.c.ch1.FlowControl@15db9742
add >>> : 3
subtract >>> : -1
multiply >>> : 2
divide >>> : 0
```

와 같이 잘 출력 되는 것을 볼 수 있습니다.


> **코드 해설**

```
int argsLength=args.length; 
```
main함수 소괄호안에 String args[]에서 args 배열의 길이를 argsLength라는 변수에 대입한 것입니다.

length는 length 필드라고도 하며, 배열의 길이를 구하는 함수 입니다. 반면, length()는 String클래스의 문자열의 길이를 구하는 함수입니다. 둘은 길이의 대상이 다르기 때문에 상황에 맞게 잘 써야 합니다.

```
boolean aBool=argsLength==2;
```
argsLength가 2인지 아닌지 true, false 결과를 aBool 변수에 대입한 코드입니다..

```
String s0 = args[0];
String s1 = args[1];
```

args 배열에 있는 원소들의 자료형은 String입니다. 해당 원소를 s0, s1이라는 변수에 할당하는 코드입니다.

```
int x = Integer.parseInt(s0);
int y = Integer.parseInt(s1);
```

Integer.parseInt(String s);는 문자 상수를 상수로 바꾸어 주는 코드입니다. 가령, "1"이라는 String s가 들어오면, 1이라는 상수로 바꾸어줍니다. 이 때 유의해야 할 것은 '1'은 char 자료형이므로 쓸 수 없습니다. 또한 "일"은 문자 상수가 아닌 문자이기 때문에 쓸 수 없습니다.


**이상으로 JAVA 배열과 조건문(if문)에 대한 포스팅을 마치도록 하겠습니다. 😊**
