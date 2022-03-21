안녕하세요. 오늘은 Apache Tomcat 서버와 eclipse를 연결하여 웹에서 Hello를 출력하는 것을 포스팅하도록 하겠습니다. 😀

## Apache Tomcat 설치


먼저, [Apache 홈페이지](https://apache.org/)로 들어간 다음 APACHE PROJECT LIST에서 Tomcat을 클릭합니다.

![](https://images.velog.io/images/yunyoseob/post/72aef560-76f4-4d5a-85c3-41fbc7a3661e/image.png)

필자는 [Apache tomcat 8.5](https://tomcat.apache.org/download-80.cgi)를 다운받도록 하겠습니다.

```
8.5.77

Binary Distributions

- Core:
 > 32-bit/64-bit Windows Service Installer(pgp, sha512)
```

Windows Service Installer를 눌러 설치를 진행합니다.


- 설치를 진행한 이후, Server Shutdown Port를 설정하고, HTTP/1.1 Connector Port를 설정한 뒤, Tomcat Administrator Login에서 User Name과 Password를 설정합니다.


> **Tomcat 시작방법**

설치한 경로로 가서, Apache Software Foundation 폴더를 클릭하고, Tomcat 8.5 폴더를 클릭한 다음, bin 폴더에 들어가서, Tomcat8W.exe를 누른뒤, start로 시작합니다.

![](https://images.velog.io/images/yunyoseob/post/c6d4f050-cb19-4ad2-bbbc-4ed85209f91a/image.png)

start를 누르고 시작한 뒤, 인터넷에서 **localhost:포트번호**를 입력하면 Manaer 화면이 나옵니다.

![](https://images.velog.io/images/yunyoseob/post/32def5fc-4182-4728-a2d7-252fba028a4c/image.png)

해당 화면에서 우측 상단의 Server Status를 클릭하면

![](https://images.velog.io/images/yunyoseob/post/7e56318f-64ed-486f-bece-2172a520b5ea/image.png)

서버 상태를 보실 수 있습니다.

**✔ 주의 사항 : Service Status가 Stopped으로 되어 있거나, 방화벽 등의 문제가 있으면 사이트에 연결할 수 없습니다.**

![](https://images.velog.io/images/yunyoseob/post/7e35c8f8-be32-4dd8-b4b3-915dcf76e77d/image.png)

## eclipse encoding setting

Tomcat과 eclipse를 연결하기 앞서, 이클립스 인코딩을 eclipse에서 Window - Preferences에서 UTF-8으로 세팅하도록 하겠습니다.

> **General Setting**

먼저, eclipse에서 Window - Preferences - General - Content Types - Java Class File의 하단 화면에 Default encoding에 UTF-8을 입력후 Update를 합니다.

![](https://images.velog.io/images/yunyoseob/post/e924e8b5-c927-4c11-8499-79a745d47c11/image.png)

그 다음, General - Workspace - Text file encoding - Other에서 UTF-8을 선택한 뒤, Apply 해줍니다.

![](https://images.velog.io/images/yunyoseob/post/2666734d-2188-4776-8fa4-12335b8cac2d/image.png)

마지막으로, General - Editors - Text Editors - Spelling - Encoding에서 Default(UTF-8)을 체크 한 뒤, Apply 해줍니다.

![](https://images.velog.io/images/yunyoseob/post/e1ff766c-a8a5-4b92-a83d-1d9cca7950cd/image.png)


> **Web Setting**

먼저, Web - CSS Files - Encoding에서 ISO 10646/Unicode(UTF-8)을 클릭하고, Apply 해줍니다.

![](https://images.velog.io/images/yunyoseob/post/cf02cf5f-39c5-4320-a931-d4bd8508cef5/image.png)

그 다음, Web - HTML FIles - Encoding에서 10646/Unicode(UTF-8)을 클릭하고, Apply 해줍니다.

![](https://images.velog.io/images/yunyoseob/post/ec9795cf-ac5f-4ed9-b016-6ea6a6c2fce5/image.png)

마지막으로, Web - JSP Files - Encoding에서 10646/Unicode(UTF-8)을 클릭하고, Apply 해줍니다.

![](https://images.velog.io/images/yunyoseob/post/25133604-caba-4788-aa6e-0a5732f7585c/image.png)

> **XML Setting**

XML - XML Files - Encoding에서 10646/Unicode(UTF-8)을 클릭하고, Apply 해주고 Apply and Close 버튼을 눌러주면서, 기본적인 세팅을 해줍니다.

![](https://images.velog.io/images/yunyoseob/post/3dee88d7-083a-4309-bcec-733b699c4b32/image.png)


## tomcat 이클립스에 플러그 인 하기

이클립스에서 Window - Preferences 에서 Server를 클릭후, Runtime Environments 창에서 우측에 있는 Add.. 버튼을 클릭합니다.

![](https://images.velog.io/images/yunyoseob/post/1c6e2b97-83c6-4ab4-ae0a-eb570d603495/image.png)

New Server Runtime Environment에서 Apache Tomcat v8.5를 선택하고 Next를 누른 뒤, Tomcat installation direcory : Browse 버튼 클릭하여 Tomcat 8.5가 있는 경로를 선택하고 Finish 버튼을 누른 뒤, Apply and Close를 누릅니다.

![](https://images.velog.io/images/yunyoseob/post/0b82d1ec-a772-4076-93ca-633c01b0081e/image.png)

마지막으로, 이클립스 하단에 Servers 탭 (Window - Show View - Servers 선택)

No servers are available. Click this link to create a new server... 링크 클릭 후, 

Define a New Server 창에서 Select the server type: Tomcat v8.5 Server 선택하고 Finish 클릭 합니다.

## Dynamic Web Project 생성

이클립스 좌측 상단에서 File - New - Other - Select a wizard 에서 Dynamic을 검색 후, Dynamic Web Project를 선택합니다.

![](https://images.velog.io/images/yunyoseob/post/cced5d07-f848-40e7-8f84-c5b997657ee7/image.png)

Next를 클릭하고, 프로젝트 이름을 적은 뒤, Next를 누르고, Web Module 창에서 Generate web.xml deployment descripter 체크박스 체크 후, Finish를 눌러줍니다.

## 새 프로젝트에 tomcat 플러그인 하기

새로운 프로젝트에 우클릭을 누른 뒤, Build Path - Configure Build Path를 클릭합니다.

Libraries 탭을 클릭하고, 우측에 Add External JARs... 버튼을 클릭합니다.

Tomcat 8.5\lib 폴더에서 라이브러리 전체를 선택하고 Java Build Path 창에서 Apply를 누른 뒤, Apply and Close를 클릭합니다.

![](https://images.velog.io/images/yunyoseob/post/2ba9552a-2a4f-40ca-a29f-4937084fd829/image.png)

여기까지 성공적으로 잘 마무리 했으면 Libraries에 Referenced Libraries에 해당 라이브러리가 들어온 것을 확인 할 수 있습니다.

![](https://images.velog.io/images/yunyoseob/post/edb14f92-fbda-4e7d-8d65-c45afeaf6336/image.png)

마지막으로 Window - Web Browser에서 3.Chrome을 선택하면, Chrome에서 출력시킬 준비는 끝이 납니다.

## 웹에서 Hello 출력하기

이제, 생성한 프로젝트에서 WebContent에서 html, jsp 폴더를 만들고, html 폴더에는 마우스 우클릭 - new - HTML File로 HTML 파일을 생성합니다.

![](https://images.velog.io/images/yunyoseob/post/962a32e4-ab37-4a21-900d-473f80dfe10e/image.png)

그리고 jsp 폴더에서는 마우스 우클릭 - new - JSP File로 JSP 파일을 생성합니다.

![](https://images.velog.io/images/yunyoseob/post/c47ef980-b314-4f0e-98e7-55d47801adcd/image.png)


> **hello.html**


```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	Hello HTML !!!
</body>
</html>
```

이제 해당 파일을 실행시키면, chrome 창에 다음과 같은 결과가 나옵니다. (Tomcat v8.5 Server at localhost가 Start라는 가정하에 실행됩니다.)

> **출력 결과**

![](https://images.velog.io/images/yunyoseob/post/e833d09c-5683-4568-8aa0-4f45036fb159/image.png)

크롬창에 성공적으로 출력하였습니다.

> **hello.jsp**


```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	Hello Jsp !!!<br>
	<hr>
<%
	out.println("Hello JSP !!!!");
	out.println("<hr>");
	java.util.Date d = new java.util.Date();
	out.println("Date >>> : " + d + "<br>");
%>	
</body>
</html>
```

> **출력 결과**

![](https://images.velog.io/images/yunyoseob/post/ed1773a6-d655-4ea6-b7d1-61304884d87f/image.png)


jsp도 성공적으로 크롬창에 나타났습니다.

**이상으로, 웹에서 Hello 출력하기 포스팅을 마치도록 하겠습니다.😀**
