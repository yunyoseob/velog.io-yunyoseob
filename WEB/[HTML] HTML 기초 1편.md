안녕하세요. 😀 오늘은 HTML 기초에 대해 포스팅 해보도록 하겠습니다.

## 들어가기 전에..

HTML은 Hyper Text Markup Language로 Hyper Text는 문서를 서로 연결해 주는 링크를 의미하며, Markup은 마크업을 표시합니다.

Hyper Text Markup Language를 만든 문서를 웹 문서라고 합니다. 
- 확장자는 html, htm

HTML을 읽어주는 프로그램이 브라우저이며, 웹 문서를 읽어주는 프로그램이 웹 브라우저 입니다.

> **HTML과 브라우저의 관계**

HTML로 작성된 문서는 브라우저를 통해 나타납니다. 
- 랜더링 과정을 통해 나타납니다.

[How browsers work](https://taligarsiel.com/Projects/howbrowserswork1.htm)에 들어가면 browsers의 작동 방식에 대해 볼 수 있습니다.

![](https://images.velog.io/images/yunyoseob/post/55f3928c-8371-4572-b5ab-4a60d28d4c52/image.png)

Tali Garsiel이 해당 문서를 웹에 배포하였는데, Tali Garsiel과 Paul lrish 개발자의 [How Browsers Work : Behind the scenes of modern web browsers](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)에서도 볼 수 있습니다.

- 한국어로 보고 싶다면, Naver D2에서 작성한 ["브라우저는 어떻게 동작하는가?"](https://d2.naver.com/helloworld/59361)로 볼 수 있습니다.


> **렌더링 엔진**

Naver D2에서 작성한 "브라우저는 어떻게 동작하는가?"의 렌더링 엔진 동작 과정 예시는 다음과 같습니다.

![](https://images.velog.io/images/yunyoseob/post/ed780194-78b2-42c1-84de-97ec2d478b9d/image.png)

html는 태그 <>라는 것을 사용하는데, html 태그가 DOM Tree로 변경되면 태그 안에 있는 요소를 node라고 칭합니다. 렌더링 엔진은 HTML 문서를 파싱하고 "콘텐츠 트리" 내부에서 태그를 DOM 노드로 변환합니다. 그 다음 외부 CSS 파일과 함께 포함된 스타일 요소도 파싱한다. 

## HTML

- 필자는 html5 기준으로 작성하였습니다.

![](https://images.velog.io/images/yunyoseob/post/796ae088-10cc-47f1-8169-e25d545fc5fc/html5.JPG)


> **HTML 구성**

- html 구성

```html
태그 tag
요소 element
<p>내용</p>
<p 속성1=속성값1>내용</p>
속성 attribute
내용 contents
```

이클립스에서 html5 문서를 생성하면 다음과 같은 코드가 나타납니다.

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>

</body>
</html>
```

> **<!DOCTYPE>**

```html
<!DOCTYPE html>
```

해당 타입을 독타입이라고 부릅니다. 해당 내용을 보고 HTML 버전을 인지할 수 있습니다.

예시로, 이클립스에서 HTML 4.01 버전으로 html 파일을 생성할 경우 다음과 같은 코드가 나타납니다.

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
		<title>Insert title here</title>		
	</head>
	<body>
		
	</body>
</html>
```

맨 첫 줄의 독타입을 통해 버전이 다름을 인지 할 수 있습니다. 해당 버전을 보고 예시로 [HTML 4.01 버전](http://www.w3.org/TR/html4/loose.dtd)이면 버전에 알맞은 사용법을 보고, [HTML 5](https://html.spec.whatwg.org/)라면 해당 버전에 알맞은 사용법을 보고 작성하면 됩니다.

> **html 태그**

html은 웹 문서의 시작과 끝을 알리는 태그 입니다.

```html
<html lang="en">
```  

다음과 같이 작성할 경우, lang 속성(문서에서 사용할 언어)를 영어로 지정하여, 검색 사이트에서 영어로 제한해 검색할 때 사용할 수 있습니다.


> **head 태그**

head 태그는 title태그, meta태그, script태그, style 태그 등등을 작성 할 수 있습니다.

> **meta 태그**

meta 정보는 데이터에 관한 데이터를 의미합니다. 문자 세트를 비롯해 문서 정보가 들어 있는 테그이며, 웹 브라우저에는 보이지 않지만, 웹 문서와 관련된 정보를 지정할 때 사용합니다.

```html
<meta charset="UTF-8">
```

만약 위와 같이 표기하면, 웹 브라우저에 글자를 표시 할 때 UTF-8 인코딩을 지정할 수 있습니다. 

- 웹 서버는 영어가 기본이며, meta 태그에 인코딩을 명시하지 않으면 웹 브라우저에서 자동으로 인코딩을 처리합니다.

> **title 태그**

title 태그는 사이트 제목 태그로, 웹 브라우저 상단 바에 나타날 제목을 작성할 수 있습니다. 

- 즐겨찾기 등록시 즐겨 찾기 제목, 검색 엔진의 결과 제목, 웹 브라우저의 제목 표시줄에 표시의 특징이 있습니다.

> **body 태그**

웹 브라우저에 내용을 표시하는 태그로, 문서 유형을 정의하고 문서 정보를 입력하면 &lt;body&gt;&lt;/body&gt; 사이에 실제 웹 브라우저에 표시할 내용을 입력 합니다.

- **Tip!**

```html
&lt;body&gt;&lt;/body&gt;

- 이렇게 작성하면 <body></body> 내용을 표기할 수 있습니다.
```

## HTML 태그

> **HTML을 연습하기 좋은 사이트**

[Learn to Code](https://www.w3schools.com/)에서 HTML에서 직접 태그를 통해 실습을 할 수도 있습니다. 

![](https://images.velog.io/images/yunyoseob/post/18fbe356-3298-4619-92d2-1deeb3f9b571/image.png)

해당 화면에서 HTML Reference를 클릭하면, 태그 정보들을 볼 수 있습니다.

![](https://images.velog.io/images/yunyoseob/post/39e982cf-e398-4d34-b8e0-001aa1ed0e51/image.png)


다음은 HTML 태그 관련 자료와 설명입니다.

> **HTML 태그 관련 자료**

```html
<h1> ~ <h6> 제목을 나타내는 태그 
<hr> 
<p> 텍스트 단락 태그
<br> 줄 바꾸는 태그 
<blockquote> 인용할 때 사용하는 태그 "" 대신 사용
	다른 텍스트보다 약간 들여 쓴다.
<strong>, <b> 텍스트를 굵게 표시
	strong : 경고나 주의사항등 중요내용 강조 
	b : 단순히 글자만 굵게 표시
<em>, <i> 기울인 텍스트
	em : 이탤릭체 강조 emphasis
	i : 이탤릭체 italic
<ol>, <li> 순서 있는 목록
	<ol type='a' start='3'>
<ul>, <li> 순서 없는 목록
<dl>, <dt>, <dd> 설명 목록


---------------------------------------
<table>, <caption> 
	table : 표를 만드는 태그 
	caption  : 표의 제목 태그 
<tr> 행을 만드는 태그 
<td>, <th> 셀을 만드는 태그 
	th : 내용을 진하게 표시, 
		 셀 안에서 중앙에 배열되므로 눈이 뜀
<thead>, <tbody>, <tfoot> 표의 구조를 지정하는 태그 
	thead : 제목
	tbody : 본문
	tfoot : 요약 
rowspan, colspan 행, 열을 합치는 속성
	<td rowspan="합칠 셀의 개수">행을 합침</td>
	<td colspan="합칠 셀의 개수">열을 합침</td>

<img> 이미지를 삽입하는 태그 
	<img src="이미지 파일 경로" alt="대체용 텍스트">

------------------------------------
이미지 경로는 웹서버의 상대경로 사용해야 한다.
이미지 경로는 절대경로를 사용하면 안 된다.
------------------------------------

src 이미지 파일 경로는 나타내는 속성
	웹 문서와 같은 폴더에 있는 이미지 파일 경로 
		<img src="xxx.jpg">
	웹 문서 하위 폴더에 있는 이미지 파일 경로 
		<imt src='images/xxx.jpg">

alt 이미지를 텍스트로 대신 설명하는 속성

width, height 이미지 크가를 조절하는 속성
	width 이미지 너비
	height 이미지 높이 
	2개 속성을 모두 사용할 수 있고 
	1개만 지정해도 나머지 속성은 비율을 자동으로 계산
	
	% 퍼센트 : 현재 웹 브라우저 창의 너비와 높이를 기준으로 이미지 크기를 결정
	px 픽셀 : 이미지 너비와 높이를 해당 픽셀 크기만큼 표시 


---------------------------------------
                  
<audio>, <video> 오디오와 비디오 파일을 삽입하는 태그 
	<audio src="오디오 파일 경로"></audio>
	<video src="비디오 파일 경로"></video>

controls	플레이어 화면에 컨트롤 바를 표시
autoplay	오디오나 비디오 자동으로 실행
loop		오디오나 비디오를 반복 재생
muted		오디오나 비디오의 소리 제거 
preload		페이지를 불러올 때 어떻게 로딩할 것인지 지정
			사용할 값 : auto, metadata, none 
			preload="auto"

width, height 비디오 플레이어의 너비와 높이 지정
poster="파일 이름" 비디오 태그 속성, 
				 비디오가 재생되기 전까지 화면에 표시할 포스터 이미지 

<object>, <embed> 다양한 멀티미디어 파일을 삽입하는 태그 
	<object width="너비" height="높이" data="파일"></object>
	<embed src="파일 경로" width="너비" height="높이">

---------------------------------------
                  
<a>, href 링크를 삽입하는 태그 및 속성
	<a href="링크할 주소>텍스트 또는 이미지</a>
	<a> href="주소><img src="">텍스트</a>
	


<form> 폼 태그 
-------------------------
	<form [속성="속성값"]>폼 요소</form>

	form 태그 속성
	name	자바스크립트로 폼을 제어할 때 사용하는 폼 이름 지정
	id		자바스크립트로 폼을 제어할 때 사용하는 폼 이름 지정
	method	폼 요소 내용을 서버쪽 프로그램에 넘겨주는 방식 지정 
		get	256 ~ 4096byte 서버로 전송 가능
			웹 브라우저 주소 표시줄에 사용자가 입력한 내용이 표시 됨 
		post 입력한 내용의 길이에 제한을 받지 않음 
			 웹 브라우저 주소 표시줄에 내용 표시 안 됨
	action	form 태그 안의 내용을 처리해 줄 서버 프로그램을 지정

<filedset>, <legend> 폼 요소를 그룹으로 묶음 
	<filedset><legend>그룹 이름</legend></filedset>
<label> 폼 요소에 레이블을 붙이는 태그 

<input> 사용자 입력을 위한 태그 

input 태그의 type 속성
                  
-------------------------
                  
텍스트와 비밀번호 type="text", type="password"
	size	화면에 보여지는 글자 제한 size="5" 
	value	텍스트필드 요소가 화면에 표시될 때 텍스트 필드에 보여주는 내용
	maxlength	최대 문자 수 지정

체크 박스와 라디오 type="checkbox", type="submit"
	value	선택한 체크 박스나 라디오 버튼을 서버에게 알려 줄 때
			넘겨줄 값을 지정, 필수 속성
	checked 기본으로 선택하는 항목에 사용, default 는 체크하지 않음

전송, 리셋 버튼 type="submit", type="reset"
	submit	폼에 입력한 정보를 
			form 태크의 action 속성에서 지정한 
			서버 프로그램으로 전송한다.
	reset	input 요소에 입력된 내용을 모두 지운다.
	value	버튼에 표시할 내용
	<input type="submit | reset" value="버튼에 표시할 내용">

이미지 버튼 type="image"
	<input type="image" src="이미지 경로" alt="대체 텍스트">

기본 버튼 type="button"
	button 타입을 submit 이나 reset 버튼 과 같은 기능은 없고 
	오직 버튼 형태만 삽입 된다.
	버튼을 클릭해서 자바스크립트를 실행할 때 사용한다.
	<input type="button" value="버튼에 표시할 내용">
	<input type="button" value="공지창열기" onclick="window.open('notice.html')">

파일을 첨부하는 type="file"
	폼에서 사진이나 문서를 첨부할 때 사용
	file 타입을 사용하면 웹 브라우저 화면에 파일선택, 찾아보기 버튼이 표시되면
	이 버튼을 클릭하고 파일을 선택하면 파일이 첨부 된다.

히든 필드 type="hidden"
	히든 필드는 화면의 폼에는 보이지 않지만
	사용자가 입력을 하면 폼과 함께 서버로 전송되는 요소이다.
	사용자에게 굳이 보여 줄 필요는 없지만
	관리자가 알아야 하는 정보는 히든 필드로 입력한다.
	<input type="hidden" name="이름" value="서버로 넘길 값">

input 태그의 주요 속성
                                                                         
--------------------------
                                                                         
autofocus 속성
	페이지 로딩시 폼에서 원하는 요소에 마우스 포인터를 표시

placehoder 속성
	사용자가 텍스트를 입력할 때 입력란에 적당한 힌트 내용을 표시 

readonly 속성
	사용자가 입력하지 못하게 하고 읽게만 하는 읽기 전용 필드 
	readonly
	readonly="true"

required 속성
	필수 입력 필드 
	내용을 폼에 입력 후 submit 할 때 필드 내용이 채워졌는지 체크 


폼에서 사용하는 태그 들 
                                                                         
---------------------------
                                                                         
<textarea> 태그 
	텍스트를 여러 줄 입력하는 태그 
	cols	가로 너비를 문자 단위로 지정
	rows	세로 길이를 줄 단위로 표시,
			지정한 숫자보다 줄 개수가 많으면 스크롤 생김

<select>, <option> 태그
	사용자가 내용을 직접 입력하지 않고 옵션 중에서 
	선택하게 하는 드롭다운 목록이나 데이터 목록
	옵션 태그 value 속성을 이용해 서버로 넘겨주는 값 지정 
select 속성
	size	화면에 표시할 드롭다운 항목의 개수 지정
	multiple 드롭다운 목록에서 둘 이상의 항목을 선개할 때 사용
option 속성
	value	해당 항목을 선택할 때 서버로 넘겨줄 값을 지정
	selected	드롭다운 메뉴를 삽입할 때 기본적으로 선택해서 보여 줄 항목 지정

<button> 태그 
	ipupt 태그의 button 타입과 같은 기능
	button 태그의 type 속성은 submit, reset, button이 있는데
	지정하지 않으면 submit 속성을 선택한 것으로 한다.
button 속성
submit	input type="submit" 같은 기능
reset	input type="reset" 같은 기능
button 	input type="button" 같은 기능
```

## HTML 실습

HTML 코드 실습과 결과를 마지막으로  이번 포스팅을 마치도록 하겠습니다.


> **HTML 실습 코드**

```html
<!DOCTYPE html>
<!-- DOCTYPE -->
<!-- 웹 문서의 유형 document type를 지정하는 선언문 -->
<!-- DOCTYPE로 html의 버전을 구별할 수 있다. -->

<html lang="ko">
<!-- html lang="ko" -->
<!-- html 웹 문서의 시작과 끝을 알리는 태그 -->
<!-- lang은 속성으로 문서에서 사용할 언어 지정-->
<!-- 검색 사이트에서 한국어로 제한해 검색 -->

<head>
<!-- head 
	웹 문서의 유형 document type을 지정하는 선언문
	웹 문서의 첫 부분에 작성한다.
-->

<meta charset="UTF-8">
<!-- meta 
메타 정보 : 데이터에 관한 데이터
웹 브라우저에 글자를 표시할 때 사용할 인코딩을 지정한다.
-->

<title>상품 소개 페이지</title>
<!-- title
문서 제목을 나타내는 태그로,  웹 브라우저 상단 바에 나타날 제목 기술-->

<!-- CSS : 선택자(selector)와 선언(declaration)으로 구성 -->
<!-- 선택자 : 웹페이지에 포함되어 있는 HTML 요소 -->
<!--  선언  : 선택자에 적용할 규칙으로서 하나의 규칙은 -->
<!--  콜론(:)으로 묶인 속성(property)와 값(value)의 쌍으로 표현 -->
<style>
	table, th, td{
		border:1px solid #ccc;
		border-collapse: collapse;
	}
	th,td{padding:10px 20px;}
	</style>
	<!-- property(속성) : border, 		 border-collapse, padding -->
	<!-- value(값) 	   : 1px solid #ccc, collapse, 		  10px 20px  -->
</head>


<body>
<!-- body
웹 브라우저에 내용을 표시하는 태그
문서 유형을 정의하고 문서 정보를 입력하면
<body></body> 사이에 실제 웹 브라우저에 표시할 내용을 입력한다.
 -->

	<img src="/firstWeb/images/link.png" alt="레드향">
	<!-- 이미지 경로를 상대경로로 불러온다. -->
	<!--  img : 이미지를 삽입하는 태그 -->

	<h1>레드향</h1>
	<!-- h1 : 제목을 나타내는 태그이다. -->

	<p>껍질에 붉은 빛이 돌아 <b>레드향</b>이라고 불린다.</p>
	<!-- p : 텍스트 단락 태그 -->

	<p>레드향은 <em>한라봉과 귤을 교배</em> 한 것으로 <br> 일반 귤보다 2~3배 크고, 과육이 붉고 통통하다.</p>
	<!-- em : 이탤릭체 강조 : emphasis -->
	<!-- br : 줄 바꾸는 태그 -->

	<p>비타민 C와 비타민 P가 풍부해<br> <strong>혈액순환, 감기예방</strong> 등에 좋은 것으로 알려져 있다.</p>
	<hr>
  <!-- <strong>, <b> 텍스트를 굵게 표시 -->
	<!-- hr : 줄 생성 -->
  <!-- strong : 경고나 주의사항등 중요내용 강조 -->

	<h2>레드향 샐러드 레시피</h2>
	<!-- h2 : 제목을 나타내는 태그 h1보다는 작은 글자 -->
	<p><b>재료 : </b>레드향 1개, 아보카도 1개, 토마토 1개, 샐러드 채소 30g</p>
	<!-- b : 단순히 글자만 굵게 표시 -->
	<p><b>드레싱 : </b>올리브유 1큰술, 레몬즙 2큰술, 꿀 1큰술, 소금 약간 </p>
	<ol>
	<!-- ol, li : 순서가 있는 목록 -->
		<li>샐서드 채소를 씻고 물기를 제거한 후 준비합니다.</li>
		<li>레드향과 아보카도, 토마토를 먹기 좋은 크기로 썰어둡니다.</li>
		<li>드레싱 재료를 믹서에 갈아줍니다.</li>
		<li>볼에 샐러드 채소와 썰어 둔 레드향, 아보카도, 토마토를 넣고 드레싱을 뿌리면 끝!</li>
	</ol>
	<img src="/firstWeb/images/salad.jpg" width="320">
	<hr>
	<h2>상품 구성</h2>
	<table>
	<!-- table :  표를 만드는 태그 -->
	<caption>선물용과 가정용상품 구성</caption>
	<!-- caption :  표의 제목 태그 -->
	<tr>
	<!-- tr : 행을 만드는 태그 -->
		<th>용도</th>
		<!-- th : 셀을 만드는 태그 -->
		<!-- th : 내용을 진하게 표시 -->
		<th>중량</th>
		<th>갯수</th>
		<th>가격</th>
	</tr>
	
  	<tr>
	<td>선물용</td>
	<!--  td : 셀을 만드는 태그 -->
	<td>3kg</td>
	<td>11~16과</td>
	<td>35,000원</td>
  	</tr>
  	
  	<tr>
	<td>선물용</td>
	<td>5kg</td>
	<td>18~26과</td>
	<td>52,000원</td>
	</tr>
	
	<tr>
	<td>가정용</td>
	<td>3kg</td>
	<td>11~16과</td>
	<td>30,000원</td>
 	</tr>
 	
 	<tr>
	<td>가정용</td>
	<td>5kg</td>
	<td>18~26과</td>
	<td>47,000원</td>
  	</tr>	
	</table>
</body>
</html>
```

> **실행 결과**

![](https://images.velog.io/images/yunyoseob/post/b8dae21f-ddd3-4d00-a58b-44f360b34c6a/image.png)

실행 결과 상품소개 페이지가 만들어 졌습니다. 주소는 다음과 같습니다.

```
현재 ip주소(혹은 localhost) + :포트번호 + / + Context docBase / + html / html파일이름.html
```

> **server.xml**

이클립스에서 Apache Tomcat 플러그인을 완료하고 server.xml 파일을 열어 Context docBase와 포트번호, path 등을 확인 할 수 있습니다.

```xml
<Connector connectionTimeout="숫자" port="포트번호" protocol="HTTP/X.X" redirectPort="숫자"/>

<Engine defaultHost="localhost" name="Catalina">
  
<Context docBase="컨텍스트" path="/시작경로" reloadable="true" source="org.eclipse.jst.jee.server:컨텍스트"/>
```

- 컨텍스트는 다른 말로, 프로젝트 혹은 웹 어플리케이션이라고도 부릅니다.
- 컨텍스트를 .war로 묶어서 관리합니다. (war : Web Application ARchive)

**✔ 만약, path를 바꾸면 URL을 바꾼 path에 맞게 수정해서 입력해야 하는데, 그렇지 않았는데도 불구하고, 정상적으로 나오는 경우가 있습니다.** 

**✔ 이럴 경우, 남아있는 쿠키를 제거하고 새로고침을 하면 정상적으로 출력되지 않습니다.**

**✔ 또한, path를 바꿨을 경우, Tomcat 서버를 다시 시작해야 합니다. 마지막으로 Tomcat 서버가 Stop이거나, 동시에 2개의 서버가 실행될 경우, 정상적으로 출력되지 않습니다.**


**이상으로 [HTML] HTML 기초 1편 포스팅을 마치도록 하겠습니다. 😃**
