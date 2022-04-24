안녕하세요 😊. 오늘은 XML과 XML을 활용하는 방법에 대해 간략히 소개해보도록 하겠습니다.

## XML이란?

![](https://velog.velcdn.com/images/yunyoseob/post/6388e61b-eab1-436e-aa56-b81dabfaecb3/image.png)

XML(eXtensible Markup Language)는 W3C에서 개발된, 다른 특수한 목적을 갖는 마크업 언어를 만드는데 사용하도록 권장하는 다목적 마크업 언어입니다. 

> **XML은 인터넷에 연결된 시스템끼리 데이터를 쉽게 주고 받을 수 있게 하여, HTML의 한계를 극복할 목적으로 만들어졌습니다.**

- 출처 : [위키백과 XML](https://ko.wikipedia.org/wiki/XML)


**🤔 HTML과 XML의 차이가 뭔가요?**

HTML은 태그로 구성되어 있는데, 만들어진 태그를 사용합니다. 반면 XML은 태그로 구성되어 있으나, 사용자 정의로 만든 태그로 사용하며, 데이터로 사용하고, DTD, XSD로 XML 규칙을 만듭니다.


## XML 태그 규칙

예시로, HTML에서 BODY에서 "VELOG POSTING TEXT입니다."를 출력시키려면 다음과 같이 코드를 작성할 수 있습니다.

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	VELOG POSTING TEXT입니다.
</body>
</html>
```

XML에서 "VELOG POSTING TEXT입니다."를 출력시키기 위한 과정은 다음과 같습니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<VELOG>
	<POSTING>
		<TEXT>
			VELOG POSTING TEXT입니다.
		</TEXT>
	</POSTING>
</VELOG>
```
다음과 같이 작성한 XML문서를 parser를 통해 jsp에서 출력시킬 수 있습니다.

여기서 &lt;VELOG&gt;는 루트 태그입니다. 

> **루트 태그는 유일해야 하며, XML의 태그는 배열이기 때문에 태그의 길이를 동일하게 사용해야 합니다.**

- 잘된 예시
```xml
<?xml version="1.0" encoding="UTF-8"?>
<VELOG>
	<POSTING>
		<TEXT>
			VELOG POSTING TEXT입니다.
		</TEXT>
	</POSTING>
    <POSTING>
		<TEXT>
			VELOG POSTING TEXT2입니다.
		</TEXT>
	</POSTING>
</VELOG>
```

- 잘못된 예시
```xml
<?xml version="1.0" encoding="UTF-8"?>
<VELOG>
	<POSTING>
		<TEXT>
			VELOG POSTING TEXT입니다.
		</TEXT>
	</POSTING>
    <POSTING>
		<TEXT>
          <MEMO>
			VELOG POSTING TEXT2입니다.
          </MEMO>
		</TEXT>
	</POSTING>
</VELOG>
```

XML로 작성한 문서를 jsp에서 출력시키기 위해서는 parser가 필요한데, 먼저 JavaScript의 DOMParser를 통해 출력시키는 방법을 먼저 소개하도록 하겠습니다.

## XML 데이터 출력하기

먼저, DOMParser를 사용하지 않고, jsp에서 BufferedReader 클래스의 참조변수를 통해 XML 데이터를 담고 BODY에서 출력시킬 때, 결과는 다음과 같습니다.

> **velog.jsp**

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!--  java.io, java.net 패키지의 클래스 import 해오기 -->
<%@ page import="java.io.BufferedReader" %>
<%@ page import="java.io.InputStreamReader" %>
<%@ page import="java.net.URL" %> 
<!--  log4j import 해오기 -->
<%@ page import="org.apache.log4j.LogManager" %>
<%@ page import="org.apache.log4j.Logger" %>
<%
Logger logger=LogManager.getLogger(this.getClass()); 
	String strHtml="";
	String strLine="";
	try{
		String strUrl="http://localhost:8088/velog.xml의 디렉토리";
		// xml 주소 불러오기
		
		BufferedReader br=new BufferedReader(
				new InputStreamReader((new URL(strUrl)).openConnection().getInputStream(), "UTF-8"));
		
		while((strLine=br.readLine())!=null){
			strHtml+=strLine;
		}
		logger.info("strHtml >>> : "+strHtml);
		br.close();
	}catch(Exception e){
		logger.info("error >>> : "+e.getMessage());
	}
%>       
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>XML PARSING</title>
</head>
<body>
<%= strHtml %>
</body>
</html>
```

> **화면 결과**

![](https://velog.velcdn.com/images/yunyoseob/post/969f0464-3409-42c0-bbae-9633c64a7755/image.png)

결과는 원하는 대로 나왔지만, 개발자 도구에서는 다음과 같이 나옵니다.

![](https://velog.velcdn.com/images/yunyoseob/post/d3e3c5e0-b07e-48f6-a773-170ddb77b3ae/image.png)

JavaScript의 DOMParser를 쓰면 어떻게 바뀔까요?

## DOMParser

JavaScript에서 DOMParser에 대한 설명은 다음과 같이 설명 되어 있습니다.

![](https://velog.velcdn.com/images/yunyoseob/post/a36cb76f-df49-4af9-bdcb-1ec80890141a/image.png)

- 출처 : [M mdn web docs](https://developer.mozilla.org/ko/docs/Web/API/DOMParser)

문법의 경우 var xmlText = new DOMParser() 명령어를 통해 소스코드를 해석할 수 있는 기반을 제공 할 수 있습니다.

> **DOMParser.parseFromString()**

![](https://velog.velcdn.com/images/yunyoseob/post/1cbcb6ee-3a30-450b-a00a-16f406c85871/image.png)

![](https://velog.velcdn.com/images/yunyoseob/post/0351202d-d2c8-4098-9ca0-5f85efe63534/image.png)

mimeType 인자를 통해 정의한 형식에 따른 Document 또는 XMLDocument 문서를 반환할 수 있습니다.

## DOMParser 활용 예제

앞의 velog.jsp 파일에 DOMParser를 활용하여 어떻게 달라지는지 보도록 하겠습니다.

> **velog.jsp**

```javascript
// jsp 영역 내용은 이전과 같으므로 생략..
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>XML PARSING</title>
<script src="http://code.jquery.com/jquery-latest.min.js"></script>
<script type="text/javascript">
 $(document).ready(function(){
	var xmlText, xmlParser, xmlDoc;
	
	xmlText='<%= strHtml %>';
	console.log("xmlText >>> : "+xmlText);
	
	xmlParser=new DOMParser();
	xmlDoc=xmlParser.parseFromString(xmlText, "text/xml");
	console.log("xmlDoc >>> : "+xmlDoc);
	
	$("#parseText").click(function(){
		console.log(xmlDoc.getElementsByTagName("TEXT")[0].childNodes[0].nodeValue);
		document.getElementById("text").innerHTML=xmlDoc.getElementsByTagName("TEXT")[0].childNodes[0].nodeValue
	});
	
	$("#parseFind").click(function(){
		var txt=$(xmlDoc).find("TEXT").text();
		console.log("txt >>> : "+txt);
		document.getElementById("text").innerHTML=txt;
	});
	
 });

</script>
</head>
<body>
<h3>XML PARSING 하기</h3>
<button id="parseText">DOM Parser로 XML 파싱하기</button>
<button id="parseFind">find() 함수로 파싱하기</button>
<p id="text"></p>
</body>
</html>
```

> **화면 결과**

![](https://velog.velcdn.com/images/yunyoseob/post/8b4ada44-9afb-4d9b-8a7e-f4e22357d134/image.png)

DOMParser로 XML 파싱하기 혹은 find() 함수로 파싱하기 버튼을 누르면 다음과 같은 결과과 화면에 나타납니다.

![](https://velog.velcdn.com/images/yunyoseob/post/208f5dd5-501a-4b47-87c7-abecb6d00fb3/image.png)

**🤔 이전과 차이점은?**

![](https://velog.velcdn.com/images/yunyoseob/post/9a74c946-e4d3-4da4-9c23-9bf4c4dbaa50/image.png)

이전과 다르게 개발자 도구에서 XML 태그가 다 사라지고  XML TEXT태그의 내용만 출력된 것을 볼 수 있습니다.

### velog.jsp 코드 해설

> **1. JavaScript 변수에 jsp의 변수 대입**

```javascript
xmlText='<%= strHtml %>';
```

jsp에서 만든, &lt;?xml version ~~~ &lt;/VELOG&gt; 내용을 JavaScript의 xmlText 변수에 대입합니다.

> **2. DOMParser() 활용**

```javascript
xmlParser=new DOMParser();
xmlDoc=xmlParser.parseFromString(xmlText, "text/xml");
```

자바스크립트에서 DOMParser 객체를 인스턴스 합니다. 이후, parseFromString() 함수에서 자바스크립트 변수에 담겨있는 xml 파일 형식으로 파싱을 합니다. 

이를 자바스크립트 변수인 xmlDoc에 대입합니다.

> **3. 클릭이벤트 만들어, JavaScript 혹은 jQuery로 innerHtml으로 출력시키기**

```javascript
$("#parseText").click(function(){
		console.log(xmlDoc.getElementsByTagName("TEXT")[0].childNodes[0].nodeValue);
		document.getElementById("text").innerHTML=xmlDoc.getElementsByTagName("TEXT")[0].childNodes[0].nodeValue
	});
	
	$("#parseFind").click(function(){
		var txt=$(xmlDoc).find("TEXT").text();
		console.log("txt >>> : "+txt);
		document.getElementById("text").innerHTML=txt;
```     

HTML에 DOM Parser로 XML 파싱하기 버튼을 클릭하면 클릭이벤트를 발생시킵니다. 이후, xmlDoc에 있는 XML에서 TEXT 태그의 nodeValue를 p태그에서 innerHTML으로 출력시킵니다.

한 편, jQuery에 find().text() 함수로 TEXT 태그를 찾아서 태그를 제외한 해당 내용은 text함수로 출력시키는 방법도 있습니다. 


다음 시간에는 XML을 더 다양하게 활용하는 방법에 대해 이어서 포스팅하도록 하겠습니다. 🙂 

이상으로 [XML] XML 활용 기초 포스팅을 마치도록 하겠습니다.
