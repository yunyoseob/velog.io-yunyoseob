# 🧰 JAVA로 개발할 때 필요한 도구 

> jdk : Java Development Kit
- Oracle JDK
- Open JDK

> Editor : EditPlus 5.5

> 명령어 실행 도구

> API



# 💻 JDK 설치 방법 

[오라클 홈페이지](https://www.oracle.com/kr/index.html)로 먼저 들어갑니다.

다음을 위한 리소스 -> 개발자 -> 선호하는 언어로 개발에서 JAVA 클릭 
-> Java 17 마침내 출시 아래 Java 다운로드 하기 클릭 -> [Java archive 클릭](https://www.oracle.com/java/technologies/downloads/archive/)

여기까지 따라오셨으면, 다음과 같은 화면이 보입니다.

![jdk설치](https://user-images.githubusercontent.com/81727895/151665575-a2aa2ad9-1191-4925-8341-54419c4f8870.JPG)


노란색 형광펜으로 되어 있는, Java SE 8(8u202 and earlier)를 클릭한 뒤, 본인의 OS환경에 맞게 클릭해주시면 됩니다.
Java SE 8(8u202 and earlier) 위 목록은 유료, 사용하고 싶으면 Open JDK를 사용하시면 됩니다.

![jdk설치2](https://user-images.githubusercontent.com/81727895/151665670-2877353d-8a0e-4aac-9878-c3af16de5b2e.JPG)

![jdk설치3](https://user-images.githubusercontent.com/81727895/151665674-c3453274-a7cb-489c-982a-92e5b484948b.JPG)


설치가 끝나셨으면, JAVA 파일 아래 jdk 파일과 jre 파일이 있습니다.

jdk 파일은 개발엔진이며, jre는 실행엔진 입니다.


# 🏵️ JDK 설치 후, 환경변수 세팅하기 

설치가 끝났으면 자바 환경변수를 세팅해야 합니다. 세팅하는 이유는 javac로 컴파일을 컴퓨터 어디서든 할 수 있게 하기 위함입니다.

**환경변수 세팅 방법**


내컴퓨터 -> 우클릭 -> 속성 -> 설정 -> 고급시스템 설정 -> 시스템 속성 팝업 화면 
-> 고급 탭 -> 환경변수 버튼 클릭 -> 환경 변수 팝업 -> 시스템 변수(S)

![환경변수](https://user-images.githubusercontent.com/81727895/151665811-373c184e-5cc3-46be-885a-cfe852a29f43.JPG)


1. **JAVA_HOME 세팅하기**

시스템 변수(S) -> 새로 만들기 버튼 클릭 
-> 새 시스템 변수 창 : 변수 이름(N) - JAVA_HOME 입력, 변수 값(V) - 주소 이름 입력하기(ex  : C:\Program Files\Java\jdk1.8.0_202)

2. **path에 세팅하기**

시스템 변수(S) 창에서 path 변수를 찾기 -> path 변수 값을 찾아서 클릭 -> 편집 버튼 클릭 
-> 환경 변수 편집 창 -> 새로 만들기 버튼 클릭 -> 맨 아래쪽 하단에 입력 창이 활성화 됨 
-> %JAVA_HOME%\bin 입력하기(한 글자도 틀리면 안 됩니다. bin을 binary의 약자로 실행파일 모음을 의미합니다.)
-> 위로 이동(U) 버튼을 클릭해서 맨 상단으로 보내기 -> 확인 버튼 클릭

**환경변수 세팅 잘 됐는지 확인 하는 방법**


Window + R 키를 누른 뒤, cmd 입력 -> 명령 프롬프트 나오면, javac 입력하기

![javac](https://user-images.githubusercontent.com/81727895/151666076-e640ff31-1971-4a01-8b81-1de9b6e35a25.JPG)


환경 변수 세팅 확인 끝!!


# 🗒️ Editplus 5.5 설치 방법 

Chrome -> [Google에 에디트플러스 검색](https://www.editplus.com/kr/) -> 에디트플러스 문서편집기 5.5 다운로드
-> EditPlus 5.5 다운로드

![editplus](https://user-images.githubusercontent.com/81727895/151666201-20aa4f3b-270b-4663-b4d2-5ec49fa6c426.JPG)



다음 시간에는 콘솔창을 이용해 "Hello java" 출력하는 것을 포스팅해서 올려보도록 하겠습니다. ✋
