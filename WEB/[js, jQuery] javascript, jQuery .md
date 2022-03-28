안녕하세요. 😀 오늘은 javascript 기초와 jQuery 기초에 대해 포스팅하도록 하겠습니다.


## javascript

javascript는 웹 브라우저에서 자바스크립트 소스를 읽고 처리하는 해석기로 구동합니다.

javascript는 웹 문서에서 &lt;script&gt; 태그를 이용하여 작성합니다.

> **javascript : 객체**

자바스크립트에서 객체는 프로그램에서 인식할 수 있는 모든 대상을 가리킵니다. 자바스크립트는 웹 사이트나 웹 애플리케이션에서 개발하는 언어이므로, 웹과 관련된 대상을 모두 객체로 인식합니다.

- 문서 객체 모델 : Document Object Model, 웹 문서 자체(document), 이미지 img 등...
- 브라우저 관련 객체: Browser Model Object : BOM, 웹 브라우저에서 사용하는 정보 screen, navigator 등등....
- 내장 객체 : 웹 프로그래밍에서 자주 사용하는 요소들(Object, String ....)
- 기타 객체 : JSON 등

### javascript :  Browser Model Object(브라우저 객체 모델)

![](https://images.velog.io/images/yunyoseob/post/36cfcd2f-2fbd-4372-a4b5-962f7cae157e/image.png)

- 출처: [레드아이님의 블로그 : JavaScript 브라우저 객체 모델](https://redthing.tistory.com/entry/Javascript-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EA%B0%9D%EC%B2%B4-%EB%AA%A8%EB%8D%B8) 

**✔ 자바스크립트의 브라우저 객체 모델의 최상위 요소는 window입니다. 브라우저 창이 열릴 때 마다 하나씩 만들어집니다.**

|window 객체 구성 요소|설명|
|---|---|
|navigator|현재 사용하는 브라우저의 정보|
|history|현재 창에서 사용자의 방문 기록을 저장|
|location|현재 페이지의 URL 정보|
|screen|현재 사용하는 화면 정보|
|document|웹 문서마다 하나씩 있으며, body 태그를 만나면 만들어진다.


> **window 객체 명령어 모음**

```javascript
open("URL", "새창이름","새창옵션")
alter(data)
prompt("질문", "답변")
confirm("질문내용")
moveTo(x,y)
resizeTo(sidth, height)
setInterVal(function(){자바스크립트 코드}, 일정시간 간격)
setTimeout(function(){자바스크립트 코드}, 일정시간 간격)
```

> **navigator 객체 명령어**

```javascript
navigator.userAgent // 브라우저와 운영체제 정보
```

> **history 객체 명령어**

```javascript
history.length // 방문 기록에 저장된 목록의 개수
history.back(n) // 이전 방문 사이트로 이동
hitory.go(n) // n번째로 이동. +,-
```

> **location 객체 명령어**

```javascript
location.href // URL을 반환한다
location.hash // URL 해시값(#에 명시된 값)
location.hostname // 호스트 이름
location.protocol // 프로토콜
location.search // 쿼리 스트링
location.reload() // 브라우저 F5 새로고침 기능
```

> **screen 객체 명령어**

```javascript
screen.width // 화면 너비
screen.height // 화면 높이
screen.availWidth // 작업 표시줄 제외한 화면 너비
screen.availHeight // 작업 표시줄 제외한 화면 높이
screen.colorDepth //  사용자 모니터 컬러 bit
```

### javascript :  Document Object Model(문서 객체 모델)

> **Document Object Model**

Document Object Model(DOM)은 자바스크립트를 이용해서 웹 문서에 접근하고 제어할 수 있도록
객체를 사용해 웹 문서를 체계적으로 정리하는 방법입니다.

DOM은 웹 문서를 하나의 객체로 정의합니다. 웹 문서 전체는  document 객체이고, 텍스트, 이미지, 표 등 모든 요소도 각각 객체 입니다.

> **DOM 요소에 접근하기**

HTML 요소(HTMLCollection)를 가져오는 함수들 

**✔ id 선택자 : document.getElementById("id명")**
**✔ class 선택자 : document.getElementById("클래스명")**
**✔ 태그 이름 선택자 : document.getElementById("태그명")**

### javascript의 변수와 함수

javascript의 자료형에는  var, let, const이 있습니다. let은 함수 블럭에서만 사용 가능한 변수이며, const는 상수 역할을 하는 변수입니다.

> **java vs javascript**

```java
String s="a";
char c='a';
int i=2000;
```

java에서는 문자열 변수는 String으로, 문자 변수는 char로 정수 변수는 int 혹은 long으로 표기하여 사용하였으나, javascript에서는 var로 통일하여 사용할 수 있습니다.

```javascript
var i=2000;
var s="a";
var c='a';
```

> **javascript : 변수 예제**

```javascript
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>Java Script 연습</title>
	<script type="text/javascript">
		window.alert("자바스크립트 연습 시작");
	</script>
	<style type="text/css">
		*{
			margin:30;
			width:500;
		}
	</style>
</head>
<body>
	<script type="text/javascript">
		window.document.write("자바스크립트 변수 연습 시작");
	 	
		// 자바스크립트에서 변수는 var로 통일한다.
		// 자바와는 다르게 변수를 따로 선언해주지 않아도, 알아서 변수 타입을 지정해준다.
		var i=2000;
		console.log("i >>> : "+i);
		console.log("typeof(i) >>> : "+typeof(i));
		var s="a";
		console.log("s >>> : "+s);
		console.log("typeof(s) >>> : "+typeof(s));
		var c='a';
		console.log("c >>> : "+c);
		console.log("typeof(c) >>> : "+typeof(c));
	</script>
</body>
</html>
```

> **개발자도구 Console 출력 결과**

```javascript
i >>> : 
typeof(i) >>> : number

s >>> : a
typeof(s) >>> : string

c >>> : a
typeof(c) >>> : string
```

특이사항은 자바에서는 싱글 쿼테이션('')은 char, 더블 쿼테이션("")은 String 이였으나
자바스크립트에서는 둘 다 String으로 나온다는 것입니다.

> **javascript : 다양한 함수 사용법**

javascript는 다양한 함수를 지원합니다.

|javascript 함수 예시|설명|
|---|---|
|function 함수명() {명령문;}|함수를 선언할 때는 function 예약어와 중괄호 {}을 사용한다.|
|function(){}|함수 이름이 없는 함수(익명함수 입니다.)|
|var 변수=function(){}|함수를 리터럴로 정의할 수 있습니다.|
|(function(){명령}());|즉시 실행 함수 입니다.|
|(매개변수)=>{함수내용}|화살표 함수|

> **javascript : 다양한 함수 사용 예제**

```javascript
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>Java Script 연습</title>
	<script type="text/javascript">
		window.alert("자바스크립트 연습 시작");
	</script>
	<style type="text/css">
		*{
			margin:30;
			width:500;
		}
	</style>
</head>
<body>
	<script type="text/javascript">
		window.document.write("자바스크립트 함수 연습 시작");
		function add(a, b){
			return a+b;
		}
		function minus(a,b){
			return a-b;
		}
		function multiply(a, b){
			return a*b;
		}
		function devide(a,b){
			return a/b;
		}
		
		document.write("두 수의 합 (10, 5) >>> : "+add(10, 5)+"<br>");
		document.write("두 수의 차 (10, 5) >>> : "+minus(10, 5)+"<br>");
		document.write("두 수의 곱 (10, 5) >>> : "+multiply(10, 5)+"<br>");
		document.write("두 수의 나눗셈 (10, 5) >>> : "+devide(10,5)+"<br>");
	</script>
	<br>
	<hr>
	<br>
	<script type="text/javascript">
		window.document.write("자바스크립트의 다양한 함수들");
		document.write("익명 함수는 함수의 이름이 없다."+"<br>");
		// 익명 함수
		var vadd=function(a,b){
			return a+b;
		}
		document.write("익명 함수 더하기 (10, 5) >>> : "+vadd(10, 5)+"<br>");
		document.write("즉시 실행 함수는 함수의 결과로 변수로 할당하지 않고 바로 실행한다."+"<br>");
		// 즉시 실행 함수
		(function(){console.log("즉시 실행 함수")})
		
		document.write("화살표 함수는 호출 하면 바로 return 값이 호출 된다."+"<br>");
		var hi = () => {return "저는 화살표 함수 입니다.";}
		document.write("화살표 함수 호출  >>> hi() >>> : "+hi());
		
		document.write("let은 함수 블럭에서만 사용이 가능하다. "+"<br>");
		let say=()=>alert("hi!!");
		say();
		
		// 함수 줄여서 쓰기
		var add=(a,b)=>a+b;
		var minus=(a,b)=>a-b;
		var multiply=(a,b)=>a*b;
		var devide=(a,b)=>a/b;
		
		console.log("add(10,5) >>> : "+add(10,5));
		console.log("minus(10,5) >>> : "+minus(10,5));
		console.log("multiply(10,5) >>> : "+multiply(10,5));
		console.log("devide(10,5) >>> : "+devide(10,5));
	</script>
</body>
</html>
```

> **document 출력 결과**

![](https://images.velog.io/images/yunyoseob/post/f12ff869-0e21-4ae5-8b3a-dad686052de1/image.png)


> **javascript 객체 리터럴로 객체 생성 : 리터럴 객체**

```javascript
// 앞뒤 생략
console.log("자바스크립트의 객체 : 객체 리터럴로 객체 생성하기");
var card={suit:"하트",rank:"A"};
var card1={"suit":"하트", "rank":"A"};
// 객체 리터럴, 리터럴 객체 : {....}
// 변수 card
// property 이름 : suit, "suit"
// property 값 : "하트", "A"
console.log("typeof(card) >>> : "+typeof(card));
console.log("typeof(card1) >>> : "+typeof(card1));
console.log("card의 suit 키의 값 >> : "+card.suit);
console.log("card1의 suit 키의 값 >> : "+card1.suit);
console.log("card의 rank 키의 값 >> : "+card.rank);
console.log("card1의 rank 키의 값 >> : "+card1.rank);
```

javascript는 객체 리터럴로 객체를 생성 할 수 있습니다. 객체 리터럴은 {}안에 key와 value형식으로 설정할 수 있습니다. 

key 형식에는 property 이름을 value 형식에는 property 값을 {"property이름":"property 값"}으로 객체를 설정 할 수 있습니다.

> **개발자도구 Console 출력 결과**

```javascript
자바스크립트의 객체 : 객체 리터럴로 객체 생성하기
typeof(card) >>> : object
typeof(card1) >>> : object
card의 suit 키의 값 >> : 하트
card1의 suit 키의 값 >> : 하트
card의 rank 키의 값 >> : A
card1의 rank 키의 값 >> : A
```

## jQuery

jQuery는 javascript를 함수로 구현해 놓은 라이브러리 입니다.

![](https://images.velog.io/images/yunyoseob/post/6e3f408c-ba4d-4b83-b97b-2d03ff48fb38/image.png)

- [jQuery 공식 홈페이지 바로가기](https://jquery.com/)

> **CDN : Content Deliveery Network**

CDN은 웹사이트의 접속자가 콘텐츠를 다운로드 할 때 자동으로 가장 가까운 서버에서 다운로드 할 수 있도록 하는 기술입니다.

```javascript
// jQuery 불러오기
<script src="http://code.jquery.com/jquery-latest.min.js"></script>
/*! jQuery v1.11.1 | (c) 2005, 2014 jQuery Foundation, Inc. | jquery.org/license */
```

> **jQuery 명령어 시작 예시** 

jQuery는 $(document).ready() 형식으로 사용할 수 있는데, 이 외에도 다양한 방법이 있습니다.

```javascript
$(document).ready(function(){});

window.jQuery(document).ready(function(){});

jQuery(document).ready(function(){});

window.$(document).ready(function(){});
```                  

### jQuery 함수 체이닝 기법

jQuery는 스크립트 블럭 ready 함수 블럭 안에서 함수들을 연결하여 사용할 수 있습니다.

> **jQuery 사용 예시**

```javascript
// 앞뒤 생략..

// $(document).ready(function(){});
$(document).ready(function(){
	// $("#아이디명").click(function({});
	$("#아이디명").click(function({
    	// $("#아이디명).attr({}).submit();
    	$("#아이디명).attr(
      		{
      			"action":"#",
      			"method":"GET"
    		}
          ).submit();
    });

	// $("#아이디명").click(function(){});
	$("#아이디명").click(function(){
    		var 변수명=$("#아이디명");
      		변수명.attr("action", "#");
      		변수명.attr("method", "GET");
      		변수명.submit();
    });
});
```

> **jQuery 시작하는 키워드**

```javascript
$ : jQuery를 시작하는 키워드
#아이디명 : css 선택자에서 #아이디명 : 태그의 id 속성의 이름을 가르킵니다.
$("#아이디명") :jQuery 함수를 이용해서 CSS 선택자를 이용해서 DOM Tree Node List(태그 요소 노드, 내용 텍스트 노드, 속성 노드)에서 아이디 속성의 값을 찾습니다.
$("#노드명") : html 웹 문서의 DOM Tree 노드 리스트에서 아이디 속성값이 노드명인 노드를 찾습니다.

$("#노드명").click(); : html 웹 문서의 DOM Tree 노드 리스트에서 아이디 속성값이 노드명인 노드를 찾아서  click 이벤트를 수행합니다.
```

### jQuery 활용 예제

HTML FORM 태그를 활용하여 아이디와 비밀번호를 입력 받은 뒤, 이를 jQuery를 활용하여, JSP File로 넘어갈 수 있습니다.

JSP File는 Web Server에서 WAS(Web Application Server)로 해당 데이터를 넘긴 뒤, JDBC로 Oracle DB와 연결된 JAVA 클래스에 생성자를 생성한 뒤, 정보를 조회 할 수 있습니다.


> **html, css, javascript, jQuery <=> JSP <=> java <=> Oracle DB**

이번 포스팅에서는 아이디와 비밀번호를 입력받아, jQuery로 JSP File로 이동하여, JSP File에서 입력받은 아이디와 비밀번호를 출력시키도록 하겠습니다.


> **jQueryPractice.html**

```javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>제이쿼리 테스트</title>
<style type="text/css">
	*{
	width:500px;
	margin:10px auto;
	}
</style>
<script src="https://code.jquery.com/jquery-1.12.4.js"></script>
<script type="text/javascript">
	$(document).ready(function(){
		$("#login_btn").click(function(){
			$("#login").attr(
				{
					"action":"/firstWeb/cgiForm/jQueryPractice.jsp",
					"method":"GET"
				}		
			).submit();			
		});
	});
</script>
</head>
<body>
	<fieldset>
	<h3>로그인서비스</h3>
	<hr>
	<form name="login" id="login">
		아이디 : <input type="text" name="uid" id="uid"/>
		<hr>
		비밀번호 : <input type="password" name="upw" id="upw"/>
		<hr>
		<input type="button" id="login_btn" value="로그인하기">
		<input type="reset" value="취소">			
	</form>
	</fieldset>
</body>
</html>

```

> **화면**

![](https://images.velog.io/images/yunyoseob/post/285022d7-b332-4f9d-8c71-9028a1de7f97/image.png)

> **jQueryPractice.html**

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Login Check</title>
</head>
<body>
	<h3>Login Check</h3>
	<hr>
<%= "Login Check를 시작합니다." + "<br>"%>
<%
	String uid=request.getParameter("uid");
	String upw=request.getParameter("upw");
%>
<%= "입력된 아이디는 : "+uid+"입니다."+"<br>" %>
<%= "입력된 비밀번호는 : "+upw+"입니다."+"<br>" %>
</body>
</html>
```

> **로그인하기 결과**

![](https://images.velog.io/images/yunyoseob/post/c41254bc-b772-4317-b74d-7f8e1e0bdffe/image.png)

해당 값을 DB에서 아이디와 비밀번호를 조회 후, 틀릴 경우, javascript의 history.go(-1) 명령어를 통해 뒤로 가기를 할 수도 있고, 맞을 경우, javascript의 location.href 명령어를 통해 DB에 insert를 하는 jsp 파일로 넘어갈 수도 있을 것입니다.

이처럼 javascript, jQuery, JSP, java를 활용하여 DB 조회부터 화면 출력까지 다양하게 활용할 수 있습니다.

**이상으로, [js, jQuery] javascript, jQuery 기초 포스팅을 마치도록 하겠습니다. 😀**
