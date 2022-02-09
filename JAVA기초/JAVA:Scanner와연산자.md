안녕하세요. 😀 오늘은 JAVA에서 Scanner와 연산자에 대해 포스팅하도록 하겠습니다.

### 들어가기 전에...

저번 포스팅 [JAVA 배열과 조건문(if문)](https://velog.io/@yunyoseob/JAVA-%EB%B0%B0%EC%97%B4%EA%B3%BC-%EC%A1%B0%EA%B1%B4%EB%AC%B8if%EB%AC%B8)에서 마지막에 boolean 연산과 if와 else문으로 사칙연산 한 거 기억나시나요??

사실 해당 코드는 Scanner를 사용하면 좀 더 편리하게 사칙연산 코드를 작성할 수 있습니다.

> **실습 코드**

```
package a.b.c.ch1;

import java.util.Scanner;

public class FlowControl_2{

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
		Scanner sc=new Scanner(System.in);

		System.out.println("\n 첫 번째 숫자를 입력하세요.");
		int x=sc.nextInt();
		System.out.println("\n 두 번째 숫자를 입력하세요.");
		int y=sc.nextInt();

		System.out.println("\n Scanner를 통해 입력한 첫 번째 숫자 >>> :"+x);
		System.out.println("\n Scanner를 통해 입력한 두 번째 숫자 >>> :"+y);
		
		FlowControl_2 iarr=new FlowControl_2();
		int add = iarr.add(x, y);
		System.out.println("\n add >>> : " + add);
			
		int subtract = iarr.subtract(x, y);
		System.out.println("\n subtract >>> : " + subtract);
			
		int multiply = iarr.multiply(x, y);
		System.out.println("\n multiply >>> : " + multiply);
			
		int divide = iarr.divide(x, y);
		System.out.println("\n divide >>> : " + divide);
	}
}
```

**출력 결과**

![](https://images.velog.io/images/yunyoseob/post/dd1b1284-f986-4bdf-a71b-789943c58bbb/image.png)

## 코드 해설과 함께하는 Scanner 설명

> **import java.util.Scanner;**

이제까지 단, 한 번도 import 명령어를 사용한적이 없는데, import를 안 해도 문제가 없었던 이유는 import java.lang.* 기본적으로 java에 내장되어 있었기 때문입니다.

java.lang 패키지에 있지 않은 클래스인 경우, 해당 패키지의 클래스를 import 키워드를 사용하여야 합니다.

이 때 유의사항은 

```
java -version
```
명령어를 통해 꼭 버전을 확인한 후에, import를 해야 합니다.

![](https://images.velog.io/images/yunyoseob/post/28694ae7-5a5b-464d-8038-0e1d86ddab5e/image.png)

이유는 다음과 같습니다.

[Java 8 api](https://docs.oracle.com/javase/8/docs/api/)에서 java.util을 클릭한 뒤, Scanner를 클릭할 경우

![](https://images.velog.io/images/yunyoseob/post/1ab5ccbf-62c9-4b73-ad50-9ed9fd4c5588/image.png)

다음과 같은 창이 나옵니다. 스크롤을 내리다 보면

```
Since:
1.5
```
를 확인할 수 있습니다. [Java SE에서 downloads](https://www.oracle.com/java/technologies/downloads/archive/)를 할 때, 버전을 보면

![](https://images.velog.io/images/yunyoseob/post/fcb4eca6-cc71-4783-8abd-fbbdbd044970/image.png)

버전이 다양한 것을 볼 수 있습니다.

![](https://images.velog.io/images/yunyoseob/post/637d0bbb-b145-4403-b203-1243e5e67a81/image.png)

해당 버전을 잘 체크하셔서 내가 사용하고 있는 Java 버전에서 import를 할 수 있는지 없는지 꼭 체크해야 합니다.

- 또한 import 할 때, 패키지명.클래스이름으로 사용하셔야 합니다. import.java.util.*으로 import 하게 된다면 import.java.util에 있는 모든 클래스들을 불러올 수 있습니다. 그러나 소스코드의 가독성 때문에 가급적이면 사용하고자 하는 클래스명까지 써서 import 하는 것을 개인적으로 추천합니다. 😀


> **Scanner sc = new Scanner(System.in);**

공식문서에서 Scanner를 사용할 때, 코드입니다. System.in은 [Java 8 api](https://docs.oracle.com/javase/8/docs/api/)에서 java.lang을 누르고, System을 클릭하시면,

Field Summary에 다음과 같은 화면이 뜹니다.

![](https://images.velog.io/images/yunyoseob/post/e57cafe6-89ae-4af0-8eae-d11e5340a2b4/image.png)

java에서 System의 구조는 다음과 같습니다.

![](https://images.velog.io/images/yunyoseob/post/182c9ec5-9bd7-47d8-83f6-efacc4fb9a20/image.png)

System.in과 System.out은 System에 키인한 내용이 들어가는 것과 소스코드에서 개발자가 볼 수 있게 콘솔창으로 출력하는 명령어입니다.


> **int x=sc.nextInt();**


[Java 8 api](https://docs.oracle.com/javase/8/docs/api/)에서 java.util을 클릭한 뒤, Scanner를 클릭한 다음, ctrl+f를 통해 nextInt를 검색하면 다음과 같이 설명되어 있습니다.

|Modifier and Type|Method and Description|
|--|--|
|int|nextInt() Scans the next token of the input as an int.|

nextInt()를 클릭하면, 

![](https://images.velog.io/images/yunyoseob/post/4f8a74b0-b6b0-4b9c-b51c-8248bb36acad/image.png)

다음과 같이 사용방법을 보실 수 있습니다. 

- Scanner.nextInt()가 아닌 sc.nextInt()를 한 이유는 static이 없기 때문에 객체로 할당하여 사용해야 하기 때문입니다.

> **FlowControl_2 iarr=new FlowControl_2();**

이 와는 별개로 add, substract, multiply, divide 함수는 static 명령어가 없기 때문에 클래스 전체를 new 명령어를 통해 생성자를 만들어서 객체를 만들어 줍니다.

> **int add = iarr.add(x, y);**

마지막으로 참조변수.실행하고자하는함수()에 인수들을 입력한 다음 이를 int 변수에 대입하여 줍니다. 함수들을 보면 4개의 함수 전부 public int 함수이름(int 파라미터1, int 파라미터2);로 구성되어 있고, 4개의 함수의 return 값 역시 int 자료형입니다.

따라서, int형 자료형인 인수 2개가 함수에 들어간 뒤, int형인 return 값을 대입연산자를 통해 int add에 대입해주는 과정입니다.

## 연산자

java에서 연산자의 종류가 많지만 이번 포스팅에서는 증감 연산자와 삼항 연산자, 논리 연산자, 관계연산자만 다뤄보도록 하겠습니다.

> **증감 연산자 : increment and decrement operators**

```
++x		
x 를 먼저 1 증가 시킨 후 그 값을 사용	
--x	: x 를 먼저 1 감소 시킨 후 그 값을 사용	
x++ : x 값를 먼저 사용한 후 1 증가 
x--	: x 값를 먼저 사용한 후 1 감소 
```

**주의해야 할 사항**

```
// 클래스와 메소드 생략..

		int aX = 10;
		System.out.println(aX);
		
		aX++; // aX = aX + 1 --> 10 = 10 + 1;
		System.out.println(aX);

		++aX;
		System.out.println(aX);


		int aXX = 100;
		System.out.println(aXX);

		int aa = aXX++; // int aa = aXX = aXX + 1		
		System.out.println(aa);		
		
		aa = ++aXX;
		System.out.println(aa);
```

다음과 같이 입력하면, 순서대로 10,11,12,100,100,102가 출력됩니다.

aX++;으로 입력하나, ++aX;으로 입력하나 똑같이 1이 증가합니다. 그러나, int aa = aXX++; 명령어를 입력 후 출력하면 똑같이 100이 나오고, aa= ++aXX;를 입력하면 100에서 101이 아니라, 102가 출력 됩니다.

따라서, int aa=aXX++; 와 같은 명령어는 지양하는 것이 좋습니다.

**🤔 마지막에 102가 출력된 이유?**

마지막으로, 102가 출력하는 이유는 Java는 함수 블록 내에서 인터프리터 방식으로 실행이 됩니다. 따라서 aa=++aXX; 명령어 실행 이전에 int aa=aXX++; 명령어에서 aXX가 1이 증가하여, 101이 이미 됐는데, int aa에 대입이 되지 않고 있다가 aa=++aXX; 명령어 실행 후, aXX가 1이 더 증가하여 102가 된 상태로 aa에 대입이 되어 102가 출력 된 것입니다.

> **삼항 연산자 : ternary operator**

이제까지 조건문의 경우 if, else문만 사용했으나, 삼항 연산자를 통해서도 조건식을 만들 수 있습니다.

```
사용방법
조건식 ? 결과1 : 결과2

코드예시
int A=10;
int B=11;

char ch = ' ';

ch = (A>B) ? 'T' : 'F';

출력결과 : F

```

조건식에서 조건식이 맞을 경우 결과1을 출력하며, 조건식이 틀릴 경우 결과2를 출력합니다.

저번 포스팅 [JAVA 배열과 조건문(if문)](https://velog.io/@yunyoseob/JAVA-%EB%B0%B0%EC%97%B4%EA%B3%BC-%EC%A1%B0%EA%B1%B4%EB%AC%B8if%EB%AC%B8)에서 if문을 쓸 때, boolean 연산자를 같이 쓰는 방법에 대해서도 포스팅했었습니다.

삼항 연산자의 경우에도 boolean 연산자를 같이 쓸 수 있습니다. 이는 논리 연산자를 통해
설명하도록 하겠습니다.

> **논리 연산자**

논리 연산자 중 이번 포스팅에서는 논리 곱 연산과 논리 합 연산만 다뤄보도록 하겠습니다. 😊

**논리 곱 (&&) 연산**

```
T AND T -> T
T AND F -> F
F AND T -> F
F AND F -> F
```

**논리 합 (&&) 연산**

```
T OR T -> T
T OR F -> T
F OR T -> T
F OR F -> F
```

어디서 많이 본 것 같지 않나요?? 🤔

이는 [비트연산](https://ko.wikipedia.org/wiki/%EB%B9%84%ED%8A%B8_%EC%97%B0%EC%82%B0)의 규칙과 똑같습니다.

**쉬운 설명 😁**

논리 곱과 논리 합을 쉽게 설명하면, boolean의 default 값은 false인데, 논리 곱의 경우, 논리 곱 양쪽이 전부 true여야, default 값인 false가 true로 움직입니다. 

반면, 논리 합의 경우 논리 합 양쪽 중에 하나라도 true면 default 값인 true로 움직입니다. 논리 곱의 조건이 논리 합보다 더 까다롭다고 볼 수 있습니다.

> **논리 연산자 : Short Circuit 현상**
 
Short Circuit 현상이란 단락 회로 평가(Short Circuit Evaluation : SCU)에서 논리 곱과 논리 합 연산을 할 때 두 항을 모두 실행하지 않더라도 결과 값을 알 수 있는 경우, 나머지 항이 실행되지 않는 것을 의미합니다.

> **삼항 연산자에서 논리 연산을 사용하면 좋은 이유**

아까, 삼항 연산자에서 논리곱인 경우 첫 번째 항이 False라면 두 번째 항의 결과를 보지 않아도 이미 결과가 False인 것을 알 수 있습니다. 이럴 경우 Short Circuit 현상으로 컴퓨터는 두 번째 항의 결과를 실행하지 않습니다.

논리합인 경우도 마찬가지로 첫 번재 항이 True라면 두 번째 항의 결과를 보지 않아도 이미 결과가 True인 것을 알 수 있습니다. 이럴 경우 마찬가지로 컴퓨터는 두 번째 항의 결과를 실행하지 않습니다.

```
boolean value = (조건식A) && (조건식B);
```

가령, 위의 코드가 있을 때, Short Circuit 현상을 방지 하기 위해

```
boolean v1=조건식A;
boolean v2=조건식B;
boolean value = (조건식A) && (조건식B);
```

다음과 같이 코드를 작성하고, v1, v2, value 모두 출력한다면 향후 Short Circuit 현상으로 인한 문제가 발생했을 시, 문제를 해결하기 더 쉬워집니다.


> **관계 연산자**

관계 연산자의 경우,

```
boolean bool0 = 1>2;
boolean bool1 = 'a' > 'b';
boolean bool2 = 'A'>'b';
```

모두 결과를 출력해서 확인 할 수 있습니다.

**🤔 문자(char)도 비교할 수 있는 이유??**

[ASCII 코드](https://ko.wikipedia.org/wiki/ASCII)란 미국정보교환표준부호로 7비트 인코딩을 의미합니다. [ANSI 코드](https://namu.wiki/w/ANSI)는 ASCII 코드를 확장한 코드입니다.

[Unicode 코드](https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%88%EC%BD%94%EB%93%9C)는 ASCII 코드의 확장판으로 전 세계의 모든 문자를 컴퓨터에서 일관되게 표현하고 다룰 수 있도록 설계된 산업 표준입니다. ( ex : UTF-8, UTF-16 ...)

원래 미국에서 ASCII 코드를 쓰다가 전세계에서 활용하면서 영문자 대문자 소문자만 인코딩하는 것에 한계가 있었고, 이러한 점을 보완하기 위해, ANSI코드 Unicode코드가 등장하게 된 것입니다.

- 한글 Windows의 경우 [CP949](https://namu.wiki/w/CP949)를 사용합니다.

이전 [JAVA 자료형 : 문자와 문자열](https://velog.io/@yunyoseob/JAVA-%EC%9E%90%EB%A3%8C%ED%98%95-%EB%AC%B8%EC%9E%90%EC%99%80-%EB%AC%B8%EC%9E%90%EC%97%B4) 포스팅에서 

```
알아두면 좋은 사항 : JVM에서 컴파일할 때, JAVA는 어떤 데이터 자료형으로 들어와도 int 밖에 모릅니다.
```
위의 내용을 작성했었습니다. JAVA는 문자가 들어오면 이를 int형으로 처리하기 때문에 char 데이터 타입의 관계 연산이 가능합니다.

**ANSI characters 예시**

![](https://images.velog.io/images/yunyoseob/post/5243ac73-9d0c-4aca-9a3f-f0aed28b624b/image.png)

![](https://images.velog.io/images/yunyoseob/post/7c032bac-0220-418f-9206-735e16117038/image.png)

- [Java 8 api](https://docs.oracle.com/javase/8/docs/api/)에서 볼 수 있듯, 2진수, 8진수, 16진수에 따라 int로 변환되는 숫자가 다릅니다.

### 아이디, 비밀번호 입력받아 체크하는 코드 만들기

마지막으로 java.lang의 기존 내장 패키지로만 아이디, 비밀번호를 입력받아 체크하는 프로그램과
java.util.Scanner를 활용하여 아이디, 비밀번호를 입력받는 코드를 만들어 실습을 마지막으로, 이번 포스팅을 마치도록 하겠습니다.  😊

```
아이디 : velog
비밀번호 : @yunyoseob
```

> **java.lang만으로 만들어본 실습 코드**

```
package velog.homepage.login;

public class Login_check{
	public boolean idcheck(String id, String pw){
		System.out.println("\n idcheck 시작 >>>>> \n");
		System.out.println("\n 입력하신 아이디는 "+id+" 입니다.\n");
		System.out.println("\n 입력하신 비밀번호는 "+pw+" 입니다. \n");
		boolean bool=false;
		// 지역변수는 그 자료형의 default 값으로 초기화 해서 사용한다.
		System.out.println("\n 지역변수의 bool 연산자의 default 값 >>> : "+bool);
	
		if ( id!=null && id.length() >0)
		{
			System.out.println("\n idcheck 에서 다시 확인한 id >>> : "+id);
			System.out.println("\n idcheck 에서 다시 확인한 password >>> : "+pw);
			
			if("velog".equals(id)&&"@yunyoseob".equals(pw)){
				System.out.println("\n 아이디가 맞는지 확인이 되었습니다. \n");
				System.out.println("\n 비밀번호가 맞는지 확인이 되었습니다. \n");
				bool=true;
			} // end of if 안에 if
			else{
				System.out.println("\n 아이디 혹은 비밀번호가 틀립니다. \n");
			} // end of if 안에 else
		} // end of if
		// id!=null && id.length()는 id가 null값인지 확인하고
		// id의 배열의 길이가 아니라, 문자열 길이가 0보다 큰지 확인한다. 
        
		System.out.println("\n 아이디와 비밀번호 둘 다 맞으면 true 아니면 false >>> : "+bool);
		return bool;
	} // end of idcheck method


	public static void main(String args[]){
		System.out.println("\n main method 시작 >>>> \n");
		int argsLength=args.length;
		System.out.println("\n 들어온 String 배열의 길이 >>> : "+argsLength);

		boolean aBool=argsLength ==2;
		// 배열의 길이가 2인지 아닌지 boolean으로 체크하기
		System.out.println("\n 배열의 길이가 맞으면 true 아니면 false >>> :"+aBool);

		 //if else 문 사용해서 구별하기
		if (aBool){
			String id=args[0];
			String password=args[1];
			System.out.println("\n 첫 번째 배열 >>> : "+id);
			System.out.println("\n 두 번째 배열 >>> : "+password);
			Login_check lc=new Login_check();
			// idcheck는 static이 없으므로, 객체로 올려준다.
			System.out.println("\n 객체 생성하였으니 idcheck로 id, password 넘겨주기 \n");

			boolean finalbool=lc.idcheck(id, password);
			// idcheck에 id, password 입력해서 결과 출력하기
			System.out.println("\n 마지막으로 체크해서 아이디와 패스워드를 모두 잘 입력했다면 true, 아니면 false >>> :"+finalbool);

			// public boolean idCheck(String id, String pw)
			// boolean bool=lc.idcheck(id, password);
		} // end of if
		else{
			System.out.println("다시 입력하세요.");
		} // end of else
	} // end of main method
} // end of Login_check class
```

**명령문 실행**

```
javac -d . Login_check.java
java velog.homepage.Login_check velog @yunyoseob
```

**출력 결과**

![](https://images.velog.io/images/yunyoseob/post/9e5d552f-b139-43d7-b515-adff0d1c863a/image.png)

**비밀번호랑 아이디 반대로 작성하여 실행**
```
javac -d . Login_check.java
java velog.homepage.Login_check @yunyoseob velog
```

**출력 결과**

![](https://images.velog.io/images/yunyoseob/post/e75525cf-0e77-4762-b7c8-b66f600320f0/image.png)

> **java.util.Scanner으로 만들어본 실습 코드**

```
package velog.homepage.login;

import java.util.Scanner;

public class Login_check{
	public boolean idcheck(String id, String pw){
		System.out.println("\n idcheck 시작 >>>>> \n");
		System.out.println("\n 입력하신 아이디는 "+id+" 입니다.\n");
		System.out.println("\n 입력하신 비밀번호는 "+pw+" 입니다. \n");
		boolean bool=false;
		// 지역변수는 그 자료형의 default 값으로 초기화 해서 사용한다.
		System.out.println("\n 지역변수의 bool 연산자의 default 값 >>> : "+bool);
		
		if ( id!=null && id.length() >0)
		{
			System.out.println("\n idcheck 에서 다시 확인한 id >>> : "+id);
			System.out.println("\n idcheck 에서 다시 확인한 password >>> : "+pw);
			
			if("velog".equals(id)&&"@yunyoseob".equals(pw)){
				System.out.println("\n 아이디가 맞는지 확인이 되었습니다. \n");
				System.out.println("\n 비밀번호가 맞는지 확인이 되었습니다. \n");
				bool=true;
			} // end of if 안에 if
			else{
				System.out.println("\n 아이디 혹은 비밀번호가 틀립니다. \n");
			} // end of if 안에 else
		} // end of if
		// id!=null && id.length()는 id가 null값인지 확인하고
		// id의 배열의 길이가 아니라, 문자열 길이가 0보다 큰지 확인한다. 
		System.out.println("\n 아이디와 비밀번호 둘 다 맞으면 true 아니면 false >>> : "+bool);
		return bool;
	} // end of idcheck method


	public static void main(String args[]){
		System.out.println("\n main method 시작 >>>> \n");		
		// scanner 사용해서 간단하게 구현하기
		Scanner sc=new Scanner(System.in);

		// public String nextLine()
		System.out.println("\n 아이디를 입력하세요 :     ");
		String x=sc.nextLine();
		System.out.println("\n 비밀번호를 입력하세요 :     ");
		String y=sc.nextLine();

		System.out.println("\n Scanner를 통해 입력한 아이디 >>> :"+x);
		System.out.println("\n Scanner를 통해 입력한 비밀번호 >>> :"+y);

		boolean aBool= x.length()>0 && y.length()>0;
		System.out.println("\n 아이디와 비밀번호의 길이가 둘 다 0이 아니면 true, 둘 중 하나라도 0이면 false >>> : "+aBool);

		// if else 문 사용해서 구별하기
		if (aBool){
			Login_check lc=new Login_check();
			// idcheck는 static이 없으므로, 객체로 올려준다.
			System.out.println("\n 객체 생성하였으니 idcheck로 id, password 넘겨주기 \n");

			boolean finalbool=lc.idcheck(x, y);
			// idcheck에 id, password 입력해서 결과 출력하기
			System.out.println("\n 마지막으로 체크해서 아이디와 패스워드를 모두 잘 입력했다면 true, 아니면 false >>> :"+finalbool);

			// public boolean idCheck(String id, String pw)
			// boolean bool=lc.idcheck(id, password);
		} // end of if
		else{
			System.out.println("다시 입력하세요.");
		} // end of else
		

	} // end of main method
} // end of Login_check class
```

**명령문 실행**

```
javac -d . Login_check.java
java velog.homepage.Login_check

velog

@yunyoseob
```

**출력 결과**

![](https://images.velog.io/images/yunyoseob/post/e4da6db3-dd88-488e-af4f-7c75dd8bf8c5/image.png)

**비밀번호랑 아이디 반대로 작성하여 실행**
```
javac -d . Login_check.java
java velog.homepage.Login_check

@yunyoseob

velog
```

**출력 결과**

![](https://images.velog.io/images/yunyoseob/post/275dcf48-7a0c-416e-bd4f-bed4f0a07f08/image.png)

**코드 내용을 보면 유난히 System.out.println();이 많은 것을 확인할 수 있습니다. 이는 코드가 길 때, 코드의 출력과정을 개발자가 눈으로 확인하여 순차적으로 잘 실행되고 있는지를 확인하기 위함입니다. 이를 전문용어로 로그를 찍어서 본다고 할 수 있습니다.**

**이상으로 JAVA Scanner와 연산자 포스팅을 마치도록 하겠습니다. 😊**
