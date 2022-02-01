이번에는 JAVA 기초: Keywords 1편에 이어서 2편으로 이어서 진행하도록 하겠습니다. 😄


# package

저번 Keywords 중에 [class](https://velog.io/@yunyoseob/JAVA-%EA%B8%B0%EC%B4%88-Keywords-1%ED%8E%B8)를 다뤘었는데요.

자바에서 클래스는 항상 package에 있어야 합니다.

여기서, package는 자바 디렉토리 또는 클래스 파일을 모아두는 곳입니다.

> 저번 HelloJava.java 포스팅에서는 단순히, "Hello Java"를 출력하고, 해당 코드를 설명하기 위해 package를 쓰지 않았습니다.

만약, Hello_Pack_1.java 파일을 실행하고자 할 때, 

```
package a.b.c.d;

public class HelloPack_1{

	public static void main(String args[]){
		
		System.out.println("패키지는 디렉토리이다");
	}
}
```

이런 식으로 코드를 짜고 저번 포스팅 처럼 컴파일과 자바파일 실행을 진행하면 오류가 출력됩니다.

> 콘솔창에 다음과 같은 명령어를 입력하면, 오류가 나타나게 됩니다.

```
javac HelloPack_1.java
java HelloPack_1
```

![hellopack](https://user-images.githubusercontent.com/81727895/151694631-4f977f84-89df-47ad-8fe0-0662b02e73bd.JPG)

오류가 나타나는 첫 번째 이유는 javac 명령어로 컴파일시 해당 디렉토리에서 컴파일 하지 않았기 때문이고, 두 번째 이유는 java 명령어로 실행시 패키지 경로에 있는 자바 파일을 실행하지 않았기 때문입니다.

따라서,

```
javac -d . HelloPack_1.java
java a.b.c.d.HelloPack_1
```

![hellofd](https://user-images.githubusercontent.com/81727895/151694756-3606fee7-5e12-411f-9095-f9f9871b7e6d.JPG)

명령어로 실행을 해주어야 자바파일이 실행이 됩니다.

> 아까와는 달리 컴파일 과정에서 -d와 .(도트 연산자)가 추가됐고, java 파일 실행시 a.b.c.d가 추가 됐는데 뭐가 달라진 건가요?

>  -d는 "-d <directory> Specify where to place generated class files"를 의미합니다. 즉, class 파일이 있는 경로에 대한 명령어를 추가해준 것입니다.

> . (도트 연산자)는 현재 디렉토리를 의미합니다. 도트 연산자 대신 현재 경로를 넣어주셔도 됩니다.
  
> java파일 실행시 a.b.c.d.HelloPack_1은 a안에 b안에 c안에 d안에 있는 HelloPack_1 자바파일을 실행하라는 의미입니다.
  
> java HelloPack_1이 실행되지 않는 이유는 HelloPack_1이 있는 경로에서 자바파일 실행을 해야하는데 그렇게 하지 않았기 때문입니다.
 
# Byte

java에서 class는 java 프로그램의 최소 단위로, class는 변수와 함수로 이루어져 있습니다.
  
java에서 변수는 크게 기초 자료형(primitive type)과 참조 자료형(reference type)이 있습니다.
  
java는 [객체지향언어](https://ko.wikipedia.org/wiki/%EA%B0%9D%EC%B2%B4_%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)이기 때문에, java에서 사용하는 모든 자원은 객체이어야 합니다.

객체에 대한 설명은 잠시 뒤로, 하고 이번에는 기초자료형 중에 숫자 자료형의 Keyword중 Byte에 대해 먼저, 포스팅해보도록 하겠습니다. 😃
  
[자바 공식문서 : Java Platform, Standard Edition 8 API Specification](https://docs.oracle.com/javase/8/docs/api/)를 보면, 
  
> BYTES : The number of bytes used to represent a byte value in two's complement binary form

라고 적혀있습니다. 
  
BYTE에 대해 이해하기 위해서는 BIT에 대한 이해가 있어야 하는데요. 
  
BIT와 BITE를 비교하면 다음과 같습니다.
  
|BIT|BYTE|
|---|----|
|컴퓨터 내부를 구성하는 반도체가 데이터를 표현할 수 있는 최소 단위|자바에서 데이터의 최소단위|

> BIT가 8개가 모이면 8BIT이고, 8BIT가 1BYTE입니다.
  
![bite](https://user-images.githubusercontent.com/81727895/151909719-b4f68d6f-8eb7-433e-b131-e9bc47c0f4f3.JPG)

공식문서에 의하면, BITE의 최댓값은 2^7-1이고, 최소값은 -2^7입니다. 위에서 다뤘듯, byte는 8개의 bit가 모인 것으로,
byte의 size는 8입니다.
  
![byte2](https://user-images.githubusercontent.com/81727895/151910140-b569e1cf-a8fa-4ec3-acc2-dcefa5894791.JPG)

코드를 실행하면,
 
![byte3](https://user-images.githubusercontent.com/81727895/151910191-3fa4f82e-d34f-4745-bb41-7297e169fb43.JPG)

결과가 나오는 것을 볼 수 있습니다.

> bite의 최소값보다 더 작은 수를 입력하면,
 
![byte4](https://user-images.githubusercontent.com/81727895/151910400-58774424-ba23-4019-ad55-3543739ffb42.JPG)

![byte5](https://user-images.githubusercontent.com/81727895/151910407-80f895bf-79d0-4576-b859-bb21fee07dfe.JPG)

오류가 출력됩니다.
  
# Integer

 Integer는 숫자를 담당하는 클래스입니다.
  
[자바 공식문서 : Java Platform, Standard Edition 8 API Specification](https://docs.oracle.com/javase/8/docs/api/)를 보면, 

![integer](https://user-images.githubusercontent.com/81727895/151910767-39b6b3fc-a9c2-4894-bb2c-8e99a090200a.JPG)

다음과 같이 기술되어 있는 것을 볼 수 있습니다.
  
> BITES와는 달리, MAX_VALUE가 더 크고, MIN_VALUE가 더 작은 것을 볼 수 있습니다.
  
아래와 같은 코드를 입력하면,
  
```
// 클래스와 함수 부분은 생략...
int intBytes = Integer.BYTES;	
int intMax = Integer.MAX_VALUE;
int intMin = Integer.MIN_VALUE;
int intBits = Integer.SIZE;
 
System.out.println("int intBytes >>> : " + intBytes);
System.out.println("int intMax >>> : " + intMax);
System.out.println("int intMin >>> : " + intMin);
System.out.println("int intBits >>> : " + intBits);  
```

![integer2](https://user-images.githubusercontent.com/81727895/151911190-b761e801-98f2-45e5-a814-4ae7703df20b.JPG)

다음과 같은 결과가 출력되는 것을 볼 수 있습니다.
  
# Long
마지막으로, long이라는 키워드에 대한 설명으로 이번 포스팅을 마치도록 하겠습니다.

이전에 Integer의 최댓값을 보았을 때, 2,147,483,647까지가 최댓값인 것을 확인했었습니다.
  
그러나, 2,147,483,647보다 큰 수를 다뤄야 한다면, Integer를 사용할 수 없을 것입니다. 이럴 경우, long이라는 키워드를 사용합니다.

다음과 같은 코드를 입력하게 되면,
```
// 클래스와 함수 부분은 생략...
int intMax = Integer.MAX_VALUE;
long longMax = Long.MAX_VALUE;
  
System.out.println("intMax >>> : " + intMax);
System.out.println("longMax >>> : " + longMax);
```
  
![loong](https://user-images.githubusercontent.com/81727895/151911650-11e23383-24fa-4322-9718-2fc20ac8ae9c.JPG)

Long.MAX_VALUE가 Integer.MAX_VALUE보다 최댓값보다 훨씬 큰 것을 확인 할 수 있습니다.
 
> 여기서 유의해야 할 사항은 long 명령어를 사용할 때, 숫자 마지막에 L 혹은 l을 반드시 붙여줘야 합니다.
  
만일 코드를
  
```
// 클래스와 함수 부분은 생략...
long num3 = 9223372036854775807;		
System.out.println("long num3 >>> : " + num3);

long num4 = 9223372036854775807;		
System.out.println("long num4 >>> : " + num4);
```
  
이렇게 쓰게 되면, javac 명령어 실행시,
  
![long2](https://user-images.githubusercontent.com/81727895/151911906-bd0ef7c4-a59c-4c86-a008-f07a191aa70b.JPG)

오류를 만나게 됩니다.
  
마지막 숫자 뒤에 l 혹은 L을 써서
```
// 클래스와 함수 부분은 생략...
long num3 = 9223372036854775807L;		
System.out.println("long num3 >>> : " + num3);

long num4 = 9223372036854775807l;		
System.out.println("long num4 >>> : " + num4);
```
이렇게 작성해 주셔야,
  
![long3](https://user-images.githubusercontent.com/81727895/151912015-306e5c1f-a49e-4689-9be8-e2aefb680e2a.JPG)

정상적으로 실행이 됩니다!! 😄
  
**이번 포스팅은 여기서 마치도록 하겠습니다~!**





