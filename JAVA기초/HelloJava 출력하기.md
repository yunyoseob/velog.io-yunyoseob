# HelloJava 출력하기 ✋

오늘은 cmd(명령 프롬프트)를 이용해여 HelloJava를 출력하는 포스팅을 해보겠습니다.

먼저, EditPlus를 키고, 새 파일을 열어, 다음 코드를 입력하여 줍니다.

```
public class HelloJava{

        public static void main(String args[]){

                System.out.println("Hello Java");
        }
}

```

public, class, static 등등 용어에 대한 설명은 다음 포스팅에서 진행하도록 하겠습니다.

코드를 다 입력하셨으면 파일이름을 HelloJava.java로 입력하여 주시고, 파일 형식을 All Files(*.*), 인코딩(E) : ANSI 로 
입력한 뒤, 저장하여 줍니다. (클래스 이름과 파일 이름은 항상 똑같아야 합니다!!)

> **저장하기 전**

![hellojava_before](https://user-images.githubusercontent.com/81727895/151670375-15576008-9ae9-467b-a5e9-abb30b8444af.JPG)

> **저장 후**

![hellojava](https://user-images.githubusercontent.com/81727895/151670341-8b6b82c8-afa7-4db6-923b-b11f17ae86d5.JPG)


저장이 끝나면, 윈도우+R을 누른 뒤, cmd를 입력하고 엔터를 칩니다. 

# 콘솔명령어 🔲

```
cd : 현재 디렉토리를 의미합니다.

cd.. : 이전 디렉토리로 이동 

cd \ or cd / : 가장 앞의 디렉토리로 이동

dir : 해당 위치에서 디렉토리 목록 보기

cd 경로 : 경로로 이동하기

cd a* : a로 시작하는 디렉토리로 이동하기

cls : clear

```

다음과 같은 콘솔 명령어로 java를 저장해놓은 디렉토리로 이동합니다.

명령어 dir을 입력했을 때, HelloJava.java가 있으면 잘 찾아간 겁니다. 😄

디렉토리를 잘 찾아갔으면, 이제 javac 명령어를 통해 컴파일을 진행합니다.


# javac  명령어

- javac 명령어 사용방법 : javac 한 칸 띄고 자바프로그램이름.java

```
javac 자바프로그램이름.java
```

여기서는 HelloJava.java로 저장했으니 다음과 같이 입력하여 줍니다.

```
javac HelloJava.java
```

컴파일이 완료되면, dir 명령어를 입력하면

![javac1](https://user-images.githubusercontent.com/81727895/151670780-de062392-10d8-4f3a-a468-b80abd0e18b8.JPG)

다음과 같이 HelloJava.class 파일이 생성된 것을 확인하실 수 있습니다.


# java  명령어

- java 명령어 사용방법 : java 한 칸 띄고 자바프로그램이름

```
java 자바프로그램이름
```

여기서는 HelloJava로 저장했으므로, 다음과 같이 명령어를 입력합니다.

```
java HelloJava
```

명령어를 입력하면, Hello Java가 콘솔창에 출력되는 것을 보실 수 있습니다. 😄

# type 명령어

```
type 자바프로그램이름.java
```

type 명령어를 통해 명령어를 입력하면, 코드 내용을 볼 수 있습니다.


```
type HelloJava.java
```

![type명령어](https://user-images.githubusercontent.com/81727895/151671344-476754c4-f75b-414e-9dfc-4fa7cc68ec74.JPG)

참고 : type 명령어는 향후에, java 파일이 package라는 자바에서 디렉토리 역할을 하는 키워드를 통해 java파일의 위치를 확인할 때, 유용합니다. 🙂



# javap 역 컴파일러 

프로그램 언어를 통해 명령어를 입력하면, 컴퓨터가 알아들을 수 있게 컴파일을 해주어야 합니다.
javac.exe 명령어를 통해 자바 언어를 자바 가상머신(JVM)이 알아볼 수 있게 byte code로 바꾸고 java명령어로 실행하는 것이 지금까지 과정이였습니다.

그러나, type 명령어로 

```
type HelloJava.class
```

를 입력하면 

![hellojavaty](https://user-images.githubusercontent.com/81727895/151671110-4ddd3c89-9bc2-4a93-9994-6ca26a25e318.JPG)

컴퓨터가 알아듣는 바이트 코드이다 보니 사람은 읽을 수가 없습니다.

javap 명령어는 이 때, 사람이 알아볼 수 있게 역으로 컴파일러를 해주는 명령어 입니다.

즉, 자바클래스 바이트코드를 소스코드로 변환하여 줍니다.

```
javap HelloJava.class
```

![javap](https://user-images.githubusercontent.com/81727895/151671177-1e885958-1c73-4b32-b7a9-0d18588a9f5f.JPG)

javap 명령어로 역컴파일하여 보기 😄

이번 포스팅은 여기서 마치도록 하겠습니다~ ✋

