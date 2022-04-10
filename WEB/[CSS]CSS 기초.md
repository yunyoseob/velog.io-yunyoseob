안녕하세요. 😊 오늘은 css 기초에 대해 포스팅해보도록 하겠습니다.

![](https://velog.velcdn.com/images/yunyoseob/post/3bb43c80-279c-4202-b1b7-f295db075749/image.png)

## 들어가기 전에

> **CSS(Cascading Style Sheets)**

![](https://velog.velcdn.com/images/yunyoseob/post/8d267904-feb6-460a-80fd-7154d7d4e798/image.gif)

- 출처 : [vanilla coding (css의 역할 포스팅)](https://book.vanillacoding.co/starter-kit/step-1/html-css/css) 

이제까지는 HTML으로 웹문서의 구조를 만들고 내용을 채워넣었다면, CSS는 웹문서에 색깔을 입히고, 크기를 조정하는 등의 작업을 할 수 있게 해줍니다.

## CSS : 글자 크기, 색깔, 폰트 조정하기

> **velogCsshtml.html**

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<p>Hi~ Velog!!</p>
</body>
</html>
```

> **결과 화면**

![](https://velog.velcdn.com/images/yunyoseob/post/e9608d7e-86fe-4083-8e8a-f4279906387d/image.png)


예시로 다음과 같은 html 문서가 있다고 할 때, p태그 안에서 글자 크기, 색깔, 폰트를 조정할 수 있습니다.


> **velogCsshtml.html**

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<center>
	<p style="font-size:140px; font-family:Verdana; color:#20C997;">Hi~ Velog!!</p>
	</center>
</body>
</html>
```

다음과 같이 font-size로 글자의 size를 조정하고, font-family를 Verdana로 조정하여 글자의 폰트를 바꾸고 color를 #20C997로 바꾼 다음 이미지를 가져와 붙일 수도 있습니다.

> **결과 화면**

![](https://velog.velcdn.com/images/yunyoseob/post/09ae77c1-7076-41d3-bac3-0e1fbe1001c9/image.png)


## **font-size, font-family, color 설명**

[w3schools.com](https://www.w3schools.com/)에 들어가서, font-size를 검색합니다.

그 다음, [CSS font-size Property](https://www.w3schools.com/cssref/pr_font_font-size.asp)를 클릭합니다. Example을 읽어본 뒤에, Definition and Usage에 Show demo를 클릭합니다. 

![](https://velog.velcdn.com/images/yunyoseob/post/e392ac9b-e201-49a7-8c52-05dfceb74afd/image.png)

데모파일을 보고 사용법을 익힌 후, 본인이 사용하고 싶은 대로 사용하면 됩니다.


font-family Property도 마찬가지로 [CSS font-family Property](https://www.w3schools.com/cssref/pr_font_font-family.asp)에 들어가서, demo를 보신 후, 선택하면 됩니다.

![](https://velog.velcdn.com/images/yunyoseob/post/70012e91-bfa0-4b33-85a4-bcefc5838b95/image.png)

텍스트의 컬러를 수정하고 싶을 경우, color: 바꿀 값을 입력하면 됩니다. w3 School에서 색까을 고르는 두 가지 방법을 설명해드리도록 하겠습니다. 

> **Color 고르기**

첫 번째는 [HTML Color Picker](https://www.w3schools.com/colors/colors_picker.asp)에서 고르는 방법입니다. 

예시로 초록색을 찾고 싶다하면 green을 입력하고, 내가 사용하고 싶은 색깔을 Hex, Rgb, Hsl에서 보고 고르면 됩니다.

![](https://velog.velcdn.com/images/yunyoseob/post/aac79bbd-2626-44ad-95dc-bea91790e1ee/image.png)

두 번째 방식은 [CSS Colors](https://www.w3schools.com/cssref/css_colors.asp)를 가서 색깔을 보고 마음에 드는 것을 고르는 방식 입니다.

![](https://velog.velcdn.com/images/yunyoseob/post/dd1895b9-1fa1-4b99-a53f-651a33c34e1a/image.png)


## head에서 p태그 일괄 적용하기

html 문서에서 p태그가 3개라고 할 때, 3개 태그에 동시에 css를 적용할 수도 있습니다.

> **velogCsshtml.html**

```css
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style type="text/css">
	p{
		font-size:40px;
		font-family:Verdana;
		color:#20C997;
	}

</style>
</head>
<body>
	<center>
	<p>Hi~ Velog!!</p>
	<p>WEB 포스팅 :: </p>
	<p>CSS 포스팅</p>
	</center>
</body>
</html>
```

> **결과 화면**

![](https://velog.velcdn.com/images/yunyoseob/post/7d24094d-4984-454a-b34f-d86b17644f18/image.png)

**🤔 만약, p태그중에서 CSS 포스팅이라는 내용이 있는 p태그만 빨간색으로 바꾸고 싶다면??**

두 가지 방법이 있습니다. 첫 번째 방법은  &lt;CSS 포스팅&gt;안에 p태그만 색깔을 다르게 하는 방식입니다.

```css
<!-- 앞뒤 생략 -->
	<p style="color:red;">CSS 포스팅</p>
```

두 번째 방식은 해당 p태그에 아이디 혹은 class를 부여한뒤 따로 설정해주는 방법입니다.

```css
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style type="text/css">
	p{
		font-size:40px;
		font-family:Verdana;
		color:#20C997;
	}

	#cssposting{
		color:red;
	}
</style>
</head>
<body>
	<center>
	<p>Hi~ Velog!!</p>
	<p>WEB 포스팅 :: </p>
	<p id=cssposting>CSS 포스팅</p>
	</center>
</body>
</html>
```

p태그 안에 class=클래스명일 경우 header안에 style 태그 사이에 클래스 선택자를 적용하여 .cssposting으로, id=아이디명일 경우 header 안에 style태그 사이에 id 선택자를 적용하여 #cssposting으로 하시면 됩니다.

> **결과 화면**

![](https://velog.velcdn.com/images/yunyoseob/post/1d224b01-7606-4f05-9a06-18df30adb363/image.png)


## CSS 박스 모델 요소 box model element

![](https://velog.velcdn.com/images/yunyoseob/post/9f64d203-8363-4ff8-901d-9531da79a8eb/image.png)

css에는 여백, 테두리, 패딩, 콘첸츠의 박스 모델 요소가 있습니다. 여백(margin)은 박스의 맨 바깥 영역으로, 테두리 바깥 공간으로 아래 위 인접한 태그와 만나는 공간을 의미합니다.

> **margin 적용전과 후 비교해보기**

```css
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style type="text/css">
	body{
		background-color:black;
	}
	
	div{
		font-size:40px;
		font-family:Verdana;
		color:#20C997;
		background-color:white;
		text-align:center;
		border-style:dotted;
		border-color:red;
	}

	.cssposting{
		color:red;
	}
</style>
</head>
<body>
	<div class="csspractice">
	<p>Hi~ Velog!!</p>
	<p>WEB 포스팅 :: </p>
	<p class=cssposting>CSS 포스팅</p>
	</div>
</body>
</html>
```

margin에 대해 설정값을 따로 주지 않고, border에 색깔을 빨간색 점선으로만 표기 하였고, div 밖의 body부분은 검정색으로 채운 뒤, margin에 변화를 주었을 때 어떤 변화가 있는지를 비교하여 보도록 하겠습니다. 

> **margin에 변화주기 전**

![](https://velog.velcdn.com/images/yunyoseob/post/b66073eb-f9a0-47f8-a181-fc58a2e4dd73/image.png)

![](https://velog.velcdn.com/images/yunyoseob/post/7f5a6d5f-3063-4ee9-b4d8-4c9ead22f538/image.png)



> **margin에 100px 적용한 이후**

```css
/* 앞 뒤 생략  div{} 사이 margin 추가*/
margin:100px;
```


![](https://velog.velcdn.com/images/yunyoseob/post/59df91f7-01cd-46d7-a158-50021341a8e2/image.png)

![](https://velog.velcdn.com/images/yunyoseob/post/430990cd-a5f0-4d84-8ed1-d9005b2bfabd/image.png)

마진이 100px 적용 됐을 때, 박스모델에 변화가 생긴 것을 볼 수 있습니다.

> **margin에 상하좌우 다 다르게 계산하여 넣어주기**

```css
/* 앞 뒤 생략  div{} 사이 margin 추가*/
margin:100px 50px 40px 20px;
```

> **margin에 100px 50px 40px 20px을 적용한 이후**

![](https://velog.velcdn.com/images/yunyoseob/post/24f38af1-7cd8-42a5-b251-2f301b2c3b0e/image.png)

![](https://velog.velcdn.com/images/yunyoseob/post/9b4bc8dc-df3d-45c6-9a6a-5b5cbe691db1/image.png)

미세하게 오른쪽과 왼쪽의 여백이 다른 것을 확인 할 수 있습니다. margin의 경우, 위에서부터 시계방향으로 정할 수 있으며, 같을 경우 생략이 가능합니다.

## css 외부에서 적용하여 활용하기

> **css 외부에서 적용하기 전**

```css
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<div class="csspractice">
	<p>Hi~ Velog!!</p>
	<p>WEB 포스팅 :: </p>
	<p class=cssposting>CSS 포스팅</p>
	</div>
</body>
</html>
```

> **결과 화면**

![](https://velog.velcdn.com/images/yunyoseob/post/201a66a1-d9a7-46a6-aa48-69ea9d996d98/image.png)


> **velog.css**

```css
@charset "UTF-8";

body{
		background-color:black;
	}
	
	div{
		font-size:40px;
		font-family:Verdana;
		color:#20C997;
		background-color:white;
		text-align:center;
		border-style:dotted;
		border-color:red;
		margin:100px;
	}

	.cssposting{
		color:red;
	}
```

해당 css 파일을 &lt; link rel="stylesheet" href="css파일 경로" &gt; 으로 불러올 수 있습니다.

> **velogCsshtml.html**

```css
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<link rel="stylesheet" href="css파일 경로">
<title>Insert title here</title>
</head>
<body>
	<div class="csspractice">
	<p>Hi~ Velog!!</p>
	<p>WEB 포스팅 :: </p>
	<p class=cssposting>CSS 포스팅</p>
	</div>
</body>
</html>
```

> **결과 화면**

![](https://velog.velcdn.com/images/yunyoseob/post/5a91b8e2-ebab-4775-936c-dbc2de8349e9/image.png)


**이상으로 CSS 기초 포스팅을 마치도록 하겠습니다. 😃**
