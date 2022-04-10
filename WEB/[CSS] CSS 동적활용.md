안녕하세요. 😁 오늘은 CSS 동적활용에 대해 포스팅해보도록 하겠습니다.

![](https://velog.velcdn.com/images/yunyoseob/post/3b1eb944-5506-4b6c-b08d-3bc8ff0949ea/image.png)

## 클릭 이벤트로 상자 색깔 바꾸기

> **velogCsshtml.html**

```css
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<script  src="http://code.jquery.com/jquery-latest.min.js"></script>
<title>Insert title here</title>
<script type="text/javascript">
	$(document).ready(function(){
		$("#box1").click(function(){
			$("#box1").css({"background-color":"red"});
		});
		
		$("#box2").click(function(){
			$("#box2").css({"background-color":"blue"});
		});
	});

</script>
<style type="text/css">
	div{
		width:300px;
		height:200px;
		margin:50px;
		border-color: black;
    	border-style: solid;
	}
	
	#box1{
		background-color:yellow;
		
	}
	
	#box2{
		background-color:green;
	}
</style>

</head>
<body>
	<div id="box1"></div>
	<div id="box2"></div>
</body>
</html>
```

첫 화면 결과는 다음과 같습니다.

> **화면 결과**

![](https://velog.velcdn.com/images/yunyoseob/post/02333d2c-946c-4d69-8c77-92764314c852/image.png)


이 때, jQuery안의 코드로 인해 각 상자를 클릭할 경우, 색깔이 변하게 됩니다.

```javascript
// 앞 뒤 생략..
$(document).ready(function(){
		$("#box1").click(function(){
			$("#box1").css({"background-color":"red"});
		});
		
		$("#box2").click(function(){
			$("#box2").css({"background-color":"blue"});
		});
	});
```

> **각 상자 클릭 후**

![](https://velog.velcdn.com/images/yunyoseob/post/8f121d0d-a101-40bc-b4c6-e119c5e0cea4/image.png)

이처럼, 특정 이벤트가 일어났을 때, 주소를 변경하지 않아도, 색깔을 변경할 수 있습니다.

## 클릭 이벤트로 이미지 바꾸기

> **velogCsshtml.html**

```css
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<script  src="http://code.jquery.com/jquery-latest.min.js"></script>
<title>Insert title here</title>
<script type="text/javascript">
	$(document).ready(function(){
		$(".btn1").click(function(){
			$(".frame img").attr({
				"src":"바꿀 이미지 경로"
			});
		});
	});

</script>
<style type="text/css">
	.frame{
		width:320px;
		border: 2px solid red;
		margin: 10px auto;
	}
	.frame img{width:100%}
</style>

</head>
<body>
	<div>
		<center>
		<button class="btn1" >이미지 속성 변경하기1</buton>
		</center>
	</div>
	<p class="frame">
		<img src="이미지 경로" alt="이미지가 안 떠요 ㅠㅠ">
	</p>
</body>
</html>
```

첫 화면 결과는 다음과 같습니다.

> **화면 결과**

![](https://velog.velcdn.com/images/yunyoseob/post/daa886c3-0617-4363-9d79-20df186996e2/image.png)


> **이미지 속성 변경하기1 클릭 후**

![](https://velog.velcdn.com/images/yunyoseob/post/87507bad-bbf3-440f-9bb7-3d5c095889c5/image.png)

## innerHTML 활용하기

> **velogCsshtml.html**

```css
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<script  src="http://code.jquery.com/jquery-latest.min.js"></script>
<title>Insert title here</title>
<script type="text/javascript">
function change() {
    var p = document.getElementById("firstP");
    // innerHTML : XHTML 에서 사용하던 프로퍼티 
    p.innerHTML= "나의 <img src='이미지경로'> 강아지";
}

</script>
</head>
<body>
	<center>
	<h3>innerHTML 활용 : 아래 글자에 클릭하면 예쁜 강아지가 보입니다.</h3>
	<p id="firstP" style="color:blue" onclick="change()">
	    여기에 <span style="color:red">클릭하세요</span>
	 </center>
</p>
</body>
</html>
```

첫 화면 결과는 다음과 같습니다.

> **화면 결과**

![](https://velog.velcdn.com/images/yunyoseob/post/a2a20f25-f1d7-4f13-9c55-74d2ec390e84/image.png)

> **클릭하세요를 클릭한 이후**

p태그 속성이 나의 + 이미지 + 강아지로 바뀝니다.

![](https://velog.velcdn.com/images/yunyoseob/post/27c21be7-41b7-4eaa-9d42-130e78df75b2/image.png)

## 객체를 동적으로 생성, 삽입, 삭제하기

> **velogCsshtml.html**

```css
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<script  src="http://code.jquery.com/jquery-latest.min.js"></script>
<title>Insert title here</title>
<script type="text/javascript">
function createDIV() {

    var obj = document.getElementById("parent");

    var newDIV = document.createElement("div");

    newDIV.innerHTML = "새로 생성된 DIV입니다.";
    newDIV.setAttribute("id", "myDiv");
    newDIV.style.backgroundColor = "yellow";

    newDIV.onclick = function() {
        var p = this.parentElement; // 부모 HTML 태그 요소
        p.removeChild(this); // 자신을 부모로부터 제거
    };

    obj.appendChild(newDIV);
}

</script>
</head>
<body id="parent">
	<h3>DIV 객체를 동적으로 생성, 삽입, 삭제하는 예제</h3>
	<hr>

	<p>    
    	DOM 트리에 동적으로 객체를 삽입할 수 있습니다.<br>
    	createElement(), appendChild(),removeChild() 메소드를<br>
    	이용하여 새로운 객체를 생성, 삽입, 삭제하는 예제입니다.<br>
	</p>
	<a href="javascript:createDIV()">DIV 생성</a><p>
<p>

</p>
</body>
</html>
```

1. DIV 생성이라는 링크를 클릭하는 순간, JavaScript의 createDIV함수로 들어가게 됩니다.

2. 이후, body태그의 id인 parent가 obj 변수로 지정이 되고, 새로운 div가 생성된 뒤, innerHTML로 "새로 생성된 DIV입니다"가 표기 됩니다.

3. 이 때, 생성된 DIV의 id는 myDiv이며, 배경색은 yellow입니다. 해당 객체를 obj(body 태그)에 추가합니다.

4. 새로 생성된 DIV입니다를 클릭하는 순간, 해당 div객체의 부모 객체인 body로 부터 div가 삭제 됩니다.

> **화면 결과**

![](https://velog.velcdn.com/images/yunyoseob/post/6b19e3a5-24fc-4d6d-938a-50cae4fb4b95/image.png)

> **DIV 생성하기 클릭 후**

![](https://velog.velcdn.com/images/yunyoseob/post/868a0e0f-7147-4bd4-8134-df1cda771d9d/image.png)

> **새로 생성된 DIV입니다. 클릭 후**

![](https://velog.velcdn.com/images/yunyoseob/post/6b19e3a5-24fc-4d6d-938a-50cae4fb4b95/image.png)

다시 원상복귀 되는 것을 확인 할 수 있습니다.

이처럼 HTML, CSS, JavaScript, jQuery 등을 이용하여, 다른 홈페이지로 이동하게 할 수도 있고, 해당 웹문서의 정보를 다른 웹문서로 전달할 수 있을 뿐만아니라, 해당 웹문서에서 자체적으로 이벤트를 줄 수 도 있습니다.

**이상으로 [CSS] CSS 동적활용 포스팅을 마치도록 하겠습니다. 😀**


