안녕하세요 😀. 오늘은 jsp의 내장 객체로 파일을 보낸 뒤, 화면에 출력하는 방법에 대해 포스팅해보도록 하겠습니다.

### JSP 내장 객체

JSP의 내장객체는 다음과 같습니다.

|객체|javax|설명|
|---|---|--|
|request|javax.servlet.http.HttpServletRequest, javax.servlet.ServletReqeust|웹 브라우저의 요청 정보를 저장하고 있는 객체|
|response|javax.servlet.http.HttpServletResponse, javax.servlet.ServletResponse|웹 브라우저의 요청에 대한 응답 정보를 저장하고 있는 객체|
|out|javax.servlet.jsp.JspWriter|JSP페이지의 출력할 내용을 가지고 있는 출력 스트림 객체|
|session|javax.servlet.http.ServletContext|하나의 웹 브라우저 내에서 정보를 유지하기 위한 세션 정보를 저장하고 있는 객체|
|application|javax.servlet.ServletContext|웹 애플리케이션의 Context의 정보를 담고 있는 객체|
|pageContext|javax.servlet.jsp.PageContext|JSP페이지에 대한 정보를 저장하고 있는 객체|
|page|java.lang.Object|JSP 페이지를 구현한 자바 클래스 객체|			
|config|javax.servlet.ServletConfig|JSP 페이지에 대한 설정 정보를 담고 있는 객체|
|exception|java.lang.Throwable|JSP 페이지에서 예외가 발생한 경우 사용하는 객체|

## enctype : multipart/form-data

> **enctype**

```

application/x-www-form-urlencoded
	&으로 분리되고, "=" 기호로 값과 키를 연결하는 key-value tuple로 인코딩되는 값입니다. 
	영어 알파벳이 아닌 문자들은 percent encoded 으로 인코딩됩니다. 
	content type은 바이너리 데이터에 사용하기에는 적절치 않습니다. 
multipart/form-data
	파일이나 이미지를 서버로 전송할 때 주로 사용
  
text/plain
	공백 문자(space)는 “+” 기호로 변환,
	나머지 문자는 모두 인코딩되지 않음
```

jsp로 파일을 보낼 때는 POST방식으로, enctype은 multipart/form-data로 보냅니다.

> **예제로 보는 파일 보내기**

```html
<h3>FILE UPLOAD</h3>
<hr>
<form name="fileUploadForm"
	  action="/Context/velog/velog_file.jsp"
	  method="POST"
	  enctype="multipart/form-data">
이름1 : <input type="text" name="name"><br>
파일1 : <input type="file" name="fileName1"><br>
파일2 : <input type="file" name="fileName2"><br>	
<input type="submit" value="전송">  
</form>
```

- Context는 현재 컨텍스트(웹 프로젝트 이름 or Web Application or Domain or Project)의 이름을 의미합니다.

> **화면**

![](https://velog.velcdn.com/images/yunyoseob/post/12a64360-6e10-4e6b-bbca-2f2dcb347765/image.png)

> **🤔 .JSP에서는 어떻게 파일을 받아야 할까?**

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>  
    <%@ page import="com.oreilly.servlet.MultipartRequest" %>   
<%@ page import="com.oreilly.servlet.multipart.DefaultFileRenamePolicy" %>    
<%@ page import="java.io.File" %>         
<%@ page import="java.util.Enumeration" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<%
	String saveDirectory=pageContext.getServletContext().getRealPath("/upload/aaaa/");
	out.println("saveDirectory >>> : "+saveDirectory+"<br>");
	
	File saveDir=new File(saveDirectory);
	
	if(!saveDir.exists()){
		saveDir.mkdirs();
	}
	
	int maxPostsize=1024*1024*5;
	String encoding="UTF-8";
	String filename1="";
	String filename2="";
	

	try{		
		MultipartRequest mr=new MultipartRequest(request, 
				saveDirectory, maxPostsize, encoding, new DefaultFileRenamePolicy());
		out.println("mr 참조변수 가지고 서버에 업로드된 파일 정보. <br>");
		
		// name
		String name=mr.getParameter("name");
		out.println("name >>> : "+name+"<br>");
		
		// file
		Enumeration<String> files=mr.getFileNames();
		
		String file1=String.valueOf(files.nextElement());
		filename1=mr.getFilesystemName(file1);
		out.println("filename1 >>> : "+filename1+"<br>");
		
		String file2=String.valueOf(files.nextElement());
		filename2=mr.getFilesystemName(file2);
		out.println("filename2 >>> : "+filename2+"<br>");
		
		
	}catch(Exception e){
		System.out.println("에러가 >>> : "+e.getMessage());
	}
%>
<h3>File Upload Testing</h3>
<hr>
<table border="1">
<tr align="center">
	<td><%= filename1 %></td>
	<td><img src="/Context/upload/aaaa/<%= filename1 %>"></td>
</tr>
<tr>
	<td><%= filename2 %></td>
	<td><img src="/Context/upload/aaaa/<%= filename2 %>"></td>
</tr>
</table>
<body>
</body>
</html>
```

## 코드 풀이와 함께하는 JSP에서 파일 출력시키기

> **pageContext.getServletContext().getRealPath("path");**

[Servlet 3.1 - Apache Tomcat 8.0.53](https://tomcat.apache.org/tomcat-8.0-doc/servletapi/index.html)에서 javax.servlet.ServletConfig 인터페이스 클래스안에 getServletContext() 함수가 있습니다.

✔ Method Summary

```java
Modifier and Type | Method and Description

ServletContext	  |	getServletContext()	

Returns: Returns a reference to the ServletContext in which the caller is executing.
```

또한 getRealPath("path")의 경우, javax.servlet.ServletContext 인터페이스 클래스 안에 getRealPath(java.lang.String path)가 있습니다.

✔ Method Summary

```java
Modifier and Type | Method and Description

java.lang.String  |	getRealPath(java.lang.String path)

Returns: Returns a String containing the real path for a given virtual path. For example, the path "/index.html" returns the absolute file path on the server's filesystem would be served by a request for "http://host/contextPath/index.html", where contextPath is the context path of this ServletContext..
```

해당 함수들을 통해 ServletContext의 object를 리턴 시킨 뒤, 주어진 가상경로를 실제경로에 붙이는 작업을 한 뒤, String 데이터 타입에 saveDirectory 변수에 대입합니다.

> **new File(saveDirectory)**

```java
File(String pathname)
		Creates a new File instance by converting the given pathname 
		string into an abstract pathname.
```

주어진 경로로 새로운 파일을 생성합니다.

> **new MultipartRequest(parameters)**

```java
MultipartRequest(javax.servlet.http.HttpServletRequest request, java.lang.String saveDirectory, int maxPostSize, java.lang.String encoding, FileRenamePolicy policy)

          Constructs a new MultipartRequest to handle the specified request, saving any uploaded files to the given directory, and limiting the upload size to the specified length.
```

각 인수들을 매개변수에 대입하여, 주어진 경로로 파일을 업로드 합니다.

**🤔 왜 FileRenamePolicy policy 자리에 다른 클래스의 생성자를 입력 하나요??**

![](https://velog.velcdn.com/images/yunyoseob/post/5731b087-0328-4152-98e6-f97a6ec9e2ff/image.png)


[servlets.com](http://www.servlets.com/cos/javadoc/com/oreilly/servlet/multipart/FileRenamePolicy.html)의 api를 보면 FileRenamePolicy는 interface 클래스고, 이 클래스를 상속을 받은 클래스가 DefaultFileRenamePolicy입니다. 해당 인터페이스 클래스의 상속 받은 클래스에서 생성자를 인스턴스하였습니다.

```java
com.oreilly.servlet.multipart
Class DefaultFileRenamePolicy

public class DefaultFileRenamePolicy
extends java.lang.Object
implements FileRenamePolicy


Implements a renaming policy that adds increasing integers to the body of any file that collides. For example, if foo.gif is being uploaded and a file by the same name already exists, this logic will rename the upload foo1.gif. A second upload by the same name would be foo2.gif. Note that for safety the rename() method creates a zero-len
```

해당 클래스에 인스턴스하면, 같은 파일이 저장 될 경우, 뒤에 숫자가 추가로 붙습니다.

ex) velog.jpg, velog1.jsp, velog2.jsp....

> **String name=mr.getParameter("name");**

![](https://velog.velcdn.com/images/yunyoseob/post/15205e5c-20fc-45ab-a450-52f976eb0d92/image.png)

com.oreilly.servlet.MultipartRequest 클래스의 참조변수에서 파라미터의 이름을 Stirng name으로 저장합니다. 

![](https://velog.velcdn.com/images/yunyoseob/post/12a64360-6e10-4e6b-bbca-2f2dcb347765/image.png)

화면에서 이름1에 입력한 값이 저장됩니다.

- 주의 : request.getParameter와는 다릅니다.

> **Enumeration&lt;String&gt; files=mr.getFileNames();**

```
getFileNames
public java.util.Enumeration getFileNames()

Returns the names of all the uploaded files as an Enumeration of Strings. It returns an empty Enumeration if there are no file input fields on the form. Any file input field that's left empty will result in a FilePart with null contents. Each file name is the name specified by the form, not by the user.

Returns:
the names of all the uploaded files as an Enumeration of Strings.
```

업로드 된 파일의 이름을 Enumeration 인터페이스 클래스에 담습니다.

> **String file1=String.valueOf(files.nextElement());**


```
java.util.Enumeration<E>
		files.nextElement()
		
		Returns the next element of this enumeration 
		if this enumeration object has at least one more element to provide.
		
		Returns:
			the next element of this enumeration.
			
		java.lang.String
		String : valueOf(Object obj)
		Returns:
			the next element of this enumeration.
```

이제 Enumeration 인터페이스 클래스에 있는 file의 이름을 찾아 file1이라고 해줍니다.

> **filename1=mr.getFilesystemName(file1);**

```
java.lang.String : 
			
	getFilesystemName(java.lang.String name)
	    Returns the filesystem name of the specified file, 
	    or null if the file was not included in the upload.
```        

이제 여기까지 왔으면, filename1에 성공적으로 출력이 된다면, 파일이 잘 업로드가 되었다고 볼 수 있습니다. 


> **&lt;td>&lt;img src="/Context/upload/aaaa/&lt;%= filename1 %>">&lt;/td>**

이제 이미지가 업로된 것까지 전부 확인하였으면, 이미지 경로를 잡아 출력시켜 줍니다.

### 입력값과 결과값 확인해보기

> **입력값**

![](https://velog.velcdn.com/images/yunyoseob/post/c7e5ab29-c5b0-42ad-bcfb-c3013779e6a1/image.png)


> **결과값**

![](https://velog.velcdn.com/images/yunyoseob/post/387f528e-ba0a-40d6-ae10-64100118ca76/image.png)

**✔ saveDirectory 볼 때, 주의해야 할 사항**

```java
String saveDirectory=pageContext.getServletContext().getRealPath("/upload/aaaa/");
```

다음 코드에서 이클립스 내에서의 경로와 실제 이미지가 저장되는 경로가 다릅니다.

가장 많이 실수하는 점이 본인의 워크스페이스안에 있는 src 혹은 WebContent 안에서 실제 image의 경로가 존재한다고 생각하나, 그렇지 않습니다. 

예시로, 

```
C:\..workspace..\Context\WebContent\image\img_kakao\
```
해당 경로안에 있는 이미지를 전송하였다고 하면, 실제 업로드 되는 경로는 아래와 같습니다.


```
saveDirectory >>> : C:\..workspace..\Context\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\Context\upload\aaaa\
```

이상으로, [html, jsp, java] 파일 업로드 포스팅을 마치도록 하겠습니다.

