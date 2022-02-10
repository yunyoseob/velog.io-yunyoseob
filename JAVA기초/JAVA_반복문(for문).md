안녕하세요 😄 오늘은 JAVA에서 반복문 중 for문에 대해 포스팅하도록 하겠습니다.

## 반복문(for문)

예전에 [함수와 변수 : 1부터 10까지 함수들을 연결해서 출력하는 예제](https://velog.io/@yunyoseob/%ED%95%A8%EC%88%98%EC%99%80-%EB%B3%80%EC%88%98)에서

함수의 리턴 값을 받아 1부터 10까지 합을 출력하는 예제를 올린 적이 있습니다. 

해당 코드는 무려, 86줄에 거쳐 작성이 되었었는데요. for문을 사용하는 것만으로
해당 코드를 11줄로 줄일 수가 있습니다.

> **1부터 10까지 합 출력 코드**

```
package a.b.c.ch1;

public class Add_One_To_Ten_2{
	public static void main(String args[]){		
		int sum=1;	
		for (int i=0; i<9; i++){
			System.out.println(" 1부터 "+(i+2)+"까지의 합 >>> :"+(sum+i+2)+"\n");
			sum=sum+i+2;
			}
	} // end of main method
} // end of Gugu_2 class
```

### for문 사용 방법

```
for (초기화식; 조건식; 증감식){
	System.out.println(출력하고자 하는 내용);
}
```

for문은 다음과 같이 이루어져 있습니다.

```
초기화식은 데이터 타입 변수 = 값

조건식은 boolean = 조건;
```

증감식은 초기화 식에 선언한 변수를 이용해서 증감식을 사용합니다.

증감식 연산자는 전위, 후위, ++, --, 배수 무엇이든 사용가능합니다.

> **JAVA에서는 for 키워드를 JVM이 보면 for 키워드 뒤에 ()가 있으면 무조건 반복 수행합니다.**

```
for (int i=0; ; ){
	System.out.println("---");
}
```

위의 코드와 같이 실행하면 무제한으로 ---이 출력됩니다.

-  Tip : Ctrl + c를 눌러서 무제한으로 실행되는 것을 멈출 수 있습니다.

> **변수를 for문 소괄호 안에서 값을 선언후 대입한 것과 for문 소괄호 밖에서 선언 후, 소괄호 안에서 대입한 것은 다르다.**

**1. for문 소괄호 안에서 선언 후 0을 대입한 뒤, for문 블럭 밖에서 출력***

```
		for (int i=0; i<3; i++){
			System.out.println("("+i+"< 3) >>> : "+(i<3));
			System.out.println("for {} 블럭 내부 ::: i >>> : "+i);
		}

		System.out.println("for {} 블럭 외부 ::: i >>> : "+i);
```

javac 명령어로 컴파일 과정에서부터 에러가 납니다. 

**"error : cannot find symbol"**

for문 블럭 밖에서 i를 출력시키면, for문을 제외한 함수 블록내에서 아무리 i를 찾아봐도

변수를 선언한 적이 없기 때문에 symbol을 찾을 수 없다는 에러가 출력됩니다.


**2. for문 소괄호 밖에서 선언 후 for문 블럭 밖에서 출력**

```
		int i;
		for (i=0; i<3; i++){
			System.out.println("("+i+" < 3) >>> : "+(i<3));
			System.out.println("for {} 블럭 내부 ::: i >>> : "+i);
		}
		System.out.println("for {} 블럭 외부 ::: i >>> : "+i);
```   

출력 결과 : 0,1,2,3이 출력 됩니다.

> **마지막 출력 결과가 3이 출력된 이유**

🤔 for문 소괄호에 초기화식과 조건식을 보았을 때, i가 2까지만 실행될 수 있으니, for문 블럭 밖에서 출력하면 2가 나와야 하는 것 아닌가요??

해당 코드에서 for문이 작동하는 방식은 다음과 같습니다.

```
1. int 자료형에 i가 선언 됐는데 for문을 진행해주세요.

2. i에 0을 대입해주세요.

3. i가 3보다 작나요? true (이 때 i는 0)

4. i와 i<3의 여부를 출력해주세요.

5. 이제 i에 1을 더해주세요.

6. i가 3보다 작나요? true (이 때 i는 1)

7. i와 i<3의 여부를 출력해주세요.

8. 이제 i에 1을 더해주세요.

9. i가 3보다 작나요? false (이 때 i는 3)

10. for문을 종료하도록 하겠습니다.

11. for문 블럭밖 : i를 출력해주세요 -> 3 출력
```

**for문은 초기화식 -> 조건식 -> true면 실행 -> 변수값 증감을 반복하다가, 
조건식에서 false면 for문을 종료하고 for문 밖에서 이를 출력할 경우 저장된 변수값을 출력한다.**

> **for문에서 처음 시작 값을 0으로 보통 시작하는 이유**

JAVA에서 for 문 초기화 식에서 항상 초기화 값을 0으로 하는데, 그 이유는 for 대부분
배열 데이터를 처리하는데 사용하기 때문입니다. (배열의 인덱스는 0부터 시작합니다.)

🤔 **반드시 0부터 시작을 해야 하나요?**

아닙니다. 만약, 다음과 같은 코드를 출력시, 

```
package a.b.c.ch1;

public class For_p_3{
	public static void main(String args[]){
		System.out.println("<<< main 함수 시작 >>>\n");

	// for문을 통해 출력하고자 하는 것 : 0,1,2,3,4

	// 초기화 식을 int i=0으로 시작

	// 1번째 방법
	for (int i=0; i<5 ; i++){
		System.out.println("\n 1번째 방법 : i 값은 >>> : "+i);
	}
    System.out.println("\n-----------------");
	
	// 2번째 방법
	for (int i=0; i<=4; i++){
		System.out.println("\n 2번째 방법 : i 값은 >>> : "+i);
	}
    System.out.println("\n-----------------");

	// 초기화 식은 int i=1으로 시작

	// 3번째 방법
	for (int i=1; (i-1)<5; i++){
		System.out.println("\n 3번째 방법 : i 값은 >>> : "+(i-1));
	}
    System.out.println("\n-----------------");

	// 4번째 방법
	for (int i=1; i<=5; i++){
		System.out.println("\n 4번째 방법 : i 값은 >>> : "+(i-1));
	}
    System.out.println("\n-----------------");
	} // end of main method
} // end of For_p_3 class
```
![](https://images.velog.io/images/yunyoseob/post/6cf12f94-7927-48ac-b75c-65850f8f6d7c/image.png)

전부 초기화식이 달라도, 결과는 전부 0,1,2,3,4가 출력되는 것을 확인 할 수 있습니다.

마지막으로 if문, for문, Scanner를 활용하여, 지역변수 5개를 콘솔에 16진수 출력하는 실습 코드를 올려드리면서 이번 포스팅은 마무리 하도록 하겠습니다. 🙂

### 지역변수 5개를 콘솔에 16진수 출력하기 실습

```
package a.b.c.ch1;

import java.util.Scanner;

public class ConvertHex{

	public void toHex_Str(String str) {
		System.out.println("ConvertHex.toHex_Str() 함수 진입 >>> : ");

		if (str !=null && str.length() > 0){
			char c = ' ';
			for (int i=0; i < str.length(); i++ ){
				c = str.charAt(i);
				System.out.print(c + " ");
				System.out.print("0x" + Integer.toHexString(c) + " ");
				System.out.println();
			}
		}
	}
	
	public static void main(String args[]) {
		
		String s0 = "abcdefghijklmnopqrstuvwxyz";

		String s1 = s0.toUpperCase();

		String s2 = "0123456789";

		String s3 = "*+-/";

		String s4 = "!@#%%^&*";

		System.out.println(   "1 : 영문자 소문자 \n"
							+ "2 : 영문자 대문자 \n"
							+ "3 : 숫자 \n"
							+ "4 : 연산 기호 \n"
							+ "5 : 특수 문자 \n"
							+ "를 입력하시오 ");
		
		Scanner sc = new Scanner(System.in);
		int iVal = sc.nextInt();

		if (1 == iVal){
			new ConvertHex().toHex_Str(s0);
		}
		if (2 == iVal){
			new ConvertHex().toHex_Str(s1);
		}
		if (3 == iVal){
			new ConvertHex().toHex_Str(s2);
		}
		if (4 == iVal){
			new ConvertHex().toHex_Str(s3);
		}
		if (5 == iVal){
			new ConvertHex().toHex_Str(s4);
		}
	}
}
```

**출력결과**

```
javac -d . ConvertHex.java
java a.b.c.ch1.ConvertHex
```

![](https://images.velog.io/images/yunyoseob/post/d1616c9c-2338-4def-94e1-5b6c9176ce7a/image.png)
