# JAVA 기초 : Keywords 1편

저번 포스트에서 HelloJava.java를 실행했을 때,

```
public class HelloJava{

        public static void main(String args[]){

                System.out.println("Hello Java");
        }
}
```

명령어를 입력하여, 해당 코드에 대한 설명 없이 javac HelloJava.java로 컴파일하고, java HelloJava로 실행했습니다.

이번에는 해당 코드에 대해 설명하는 시간을 갖도록 하겠습니다. 😃

# Java 언어에 대한 이해

![java구성](https://user-images.githubusercontent.com/81727895/151695359-ef49b5fb-7c2d-4823-8438-7bb3ae75f46e.JPG)

위의 코드가 자바에서 실행되는 구조는 다음과 같습니다.

원래 import 명령어를 통해 java.lang.String과 java.lang.System을 import해야 하지만, java.lang의 경우, 원래 내장되어 있기 때문에
생략이 가능합니다.

코드를 보면 {}가 있는 것을 볼 수 있습니다. 한국말로는 중괄호, 영어로는 brace라고 하는 데요. 

class 뒤에 {} 블록하나가 있고, main() 함수 뒤에 {} 블록 하나가 있는 것을 확인 할 수 있습니다.

Java는 이렇게 블록을 사용하는 언어이므로, "블록언어이다" 혹은 "스코프언어이다" 혹은 "범위언어" 등등으로
불리기도 합니다.

++ **Java는 크게 [예약어](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/_keywords.html), (기호, 문자, 문자상수),
빌트인 리소스(클래스, 인터페이스, 상수, 함수...), 식별자로 구성되어 있습니다. 식별자를 제외하고는, 정해진 일정 규칙에 따라 코드를 작성해야 합니다.**

# public

먼저, public은 접근 제한자입니다. 접근 제한자는 클래스 및 클래스의 구성원에 접근을 허락하는 기능을 가지고 있습니다. 
(단, 접근 제한자는 클래스, 변수, 메서드 각각에 따로 적용을 해야 합니다.)

접근 제한자에서 public의 역할은 다른 패키지에 있는 클래스 및 클래스 자원 (변수, 메서드) 을 사용할 수 있게 하는 역할 입니다.

패키지 명령어에 대한 설명은 JAVA 기초: Keywords 2편에서 다뤄보도록 하겠습니다.

```
public class HelloJava{

        public static void main(String args[]){

                System.out.println("Hello Java");
        }
}
```

해당 코드에서 public은 class 앞에 그리고 main 함수 앞에 쓰인 것을 확인 할 수 있습니다.


# class

```
public class HelloJava{

        public static void main(String args[]){

                System.out.println("Hello Java");
        }
}
```

코드에서 class는 자바 프로그램의 최소 단위 입니다.

class의 종류는 일반 클래스, 추상클래스, 인터페이스 클래스, 파이널 클래스, 익명 클래서, 어뎁터 클래스,
인너 클래스, 중첩 클래스가 있지만 이번 포스팅에서는 다루지 않겠습니다.

class의 구성원은 변수와 함수가 있고, class가 메모리에 올라가면 객체 Object라고 부릅니다.

# main 함수

앞에서 class의 구성원에 변수와 함수가 있다고 했는데요. 위의 코드에서 함수는 

```
        public static void main(String args[]){

                System.out.println("Hello Java");
        }
```

입니다.

여기서, 가장 중요하게 봐야할 코드는 main()인데요. main()은 자바에서 콘솔 어플리케이션에서만 사용하는
특수한 자원입니다. (수정 금지!! 😠)

# static

static 키워드는 변수 또는 함수의 자료형 앞에 기술해서 사용하며 프로그램이 시작할 때 생성되고,
프로그램이 시작할 때 static 키워드가 붙어있는 자원을 자바 가상머신이 해당 자원을 메모리에 올려줍니다.

주의해야 할 점은 함수 앞에 static을 사용하였으면, 해당 함수 블록 내에서 또 static을 사용하면 안 됩니다.

> 올바른 예

![sta1](https://user-images.githubusercontent.com/81727895/151695864-2d06f386-4692-44dc-accb-e79f3d9412a1.JPG)

> 잘못된 예

![sta2](https://user-images.githubusercontent.com/81727895/151695922-0cbd85fc-242c-4087-ab7a-102593a65e08.JPG)

![sta3](https://user-images.githubusercontent.com/81727895/151695945-40950c7f-ff68-4132-b3d4-525188202c82.JPG)


- Error로 돌아가지 않음

# System.out.println("HelloJava");

```
public class HelloJava{

        public static void main(String args[]){

                System.out.println("Hello Java");
        }
}
```

- System은 java.lang.System 클래스를 선언하는 코드입니다. System 클래스는 자바에서 시스템에 관련된 기능을 모다운 클래스입니다.

- . 은 링크 연산자로 System 클래스와 out 필드를 연결하는 연산자입니다.
- out : System 클래스에 있는 변수로 스트림을 출력하는 통로 역할을 하는 변수입니다.
- println() : 콘솔에 출력을 하는 함수입니다. print는 출력하시오라는 의미이고, ln은 라인을 하나 띄우라는 의미입니다.



**오늘 포스팅은 여기서 마무리 하도록 하겠습니다~** ✋




