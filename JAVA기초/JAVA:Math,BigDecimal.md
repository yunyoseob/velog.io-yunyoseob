안녕하세요. 😊 오늘은 Math와 BigDecimal에 대해 알아보도록 하겠습니다.

## Math

Math는 수식적인 부분을 작성할 때 사용하는 클래스입니다. [Java™ Platform
Standard Ed. 8](https://docs.oracle.com/javase/8/docs/api/)에서 Math클래스를 클릭하면, 다음과 같은 화면이 나옵니다.

![](https://images.velog.io/images/yunyoseob/post/f8658629-325e-43da-8eb3-6f19a7a93dc4/image.png)

Math클래스의 method로는 다음과 같은 메서드가 있습니다.

|method이름|설명|
|---|---|
|round|반올림 : 전달받은 실수를 소수점 첫 번째 자리에서 반올림한 결과를 반환합니다.|
|ceil|올림 : 전달 받은 실수보다 작은 정수 중 가장 작은 정수를 반환합니다.|
|floor|내림 : 전달 받은 실수보다 작은 정수 중 가장 큰 정수를 반환합니다.|
|pow|제곱연산 : 첫 번째 인수 값의 수를 두 번째 인수값으로 제곱합니다.|
|abs|절대값 반환 : 음수의 값을 양수로 반환합니다.|
|max|두 수 중에서 큰 값을 반환합니다.|
|min|두 수 중에서 작은 값을 반환합니다.|

이 외에도 Math 클래스에는 다양한 메서드가 존재합니다.

- 모든 메서드들의 Modifier and Type에 static이 붙어있으므로, Math.메서드이름으로 사용하면 됩니다.

> **Math.random()**

|Modifier and Type|Method|Description|
|static double|random()|Returns a double value with a positive sign, greater than or equal to 0.0 and less than 1.0.|

0에서 1사이의 임의의 값을 출력해줍니다. 이 수를 난수라고 합니다.

### **Math.random() 활용 예제**

이러한 난수를 활용하여, 숫자맞추기 게임이나 복권 번호 생성, 랜덤아이디&랜덤패스워드&랜덤인증번호 생성 등을 할 수 있습니다. 

> **숫자맞추기 게임의 경우, Math.random()으로 0부터 1사이의 난수를 생성 후, 100을 곱한다음 실수를 정수로 변환하고 1을 더하여 임의의 숫자를 지정후, 게임을 시작합니다.**

```java
package a.b.c.prac1;

import java.util.Scanner;

public class Math_p3{

	public static void main(String[] args) {
		int answer = (int)(Math.random() * 100) + 1;
		System.out.println("answer >>> : " + answer);
		
		Scanner sc=new Scanner(System.in);
		
		int input = 0;
		boolean iBool;
		
		try {
			do {
				System.out.println("1 과 100 사이의 정수값을 입력하시오 >>> : ");
				input = sc.nextInt();
				if (input<=100 && input>=1){
					iBool=answer==input;
					System.out.println("정답이면 true, 아니면 false"+iBool);
					if (answer==input){
						System.out.println("정답입니다!! 축하드립니다!!");
						break;
					}else if(answer>input){
						System.out.println("땡!! 다시 입력하세요!!");
						System.out.println("HINT : 더 높은 숫자를 입력하세요.");
						sc.nextLine();
					}else if(answer<input){
						System.out.println("땡!! 다시 입력하세요");
						System.out.println("HINT : 더 낮은 숫자를 입력하세요.");
					}
				}
				else{
					System.out.println("잘못 입력한 값 >>> "+input);
					System.out.println("범위를 다시 확인하시고, 다시 입력해주세요.");
					sc.nextLine();
				}				
			}
		while (true);

		}catch(Exception e){
			System.out.println("정수를 입력하지 않아 게임을 종료합니다.");
		}finally{
			System.out.println("숫자 맞추기 게임을 종료합니다.");
			sc.close();
		}
	}
}
```

**✔ 출력 결과**

👀 case1

```java
answer >>> : 89
1 과 100 사이의 정수값을 입력하시오 >>> : 
88
정답이면 true, 아니면 falsefalse
땡!! 다시 입력하세요!!
HINT : 더 높은 숫자를 입력하세요.
1 과 100 사이의 정수값을 입력하시오 >>> : 
90
정답이면 true, 아니면 falsefalse
땡!! 다시 입력하세요
HINT : 더 낮은 숫자를 입력하세요.
1 과 100 사이의 정수값을 입력하시오 >>> : 
89
정답이면 true, 아니면 falsetrue
정답입니다!! 축하드립니다!!
숫자 맞추기 게임을 종료합니다.
```
👀 case2

```java
answer >>> : 34
1 과 100 사이의 정수값을 입력하시오 >>> : 
1000
잘못 입력한 값 >>> 1000
범위를 다시 확인하시고, 다시 입력해주세요.
1 과 100 사이의 정수값을 입력하시오 >>> : 
종료
정수를 입력하지 않아 게임을 종료합니다.
숫자 맞추기 게임을 종료합니다.
```



> **복권 번호 생성의 경우, Math.random()으로 0부터 1사이의 난수를 생성 후, 45를 곱한다음 실수를 정수로 변환하고 1을 더하여 1부터 45사이의 수를 랜덤으로 생성합니다. 이후, 배열로 입력하고, 배열의 값이 중복되는 경우, for문에서 index를 하나 감소시켜 중복값을 하나로 통일시킵니다.**

```java
package a.b.c.ch5;

public class Lotto{	
	public static void main(String[] args) {
		String n0 = "";
		String n1 = "";
		char c = 'A';
		String n2[]= {" 자 동 ", " 수 동  "};		

		for (int n=0; n < 5; n++) {
			
			int lo[] = new int[6];		
			
			for (int i=0; i < lo.length; i++){
				
				lo[i] = (int)(Math.random()*45) + 1;
				for (int j=0; j < i; j++ ){				
					if (lo[j] == lo[i]){
						i--;
						break;
					}
				}
			}
							
			for (int i=0; i < lo.length; i++ ){								
				if (lo[0] == lo[i]) {								
					n1 = String.valueOf(lo[i]);								
					if (1 == n1.length()) {
						n1 = "0" + n1;
					}										
					n0 = c + n2[1] + n1;
					c += 1;
				}else {						
					n0 = String.valueOf(lo[i]);					
					if (1 == n0.length()) {
						n0 = "0" + n0;
					}	
				}
				
				n0 += " ";	
				
				System.out.print(n0);				
			}	
			
			System.out.println();
		}  							
	}
}
```
**✔ 출력 결과**

```java
A 수 동  11 10 32 02 09 08 
B 수 동  26 39 43 03 06 11 
C 수 동  26 41 17 24 29 20 
D 수 동  17 30 35 10 34 25 
E 수 동  30 05 32 02 20 44
```

> **랜덤 아이디 & 랜덤 비밀번호 & 랜덤 인증번호 만들기**

```java
package a.b.c.ch5;

import java.util.UUID;

public class Random_NUM {
	public static String tempPW(int len) {
		String u = UUID.randomUUID().toString();
		System.out.println("u >>> : " + u);
		u = u.replace("-","").substring(0, len);
		System.out.println("u >>> : " + u);
		return u;
	}
	
	public static String randomPW(int len) {
		char c[] = {
						'1','2','3','4','5','6','7','8','9','0', 
			        	'A','B','C','D','E','F','G','H','I','J',
			        	'K','L','M','N','O','P','Q','R','S','T',
			        	'U','V','W','X','Y','Z', 
			        	'a','b','c','d','e','f','g','h','i','j',
			        	'k','l','m','n','o','p','q','r','s','t',
			        	'u','v','w','x','y','z',
			        	'!','@','#','&'
			        	//'!','@','#','$','%','^','&','*','(',')'
		        	}; 
		String p = "";
		for (int i=0; i < len; i++) {
			int a = (int)(Math.random()*(c.length));
			p += c[a];
		}
		return p;
	}	
	
	public static String certificNum(int len) {
		
		char c[] = {'1','2','3','4','5','6','7','8','9'}; 

		String p = "";
		
		for (int i=0; i < len; i++) {
			int a = (int)(Math.random()*(c.length));
			p += c[a];
		}
		
		return p;
	}	

	public static void main(String[] args) {
		String s1 = Random_NUM.tempPW(8);
		String s2 = Random_NUM.randomPW(8);
		String s3 = Random_NUM.certificNum(6);
		
		System.out.println("UUID >>> : " + s1);
		System.out.println("randomPW >>> : " + s2);
		System.out.println("certificNum >>> : " + s3);
	}
}
```
**✔ 출력 결과**

```java
u >>> : d79d52f7-df14-4893-920d-e788666e73b4
u >>> : d79d52f7
UUID >>> : d79d52f7
randomPW >>> : QFzeh8jo
certificNum >>> : 952974
```

## BigDecimal

java.lang 패키지에 Math 클래스도 있지만, java.math 패키지로 가면 BigDecimal 클래스가 있습니다.

![](https://images.velog.io/images/yunyoseob/post/87a23663-3682-44fb-a936-dfe92725e65b/image.png)

java.lang 패키지에 Math 클래스를 두고, java.math.BigDecimal 클래스를 사용하는 이유는 double, float의 실수를 인수로 받았을 때, 결과가 정확하지 않을 때가 있어서 입니다.

**✔ 자바 컴파일러는 정수형 밖에 모른답니다. 😊**

```java
package a.b.c.prac1;


import java.math.BigDecimal;

public class Math_9 {

	public static void main(String[] args) {
    	int x2=1;
		double y2=0.1;
		int num=7;
		double z2=x2-(num*y2); 
		System.out.println("z2 >>> "+z2);
```        

**✔ 출력 결과**

```java
z2 >>> 0.29999999999999993
```
이를 구글에서 숫자를 입력하여 계산하면 다음과 같은 결과가 나옵니다.

![](https://images.velog.io/images/yunyoseob/post/6b1b950c-5eb2-459a-b6ef-c00dfa466bec/image.png)

Math 메서드에서 인수값을 double형으로 받는 경우가 꽤 있는데, 이럴 경우, 해결책이 java.math 패키지에 있는 BigDemical 클래스를 활용하는 것입니다.

```java
BigDecimal b1= BigDecimal.valueOf(1);
BigDecimal b2=BigDecimal.valueOf(0.7);
System.out.println("b1.subtract(b2) >>> : "+b1.subtract(b2));
```

**✔ 출력 결과**

```java
b1.subtract(b2) >>> : 0.3
```

### BigDecimal 실습 코드

```java
package a.b.c.prac1;

import java.math.BigDecimal;

public class Math_10 {

	public static void main(String[] args) {
		String x="37.56632697499861";
		String y="126.97792762801669";

		BigDecimal b1=new BigDecimal(x);
		System.out.println("b1 >>> : "+b1);
		BigDecimal b2=new BigDecimal(y);
		System.out.println("b2 >>> : "+b2);
		
		double dx=37.56632697499861;
		double dy=126.97792762801669;
		
		BigDecimal b11=new BigDecimal(dx);
		BigDecimal b22=new BigDecimal(dy);
		
		System.out.println("dx >>> : "+dx);
		System.out.println("dy >>> : "+dy);
		
		BigDecimal badd=b1.add(b2);
		System.out.println("badd >>> : "+badd);
		BigDecimal badd_D=b11.add(b22);
		System.out.println("badd_D >>> : "+badd_D);

		BigDecimal bsub=b1.subtract(b2);
		System.out.println("bsub >>> : "+bsub);
        BigDecimal bsub_D=b11.subtract(b22);
		System.out.println("bsub_D >>> : "+bsub_D);
	}

}
```

> **출력 결과**
```
b1 >>> : 37.56632697499861
b2 >>> : 126.97792762801669
dx >>> : 37.56632697499861
dy >>> : 126.97792762801669
badd >>> : 164.54425460301530
badd_D >>> : 164.54425460301529682283216970972716808319091796875
bsub >>> : -89.41160065301808
bsub_D >>> : -89.41160065301807691184876603074371814727783203125
```

### 코드 해설을 통해 알아보는 BigDecimal

> **x, y와 dx, dy**

- x, y는 문자숫자입니다. 문자숫자란 "" 혹은 ''를 제거하였을 때, 
해당 내용이 숫자를 의미합니다. 이 둘은 현재, String 자료형으로 저장되어있습니다.

- 한편, dx, dy는 double 자료형 숫자입니다. 이 둘은 현재, double 자료형으로 저장되어있습니다.

> **BigDecimal b1=new BigDecimal(x);**
**BigDecimal b2=new BigDecimal(y);**

해당 명령어로 문자숫자를 인스턴스해서 b1이라는 참조변수로 선언해줍니다.

이렇게 b1,b2를 한 다음 이 둘을 출력하고, double 자료형의 변수와 비교하면 다음과 같습니다.

```java
b1 >>> : 37.56632697499861
b2 >>> : 126.97792762801669
dx >>> : 37.56632697499861
dy >>> : 126.97792762801669
```

**🤔 여기서, double 자료형인 dx와 dy를 x대신 넣으면 안 되나요??**

> **BigDecimal b11=new BigDecimal(dx);**
**BigDecimal b22=new BigDecimal(dx);**

new BigDecimal()의 소괄호에 double 자료형과 문자숫자를 넣고 
덧셈과 뺄셈으로 비교한 결과는 다음과 같습니다.

> **BigDecimal badd=b1.add(b2);**
**BigDecimal badd_D=b11.add(b22);**
**System.out.println("bsub >>> : "+bsub);**
**System.out.println("bsub_D >>> : "+bsub_D);**

```java
badd >>> : 164.54425460301530
badd_D >>> : 164.54425460301529682283216970972716808319091796875
bsub >>> : -89.41160065301808
bsub_D >>> : -89.41160065301807691184876603074371814727783203125
```

위의 코드를 보면 double을 인수로 받아서 BigDecimal 클래스의 참조변수로 계산했을 때의 결과와 문자상수를 인수로 받아서 BigDecimal 클래스의 참조변수로 계산했을 때, 그 값이 다른 것을 볼 수 있습니다.

**이상으로 JAVA : Math, BigDecimal 포스팅을 마치도록 하겠습니다. 😀**
