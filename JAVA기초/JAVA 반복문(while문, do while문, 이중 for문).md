안녕하세요 😊 오늘은 JAVA에서 반복문 중에 while문. do while문, 이중 for문에 대해 포스팅하도록 하겠습니다.

> **JAVA 반복문에는 for문, while문, do while문이 있다.**

## While문

while문은 for문과 다르게 소괄호 안에 내용이 아무것도 없으면 컴파일부터 에러가 납니다.

**코드 예시**
```
클래스와 메서드 생략

		for (; ; ){
			System.out.println("loop");
		}

```

**출력 결과 :  loop 무제한 출력**

```
클래스와 메서드 생략

		while (){
			System.out.println("loop");
		}

```

**컴파일 과정에서 에러 : illegal start of expression**

> **while 문 사용법**

[JAVA 반복문(for문) 포스팅](https://velog.io/@yunyoseob/JAVA-%EB%B0%98%EB%B3%B5%EB%AC%B8for%EB%AC%B8)에서 for문으로 1부터 10까지 합 출력 시킬 경우

```
package a.b.c.ch1;

public class Add_One_To_Ten_2{
	public static void main(String args[]){		
		int sum=1;	
		for (int i=0; i<9; i++){
			System.out.println(" 1부터 "+(i+2)+"까지의 합 >>> :"+(sum+i+2)+"\n");
			sum=sum+i+2;
			}
	} 
} 

```
다음과 같이 코드를 작성하였습니다. 이를 while문을 통해 출력시키면

```
package a.b.c.ch1;

public class Add_One_To_Ten_3{
	public static void main(String args[]){
		int i=2;
		int sum=1;

		while (i<=10){
			sum=sum+i;
			System.out.println("1부터 "+i+" 까지의 합 >>> : "+sum);
			i+=1;
		}
		System.out.println("1부터 10까지의 합 >>> : "+sum);
	}
}
```

다음과 같은 코드로 1부터 10까지의 합을 출력시킬 수 있습니다.

while문은 소괄호 안의 내용이 false일 때까지 반복하는 명령문 입니다. 

### break

 > **break는 while 반복문에서 loop를 멈출 때 쓸 수 있습니다.**

```
package a.b.c.ch1;

public class While_p_2{
	public static void main(String args[]){
		int i=2;
		int sum=1;

		while (i<=100){
			sum += i;
			boolean iBool= sum>55;
			if (iBool){
            	sum=sum-i;
				break;
			}
			else{
				System.out.println("1부터 "+i+" 까지의 합 >>> : "+sum);
			}
			i++;
		}
        System.out.print("1부터 10까지 의 합 >>> : "+sum);
		}
} 
```

예시로 위의 코드가 있을 때, 1부터 100까지의 합이 출력되어야 하는데, 중간에 합계가 55(1부터 10까지의 합)보다 클 경우에는 break로 while문의 loop를 중단시킬 수 있는 것입니다.

**출력 결과**

![](https://images.velog.io/images/yunyoseob/post/cf7c4a0e-f9e8-427d-a0a9-4dabba55a3cd/image.png)

**break와는 반대로 continue 명령어는 loop를 지속하라는 의미인데, Python이나 C와는 다르게 따져야 하는 사항이 많으므로, JAVA에서는 사용을 지양합니다.**

## do while문

 > **do while문은 다음과 같은 방식으로 수행됩니다.**

```
do : 실행하라 

언제까지? 

while 조건식이 될 때까지
```

따라서, do 명령어는 반드시 최소 한 번은 실행 되어야 합니다.

**코드 예시**

```
package a.b.c.ch1;

public class While_p_1{
	public static void main(String args[]) {
		
		int num = 1;
		int sum = 0;

		do{
			sum += num;
			num++;
		}
		while (num <= 10);
		System.out.println("1부터 10 까지의 합은 " + sum + " 입니다.");
	}
}
```

출력 결과 : 1부터 10 까지의 합은 55 입니다.

- do while문은 do 종결 그리고 while 종결의 방식이 아닙니다. do{}while(); 명령어를 통해 볼 수 있듯이, 종결자가 한 개입니다. do while문은 while의 조건식이 true에서 false가 될 때싸지 do안의 내용을 반복해서 수행하는 반복문입니다.

## 이중 for문

> **이중 for문은 for문 안에 for문이 하나가 더 있는 반복문입니다.**

이중 for문은 첫 번째 for문의 loop를 하는 과정에서 한 loop를 돌 때, for문 내에 있는 for문에서 loop를 한 번 더 돌리는 방식으로 수행됩니다.

```
package a.b.c.ch1;

public class For_for{
	public static void main(String args[]){
		for (int i=0; i<=10; i++){
			for (int j=1; j<=i; j++){
				System.out.print("*");
				} 
				System.out.println();
			} 
		
		for (int i=10; i>0; i--){
			for (int j=1; j<=i; j++){
				System.out.print("*");
				} 
				System.out.println();
			} 
	} 
} 
```

가령, 위의 코드를 실행한다면,

**첫 번째 이중 for문**

첫 번째 이중 for문은 i가 0부터 시작하여 10과 같거나 그 보다 작을 때까지, for문 안의 for문에서 j가 1부터 시작하여, i보다 작거나 같지 않을 때까지 j를 하나씩 추가하면서 별을 출력한 뒤, i를 하나 증가하여 반복시키는 방식으로 수행됩니다.

**두 번째 이중 for문**

두 번째 이중 for문은 i가 10부터 0보다 같거나 작지 않을 때까지, for문 안의 for문에서 j가 1부터 시작하여, i보다 작거나 같지 않을 때까지, j를 하나씩 추가하면서 별을 출력한 뒤, i를 하나 감소하여 반복시키는 방식으로 수행됩니다.

**출력 결과**

![](https://images.velog.io/images/yunyoseob/post/51904115-4597-4ba8-98bb-ee9a75402b27/image.png)

- 출력결과 별로 삼각형이 만들어진 것을 확인 할 수 있습니다.

### 반복문 실습 코드

마지막으로, 반복문을 사용하여 구구단을 만들어보는 실습을 마지막으로 이번 포스팅은 마치도록 하겠습니다. 🙂

> **이중 for문, while+for문, for+do while문을 사용하여 구구단 만들어보기**

✔ **이중 for문으로 구구단 만들기**

```
package a.b.c.ch1;

public class Gugu_1{
	public static void main(String args[]){
		for (int j=1; j<=9; j++){
			System.out.println();
			for (int i=1; i<=9; i++){
				System.out.format("%d x %d =%2d ", i, j, i*j);
			}
		}
	} 
} 
```

- **System.out.format("%d x %d =%2d ", i, j, i*j);** 은 첫 번째 정수형(%d)에 i를 대입하고, 두 번째 정수형에 j를 대입한 뒤, 마지막 두 자릿수 정수형(%2d)에 i*j를 출력하라는 의미입니다.

✔ **while + for문으로 구구단 만들기**

```
package a.b.c.ch1;

public class Gugu_2{
	public static void main(String args[]){
		int w1=1;
		int w2=1;
		while (w1<=9){
			for (w2=1;w2<=9;w2++){
				System.out.printf("%d x %d =%2d ", w1, w2, w1*w2);
				}
				System.out.println();
				w1++;
			} 
	}
}   
```

- **System.out.printf** 또한, %d, %d, %2d에 w1, w2, w1*w2를 대입하여 출력할 수 있는 명령어입니다.

✔ **for + do while 문으로 구구단 만들기**
```
package a.b.c.ch1;

public class Gugu_2{
	public static void main(String args[]){
		for (int i=1; i<=9; i++){
			int j=2;
			do{
				System.out.format("%d x %d =%2d", j, i, j*i);
				j++;
			}
			while(j<=9);
			System.out.println();
		} 
	}
}   
```

**이상으로 포스팅을 마치도록 하겠습니다. 😊**
