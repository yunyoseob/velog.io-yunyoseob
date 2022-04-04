안녕하세요. 😀 오늘은 JavaScript와 jQuery를 활용하여 HTML FORM TAG에 있는 데이터를 JSP 파일로 보내는 방법에 대해 포스팅해보도록 하겠습니다.

### 들어가기 앞서서..

HTML FORM TAG의 경우 [[HTML]FORM TAG](https://velog.io/@yunyoseob/HTMLFORM-TAG)편에서 포스팅 하였습니다. FORM TAG를 처음 보신다면 참고하고 오시면 좋을듯 해요 ㅎㅎ 😃

JavaScript와 jQuery를 처음 들어보신다면 [[js, jQuery]JavaScript, jQuery 기초](https://velog.io/@yunyoseob/js-jQuery-javascript-jQuery-%EA%B8%B0%EC%B4%88)편에서 기초내용을 포스팅 하였으니 참고하고 오시면 좋을 듯 합니다 ㅎㅎ 😃

### HTML FORM TAG : JavaScript를 이용하여 jsp파일로 보내기

> **formtagpractice.html**

```javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>FORM TAG 연습</title>
<script type="text/javascript">
	function moveData(){
		var getDataForm=window.document.getData;
		console.log("window.document.getData >>> : "+getDataForm);
		console.log("typeof(window.document.getData) >>> : "+typeof(getDataForm));
		
		var getDataForm_1=window.document.getElementById("getDate");
		console.log("window.document.getElementById :: getDate >>> : "+getDataForm_1);
		console.log("typeof() :: window.document.getElementById :: getDate >>> : "+typeof(getDataForm_1));
		
		var getDataForm_2=window.document.forms[0];
		console.log("window.document.forms[0] >>> : "+getDataForm_2);
		console.log("typeof(window.document.forms[0]) >>> : "+typeof(getDataForm_2));
		
		var getInputtag=window.document.forms[0].elements[0];
		console.log("window.document.forms[0].elements[0] >>> : "+getInputtag);
		console.log("typeof(window.document.forms[0].elements[0]) >>> : "+typeof(getInputtag));
		
		var input_mname=window.document.forms[0].elements[0].value;
		console.log("window.document.forms[0].elements[0].value >>> : "+input_mname);
		console.log("typeof() :: window.document.forms[0].elements[0].value >>> : "+typeof(input_mname));
		
		var input_mname_2=document.getElementsByTagName("input")[0].value;
		console.log("document.getElementsByTagName :: input :: [0].value >>> : "+input_mname_2);
		console.log("typeof() :: document.getElementsByTagName :: input :: [0].value >>> : "+typeof(input_mname_2));
		
		getDataForm_2.action="/firstWeb/getData/formtagpracticejsp.jsp"
		getDataForm_2.method="GET"
		
		getDataForm_2.submit();
	}
</script>
</head>
<body>
<h3>FORM TAG 연습</h3>
<hr>
<br>

<form 	name="getDataa" id="getDate" >
이름 : <input type="text" name="mname" id="mname"><br>
주소 : <input type="text" name="maddr" id="maddr"><br>
	 <input type="button" value="전송" onclick="moveData()">
</form>

<form>
</form>

</body>
</html>
```
> **formtagpractice.jsp**

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>FORM TAG 연습</title>
</head>
<body>
<h3>FORM TAG 연습 ::  JSP에 넘어온 데이터 보기</h3>

<%
	String name=request.getParameter("mname");
	String addr=request.getParameter("maddr");
	
	out.println("formtagpractice.html에서 받아온 이름 >>> : "+name+"<br>");
	out.println("formtagpractice.html에서 받아온  주소 >>> : "+addr);
%>

</body>
</html>
```

> **jsp 파일 :: 주소표시줄 및 화면**

**✔ 주소표시줄**

```html
http://컴퓨터주소:포트번호/firstWeb/getData/formtagpracticejsp.jsp?mname=%ED%95%98%EC%9D%B4&maddr=%EB%B2%A8%EB%A1%9C%EA%B7%B8
```

**✔ 화면**

![](https://media.vlpt.us/images/yunyoseob/post/a7a5f4b3-3d91-4bca-9ba7-f7f37e7528bc/image.png)

> **chrome 개발자도구 :: console 출력 결과**

```javascript
window.document.getData >>> : [object HTMLFormElement]
typeof(window.document.getData) >>> : object
window.document.getElementById :: getDate >>> : [object HTMLFormElement]
typeof() :: window.document.getElementById :: getDate >>> : object
window.document.forms[0] >>> : [object HTMLFormElement]
typeof(window.document.forms[0]) >>> : object
window.document.forms[0].elements[0] >>> : [object HTMLInputElement]
typeof(window.document.forms[0].elements[0]) >>> : object
window.document.forms[0].elements[0].value >>> : 하이
typeof() :: window.document.forms[0].elements[0].value >>> : string
document.getElementsByTagName :: input :: [0].value >>> : 하이
typeof() :: document.getElementsByTagName :: input :: [0].value >>> : string
```

### 출력결과 설명

> **eclipse :: Outline**

![](https://media.vlpt.us/images/yunyoseob/post/6eeebf16-069b-4ff7-959f-158a4e1b4084/image.png)

출력 결과를 이해하기 위해서는 DOM Tree 구조를 이해하면 쉽게 이해할 수 있습니다.
DOM Tree구조는 [[HTML]HTML 기초 1편](https://velog.io/@yunyoseob/HTML-HTML-%EA%B8%B0%EC%B4%88-1%ED%8E%B8)에서 언급한 적이 있으니, 참고하시면 좋을 듯 합니다. 😃

> **window.document.태그이름**

- Outline을 보면, 먼저, window.document.getData를 출력하면, 태그의 이름이 getData인 태그를 object로 지정합니다. 해당 태그는 form 태그이므로, 해당 객체를 출력할 경우, HTMLFormElement가 출력 되는 것을 확인 할 수 있습니다.

> **window.document.getElementById("아이디명")**

- window.document.getElementById("getDate")을 출력하면, 태그의 아이디명이 getDate인 태그를 object로 지정합니다. 

> **window.document.forms[0]**

- window.document.forms[0]을 출력할 경우, form 배열중 가장 첫 번째 form을 찾아 object로 지정하여 출력할 수 있습니다.

> **window.documnet.forms[0].elements[0]**

window.documnet.forms[0].elements[0]을 출력할 경우, form 배열중 가장 첫 번째 form의 가장 첫 번째 elements를 출력할 수 있습니다. 이 때의 경우, 해당 elements가 input태그이므로, object HTMLInputElement로 출력됩니다.

> **window.document.forms[0].elements[0].value**

window.document.forms[0].elements[0].value로 출력할 경우, 해당 element의 value를 출력시킬 수 있습니다.

**🤔 HTML 태그 아이디와 태그 이름은 무슨 차이인가요?**

- 태그 아이디는 해당 웹문서에서 유일해야 하지만, 태그 이름은 유일하지 않아도 괜찮다는 특징이 있습니다. 태그 아이디가 겹칠 경우, 마지막 태그 아이디의 값을 찾아가게 됩니다. DOM Tree의 각 태그들을 식별할 때, 다 다른 아이디를 통해 찾아올 수 있습니다.


> **✔ 유의사항**

1. JavaScript에서 해당 객체의 값에 새로운 값을 대입하여도, 주소표시줄 구분자(?) 뒤의 Query String은 변하지 않습니다.

```html
http://컴퓨터주소:포트번호/firstWeb/getData/formtagpracticejsp.jsp?mname=%ED%95%98%EC%9D%B4&maddr=%EB%B2%A8%EB%A1%9C%EA%B7%B8
```
2. 주소표시줄에서는 [EBCDIC코드](https://ko.wikipedia.org/wiki/%ED%99%95%EC%9E%A5_%EC%9D%B4%EC%A7%84%ED%99%94_%EC%8B%AD%EC%A7%84%EB%B2%95_%EA%B5%90%ED%99%98_%EB%B6%80%ED%98%B8)로 출력되는데, 이유는 FORM 태그에서 정보를 넘길 때, Default enctype이 **application/x-www-form-urlencoded** 이기 때문입니다. 

3. 주소표시줄에서 EBCDIC코드여도, JSP로 파일을 받았을 때, 한글로 잘 출력되는 것을 확인 할 수 있습니다. 

### FORM TAG의 정보를 변형하여 JSP 파일로 보내기


> **1번째 formtagpractice.html**

```javascript
// 앞뒤 생략
<script type="text/javascript">
	function moveData(){
		var getDataForm_1 = window.document.getElementById("getData");
		var input_mname_2=document.getElementsByTagName("input")[0].value;
		input_mname_2='하이2';
		console.log("input_mname_2 : "+input_mname_2);
		
		getDataForm_1.action="/firstWeb/getData/formtagpracticejsp.jsp"
		getDataForm_1.method="GET"
		
		getDataForm_1.submit();
	}
</script>
```

**✔ 실제로 넘어가는 데이터**

```html
?mname=하이&maddr=벨로그
```

다음과 같이 변수로 설정한 값에 새로운 변수를 대입한다고 하여도, 실제로는 주소표시줄 ?뒤의 하이와 벨로그가 넘어가서 출력됩니다. (하이2가 출력되지 않습니다.)

> **2번째 : formtagpractice.html**

```javascript
// 앞뒤 생략
<script type="text/javascript">
	function moveData(){
		var getDataForm_1 = window.document.getElementById("getDate");
		document.getElementsByTagName("input")[0].value="하이2";
		
  		/*
        document.getElementById("mname").value = "하이3";
		window.document.forms[0].elements[0].value="하이4";
		getDataForm_1[0].value="하이5";
        */
  
  
		getDataForm_1.action="/firstWeb/getData/formtagpracticejsp.jsp"
		getDataForm_1.method="GET"
		
		getDataForm_1.submit();
	}
</script>
```

**✔ 실제로 넘어가는 데이터**

```html
?mname=하이2&maddr=벨로그
```

다음과 같이 document 객체의 input 태그의 첫 번째 값을 직접 선언하는 경우, 이름에 어떤 값을 입력하여도, 넘어가는 데이터는 하이2가 됩니다.

```javascript
document.getElementById("mname").value = "하이3";
window.document.forms[0].elements[0].value="하이4";
getDataForm_1[0].value="하이5";
```

위의 코드의 경우에도 실제로 넘어가는 데이터는 다음과 같이 넘어갑니다.

```html
?mname=하이3&maddr=벨로그
?mname=하이4&maddr=벨로그
?mname=하이5&maddr=벨로그
```

즉, 실제 document 객체의 value를 수정하거나, 실제 보낼 객체의 하위 element의 value를 직접 수정하는 경우, 수정한 데이터가 jsp파일로 넘어가서 출력이 됩니다.

### HTML FORM TAG : jQuery를 이용하여 jsp파일로 보내기

> **formtagpractice.html**

```javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>FORM TAG 연습</title>
<script  src="http://code.jquery.com/jquery-latest.min.js"></script>
<script type="text/javascript">
	$("#getDate").ready(function(){
		$("#btn").click(function(){
		let mname=$("#mname").val();
		console.log("mname >>> : "+mname);
          // mname >>> 하이
		$("#getDate").attr(
				{
					"action":"/firstWeb/getData/formtagpracticejsp.jsp",	
					"method":"GET"
				}
		).submit();
		})
	})
	
		
</script>
</head>
<body>
<h3>FORM TAG 연습</h3>
<hr>
<br>

<form 	name="getData" id="getDate" >
이름 : <input type="text" name="mname" id="mname"><br>
주소 : <input type="text" name="maddr" id="maddr"><br>
	 <input type="button" value="전송" id="btn">
</form>

<form>
</form>

</body>
</html>
```

**✔ 실제로 넘어가는 데이터**

```html
?mname=하이&maddr=벨로그
```

JavaScript와 마찬가지로 jQuery를 사용하여 데이터를 넘길 수도 있습니다.

### 코드 설명

> **$("#태그아이디명").ready(function(){});**

jQuery를 사용하여 form 태그 아이디인 getDate명을 찾은 다음, ready함수에 입력합니다.

![](https://media.vlpt.us/images/yunyoseob/post/447d5c42-9795-465a-b947-9228f8db9d49/image.png)

- [jQuery API : .ready()](https://api.jquery.com/ready/#ready-handler)

> **$("#태그아이디명").click(function(){});**

btn이라는 태그 아이디를 클릭할 경우, 해당 이벤트가 수행되는 함수 입니다.

![](https://media.vlpt.us/images/yunyoseob/post/ef3f6ff5-9c28-442d-9b1e-5dcdb6acc7e0/image.png)

- [jQuery API : .click()](https://api.jquery.com/click/#click-handler)


> **$("#태그아이디명").attr({}).submit();

getDate라는 태그 아이디의 속성을 지정하여 해당 이벤트를 수행합니다.

- .attr()

![](https://media.vlpt.us/images/yunyoseob/post/67fd0213-1f7c-44bb-a68b-c692378080f3/image.png)

- [jQuery API : .attr()](https://api.jquery.com/attr/#attr-attributeName)

- .submit()

![](https://media.vlpt.us/images/yunyoseob/post/cfbf7de0-afdf-4f69-a5ac-ff8c2f4d7772/image.png)

- [jQuery API : .attr()](https://api.jquery.com/submit/#submit-handler)


### FORM TAG의 정보를 변형하여 JSP 파일로 보내기

JavaScript와 마찬가지로, jQuery 또한, HTML의 Form Tag의 들어온 정보를 변형하여  JSP 파일에 보낼 수 있습니다.

> **formtagpractice.html**

```javascript
// 앞뒤 생략
	$("#getDate").ready(function(){
		$("#btn").click(function(){
			$("#mname").val('하이5');
		$("#getDate").attr(
				{
					"action":"/firstWeb/getData/formtagpracticejsp.jsp",	
					"method":"GET"
				}
		).submit();
		})
	})	
</script>
```


**✔ 실제로 넘어가는 데이터**

```html
?mname=하이5&maddr=벨로그
```

입력값으로 이름에 하이와 주소에 벨로그를 입력하여도 $("#mname").val('하이5'); 해당 명령어로 하이5라는 값을 jsp파일에 넘길 수도 있습니다.

```javascript
$('input[name=mname]').val('하이6');
document.getData.mname.value='하이7';
```

위의 코드의 경우에도 실제로 넘어가는 데이터는 다음과 같이 넘어갑니다.

```html
?mname=하이6&maddr=벨로그
?mname=하이7&maddr=벨로그
```

JavaScript와 jQuery의 이러한 특징을 이용하여, Form Tag에서 들어온 데이터를 그대로 JSP 파일에 보내줄 수도 있고, 상황에 따라 값을 바꿔서 JSP 파일로 보내줄 수도 있을 것입니다. 마지막으로, JSP 파일에서 데이터를 받는 request.getParameter 함수와 request.getParameterValues 함수를 간단히 소개하면서, 이번 포스팅을 마치도록 하겠습니다.

### jsp :: request

request는 내장 객체로 여러 함수를 이용하여 데이터를 요청하거나, 인코딩을 세팅하는 등의 작업을 수행할 수 있습니다.

- [Servlet 3.1 API - Apache Tomcat 8.0.53](https://tomcat.apache.org/tomcat-8.0-doc/servletapi/index.html)  

```javascript
// 앞 뒤 생략..
String name=request.getParameter("mname");
String addr=request.getParameter("maddr");
```

위의 코드가 있을 때, request.getParameter는 Form태그의 name 값을 가져옵니다.

![](https://media.vlpt.us/images/yunyoseob/post/5fad07bb-34fa-497b-ab94-369b1efa6c70/image.png)

한 편, 받아오는 name의 값이 하나가 아닐 경우, request.getParameterValues 명령어를 통해 배열로 받아올 수도 있습니다.

![](https://media.vlpt.us/images/yunyoseob/post/559c5a8e-6432-4919-a5d6-0c066dbcb816/image.png)


이 외에도 getParameterMap, getParameterNames 등, Enumeration으로 Return을 받을 수도 있고, Map으로 Returns을 받아 올 수 있습니다. 

**이상으로 [html, js, jQuery] FORM TAG 2편 포스팅을 마치도록 하겠습니다. 😃**


