안녕하세요. 😊 오늘은 HTML에서 FORM TAG에 대해 포스팅하겠습니다.

## FORM TAG

FORM TAG는 웹문서(html 태그로 만든 문서)에서 웹 서버로 데이터를 요청할 수 있는 유일한 태그 입니다.

![](https://images.velog.io/images/yunyoseob/post/af0f13d0-a934-46f9-9832-d0a40628b488/image.png)

- 사진 출처 : [HTTP 프로토콜](https://www.joinc.co.kr/w/Site/Network_Programing/AdvancedComm/HTTP) 

> **웹 문서에서 웹 서버로 데이터를 요청 할 수 있는 방법(request)**

|번호|방법|
|--|--|
|1| form 태그|
|2| XMLHttpRequest 객체|
|3| Ajax(XMLHttpRequest 객체를 가지고 구글 엔지니어가 만든 형식)|

## FORM TAG : GET방식

FORM TAG에서 GET 방식은 다음과 같은 특징이 있습니다.

> **FORM TAG의 GET방식은 사이즈 제한이 있다.**

FORM TAG의 GET방식은 256~4096byte 서버로 전송이 가능합니다. 이를 통해 GET방식은 사이즈의 제한이 있다는 것을 알 수 있습니다.

> **FORM TAG의 GET 방식은 요청 데이터를 header에 전송한다.**

**✔ HTML FORM TAG : GET 방식 예제**

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>VELOG 회원가입</title>
<style type="text/css">
	*{
		width:600px;
		margin:10px;
	}
</style>
</head>
<body>
	<h2>VELOG 회원가입</h2>
	<hr>
	<form method="GET" action="#">
		아이디 : <input type="text" name="id"><br>
		비밀번호 : <input type="text" name="pw"><br>
		<input type="submit" value="GET방식"><br>
	</form>
</body>
</html>
```

**✔ HTML FORM TAG : GET 방식 화면**

![](https://images.velog.io/images/yunyoseob/post/a9c3e4a8-8c0c-43d6-a415-e58c6dd5afbf/image.png)

```
link : http://localhost:포트번호/firstWeb/htmlp/formTest.html
```

다음 화면에서 아이디에 velog, 비밀번호에 1234를 입력한 뒤, 제출하기를 클릭하면 링크가 다음과 같이 바뀝니다.

```
link : http://localhost:포트번호/firstWeb/htmlp/formTest.html?id=velog&pw=1234#
```

바뀐 링크를 보면 ? 뒤에 id=velog&pw=1234 가 추가 된 것을 볼 수 있습니다. 이 부분을 Query String(쿼리 스트링)이라고 합니다. Query String은 key=value&key=value 로 이루어 져있습니다.

**✔ HTML FORM TAG : GET 방식 개발자 도구 Network에서 확인해보기**

![](https://images.velog.io/images/yunyoseob/post/9c669180-10b5-4828-963a-8d06ef761370/image.png)

입력한 다음 개발자 도구(윈도우 기준 F12)를 눌러서 Network의 Payload에서 확인을 해보면 Query String Parameters에 id에 velog, pw에 1234가 입력이 된 것을 확인할 수 있습니다.

## FORM TAG : POST방식

FORM TAG에서 POST 방식은 다음과 같은 특징이 있습니다.

> **FORM TAG의 POST 방식은 사이즈 제한이 있다.**

FORM TAG의 POST방식은 사이즈에 제한이 없습니다.

> **FORM TAG의 POST 방식은 요청 데이터를 BODY에 전송한다.**

**✔ HTML FORM TAG : POST 방식 예제**

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>VELOG 회원가입</title>
<style type="text/css">
	*{
		width:600px;
		margin:10px;
	}
</style>
</head>
<body>
	<h2>VELOG 회원가입</h2>
	<hr>
	<form method="POST" action="#">
		아이디 : <input type="text" name="id"><br>
		비밀번호 : <input type="text" name="pw"><br>
		<input type="submit" value="제출하기"><br>
	</form>
</body>
</html>
```

**✔ HTML FORM TAG : POST 방식 화면**

![](https://images.velog.io/images/yunyoseob/post/a9c3e4a8-8c0c-43d6-a415-e58c6dd5afbf/image.png)

```
link : http://localhost:포트번호/firstWeb/htmlp/formTest.html
```

다음 화면에서 아이디에 velog, 비밀번호에 1234를 입력한 뒤, 제출하기를 클릭하여도 링크에 쿼리 스트링이 추가되지 않습니다.

```
http://localhost:8088/firstWeb/htmlp/formTest.html#
```

**✔ HTML FORM TAG : GET 방식 개발자 도구 Network에서 확인해보기**

![](https://images.velog.io/images/yunyoseob/post/de57ced7-1855-4c52-ab80-6d263fd7e238/image.png)

입력한 다음 개발자 도구(윈도우 기준 F12)를 눌러서 Network의 Payload에서 확인을 해보면 Form Data에 id에 velog, pw에 1234가 입력이 된 것을 확인할 수 있습니다.

## Form 태그로 입력값을 jsp로 출력시키기

> **formTest.html**

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>VELOG 회원가입</title>
<style type="text/css">
	*{
		width:600px;
		margin:10px;
	}
</style>
</head>
<body>
	<h2>VELOG 회원가입</h2>
	<hr>
	<form method="POST" action="/firstWeb/jspp/formTest.jsp">
      <!-- jsp 파일 경로 action으로 설정해주기 -->
		아이디 : <input type="text" name="id"><br>
		비밀번호 : <input type="text" name="pw"><br>
		<input type="submit" value="제출하기"><br>
	</form>
</body>
</html>
```

> **formTest.jsp**

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ page import="java.util.Enumeration" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
	<title>VELOG 회원가입 데이터 입력</title>
</head>
<body>
<%
  String id=request.getParameter("id");
  String pw=request.getParameter("pw");
  out.println("입력된 아이디는 >>> : "+id+"<br>");
  out.println("입력된 비밀번호는 >>> : "+pw+"<br>");
%>
</body>
</html>
```  

다음처럼 아이디와 비밀번호를 입력받아 jsp로 받아올 수 있습니다. 

> **화면**

![](https://images.velog.io/images/yunyoseob/post/b8254fad-2cdc-43ea-9f0c-a3541dba38ac/image.png)

> **아이디와 비밀번호 입력 후**

![](https://images.velog.io/images/yunyoseob/post/eb2b177f-8c19-45ec-8d0e-382c7af48f2c/image.png)

이상으로 [HTML]FORM TAG 포스팅을 마치도록 하겠습니다. 😊
