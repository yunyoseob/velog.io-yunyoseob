
![](https://velog.velcdn.com/images/yunyoseob/post/6388e61b-eab1-436e-aa56-b81dabfaecb3/image.png)

안녕하세요 🙂. 오늘은 저번 [[XML] XML 활용 기초](https://velog.io/@yunyoseob/XML-XML-%ED%99%9C%EC%9A%A9-%EA%B8%B0%EC%B4%88) 포스팅에 이어서, XML 활용하는 기초 2편을 포스팅해보도록 하겠습니다.

## XML 활용하여 EMP TABLE 내용 출력시키기

SQL을 한 번이라도 해보셨다면, EMP TABLE을 접해본 적 있으실겁니다. 😊

EMP 테이블은 직원들의 데이터가 담긴 테이블입니다.

EMP 테이블에 대한 정보는 [[Oracle DB] SQL 기초문법 1편](https://velog.io/@yunyoseob/Oracle-DB-SQL-%EA%B8%B0%EC%B4%88%EB%AC%B8%EB%B2%95-1%ED%8E%B8)에서 더 자세히 보실 수 있습니다.

> **EMP TABLE 데이터 보기**

![](https://velog.velcdn.com/images/yunyoseob/post/c4f62757-54a4-4a11-bf9f-9508479a8c60/image.png)

![](https://velog.velcdn.com/images/yunyoseob/post/38f8c6fd-995d-4a7e-b7db-3b9963d9ad05/image.png)

## 1번째 방법

첫 번째 방법은 html에서 입력한 테이블 이름을 입력받아 jsp파일에서 콘솔에 출력시키는 방법입니다.

> **text_xml_table.html**

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<form action="test_xml_table.jsp의 파일경로"
	method="GET">
<h3>테이블 이름을 입력하세요.</h3><br>
<hr>
<input type="text" class="tablename" name="tablename" id="tablename" />
<input type="submit" value="보내기" />
</form>
</body>
</html>
```

html파일에서 emp를 입력하면 jsp 파일에서 이를 받아옵니다.

> **text_xml_table.jsp**

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!--  java.io  패키지 클래스 가져오기 -->
<%@ page import="java.io.BufferedReader" %>
<%@ page import="java.io.InputStreamReader" %>
<!--  java.net 패키지 클래스 가져오기 -->
<%@ page import="java.net.URL" %>
<!--  log4j -->
<%@ page import="org.apache.log4j.LogManager" %>
<%@ page import="org.apache.log4j.Logger" %>
<!--  java src에서 클래스 import 해오기 -->
<%@ page import="a.b.c.test.xml_p.OracleXmlTest_1" %>
<%
	Logger logger=LogManager.getLogger(this.getClass());
	
	String tablename=request.getParameter("tablename");
	logger.info("2. tablename >>> : "+tablename);	
	//  2. tablename >>> : emp

	OracleXmlTest_1 oxt_1=new OracleXmlTest_1();
	boolean bool=oxt_1.makeXml(tablename);
	// 원하는 경로에 tablename.xml이 만들어지면, bool이 true로 리턴된다.
	
	logger.info("bool >>> : "+bool);
	// bool >>> : true
	
	if(!bool) return;
	
	String strHtml="";
	String strLine="";
	String xmlFilename= tablename+".xml";
	logger.info("xmlFilename >>> : "+xmlFilename);
	// xmlFilename >>> : emp.xml
	
	try{
		String strUrl="http://xml 파일 경로/"+xmlFilename;

		BufferedReader br = new BufferedReader(
				new InputStreamReader((new URL(strUrl))
				.openConnection().getInputStream(),"UTF-8"));
		
		while((strLine=br.readLine())!=null){
			strHtml+=strLine;
		}	
		logger.info("strHtml >>> : "+strHtml);
		// strHtml >>> : <?xml version='1.0'....<DEPTNO>10</DEPTNO></EMP>
		br.close();	
	}catch(Exception e){
		throw e;
	}
%>    
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>XML PARSING</title>
<!-- jQuery CDN 불러오기  -------------------------------------------->
<script  src="http://code.jquery.com/jquery-latest.min.js"></script>
<script type="text/javascript">
	$(document).ready(function(){
		var xmlText, xmlParser, xmlDoc;
		
		xmlText="<%= strHtml %>";
		// 위에 jsp에서 만들어진 strHtml을 xmlTest에 저장
		console.log("xmlText >>> : "+xmlText);
		//  <?xml version='1.0' encoding='euc-kr'?><EMP>...><DEPTNO>10</DEPTNO></EMP>
		
		xmlParser = new DOMParser();
		// 자바스크립트에서 DOMParser 객체를 인스턴스
		
		xmlDoc=xmlParser.parseFromString(xmlText, "text/xml");
		// 인스턴스된 DOMParser를 xml파일 형식으로 파싱
		console.log("xmlDoc >>> : "+xmlDoc);
		// xmlDoc >>> : [object XMLDocument]
		
		$("#parseText").click(function(){
			var nlist = xmlDoc.getElementsByTagName("EMPNO").length;
			for(i=0; i < nlist; i++){
    			empno = xmlDoc.getElementsByTagName("EMPNO")[i].childNodes[0].nodeValue;
    			ename = xmlDoc.getElementsByTagName("ENAME")[i].childNodes[0].nodeValue;
    			job = xmlDoc.getElementsByTagName("JOB")[i].childNodes[0].nodeValue;
    			mgr = xmlDoc.getElementsByTagName("MGR")[i].childNodes[0].nodeValue;
    			hiredate = xmlDoc.getElementsByTagName("HIREDATE")[i].childNodes[0].nodeValue;
    			sal = xmlDoc.getElementsByTagName("SAL")[i].childNodes[0].nodeValue;
    			comm = xmlDoc.getElementsByTagName("COMM")[i].childNodes[0].nodeValue;
    			deptno = xmlDoc.getElementsByTagName("DEPTNO")[i].childNodes[0].nodeValue;
    			
    			console.log(			empno 
    							+ "," + ename
    							+ "," + job
    							+ "," + mgr
    							+ "," + hiredate
    							+ "," + sal
    							+ "," + comm
    							+ "," + deptno);
    		}			
		});
		
		$("#parseFind").click(function(){
			var text=$(xmlDoc).find("ENAME").text();
			document.getElementById("text").innerHTML=text;
		});
	});
</script>
</head>
<body>
<h3>XML 데이터 파싱하기</h3>
<hr>
<button id="parseText">DOM Parser로 XML 파싱하기</button>
<button id="parseFind">find() 함수로 파싱하기</button>
<p id="text"></p>
</body>
</html>
```

###  **코드 설명**

코드가 길기 때문에, 핵심 내용만 설명하도록 하겠습니다. 😃

> **1. request.getParameter()**

```javascript
String tablename=request.getParameter("tablename");
```

html에서 입력한 emp를 jsp에서 tablename 변수에 담습니다.

> **2. OracleXmlTest_1 클래스 자원 활용하기**

```java 
    OracleXmlTest_1 oxt_1=new OracleXmlTest_1();
	boolean bool=oxt_1.makeXml(tablename);
```

html에서 작성한 테이블 이름 emp를 jsp의 tablename 변수로 받아온 뒤, 이를 OracleXmlTest_1 클래스의 makeXml의 매개변수에 인수로 입력합니다.


> **OracleXmlTest_1 클래스**

```java
package a.b.c.test.xml_p;

import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.SQLException;
import java.sql.Statement;
import org.apache.log4j.LogManager;
import org.apache.log4j.Logger;

public class OracleXmlTest_1 {
	public static final String XML_FILE_PATH="xml파일 디렉토리";
	public static final String XML_PROLOG="<?xml version='1.0' encoding='euc-kr'?>"; // 선언부
	// xml mime type을 상수로 지정합니다.

	public String getXml(final String tableName) throws Exception{
		Logger logger = LogManager.getLogger(OracleXmlTest_1.class);
		
		// 사용할 지역변수 초기화
		Connection con = null;			
		Statement stmt = null;
		ResultSet rsRs = null;
				
		ResultSetMetaData resultMeta = null;		
		int colCount = 0;		
		StringBuffer strBuffer = new StringBuffer(XML_PROLOG);		
		try{
			con = DBPropertyConn.getConnection();
			stmt = con.createStatement();
			rsRs = stmt.executeQuery("SELECT * FROM "+ tableName);	
			logger.info("10. 입력한 쿼리문 >>> \n"+"SELECT * FROM "+ tableName);
			// 10. 입력한 쿼리문 >>> 
			// SELECT * FROM emp
			
			resultMeta = rsRs.getMetaData();
			colCount = resultMeta.getColumnCount();
			
			System.out.println("11. "+tableName + " 테이블 컬럼 카운드 >>> : " + colCount);
			//  11. emp 테이블 컬럼 카운드 >>> : 8
			
			strBuffer.append("\n");	
			strBuffer.append("<" +  tableName.toUpperCase() + ">");	
			// <EMP>로 루트 태그를 생성해줍니다.
			strBuffer.append("\n");	
			
			while (rsRs.next()){
				for ( int i=0; i < colCount; i++){
					strBuffer.append("<"+resultMeta.getColumnName(i+1)+ ">");
					// < 칼럼이름 >
					strBuffer.append(rsRs.getString(i+1));
					strBuffer.append("</"+resultMeta.getColumnName(i+1)+ ">");
					strBuffer.append("\n");
				}	
			}		
			strBuffer.append("</" +  tableName.toUpperCase()  + ">");		
			// while문과 for문이 다 끝나고 나면 </EMP> 로 root 태그를 닫아줍니다.
			strBuffer.append("\n");				
		}catch(SQLException e) {
			System.out.println(" getXML() : "+e);
		}finally {}			
		
			return strBuffer.toString();
			// StringBuffer 클래스의 참조변수로 <EMP>....</EMP> 내용을 리턴해줍니다.
		}
	
	public static boolean xmlParse(String fileName, String xmlVal){
		Logger logger = LogManager.getLogger(OracleXmlTest_1.class);
		logger.info("13. xmlParse 함수 진입 :: fileName >>> : "+fileName+"xmlVal >>> : "+xmlVal);
		// 13. xmlParse 함수 진입 :: fileName >>> : empxmlVal >>> : <?xml version='1.0' encoding='euc-kr'?>
		// <EMP>
		// .....
		// </EMP>
		
		boolean bool = false;
		
		try {
			
			BufferedWriter bw = new BufferedWriter(
					new FileWriter(OracleXmlTest_1.XML_FILE_PATH + "/" + fileName.toLowerCase() + ".xml"));
			// kos_xml 파일 경로 + / + filname(emp)  + .xml
			// emp.xml을 지정된 파일경로에 쓰라는 로직
			
			
			bw.write(xmlVal);
			bw.flush();
			bw.close(); 
			
			bool = true;
		}catch(IOException e){
			System.err.println(e);
		}
		
		return bool;
	}
	
	public boolean makeXml(final String tableName) {
		Logger logger = LogManager.getLogger(OracleXmlTest_1.class);
		logger.info("3. makeXml 함수 시작 >>> : ");
		logger.info("makeXml으로 들어온 매개변수  >>> : "+tableName);
		// makeXml으로 들어온 매개변수  >>> : emp
		boolean bool = false;
		
		try{		
			
			if(tableName.length() > 0){	
				// tableName에 아무 값도 입력되지 않았으면, 수행되지 않는 로직입니다.
				
				final String fileName = tableName; 
				// 매개변수를 지역변수에서 다시 한 번 final로 세팅합니다.
				
				String xmlVal = getXml(fileName);
				// OracleXmlTest_1 클래스의 getXml 함수에 fileName을 인수로 다시 입력합니다.
				// getXml 함수 로직이 성공적으로 끝났으면 <EMP>...</EMP>
				// 내용을 String 클래스의 xmlVal 변수로 받아옵니다.
				
				System.out.println("12. Oralce String Data를 xml로 생성 >>> : \n" + xmlVal);
				// 받아온 내용을 출력시킵니다.
				// 12. Oralce String Data를 xml로 생성 >>> : 
				// <?xml version='1.0' encoding='euc-kr'?>
				// <EMP>
				// .....
				// </EMP>
				
				if (xmlVal !=null && xmlVal.length() > 0){
					// 받아온 xmlVal 변수가 null이거나 변수의 길이가 0이면 수행되지 않는 로직입니다.
					
					bool = OracleXmlTest_1.xmlParse(fileName, xmlVal);
					// 13. OracleXmlTest_1 클래스의 getXml 함수에 fileName과 xmlVal을 인수로 다시 입력합니다.
					// fileName : EMP
					// xmlVal : <EMP>....</EMP>
					
					if (bool){

						System.out.println("14. "+OracleXmlTest_1.XML_FILE_PATH +" 디렉토리에 " + fileName +".xml 파일이 잘 생성 되었습니다. ");
						// 파일을 다 쓰고 나면, bool이 true가 된다. 
						// 이 떄, if문으로 와서, 해당 경로에 파일이 잘 생성됨을  출력시켜준다.
					
					}else{
						System.out.println(" 파일이 생성 되지 않았습니다. ");
					}	
				}
			}else{	
				System.out.println("java OracleXmlTest 테이블이름 ");
			}				
		}catch(Exception e){
			System.out.println("e.getMessage() >>> : " + e.getMessage());
		}	
		
		// 로직이 잘 수행 되면, bool이 true로 리턴된다.
		return bool;
	}
} // end of OracleXmlTest_1
```

코드가 매우 길기 때문에, JAVA 파일에서도 핵심만 소개하면 다음과 같습니다.

> **2-1. makeXml 함수**

```java
public boolean makeXml(final String tableName)
```

makeXml로 emp를 입력받아옵니다. 테이블 이름이 입력되지 않으면, if문이 false이므로, if문이 수행되지 않습니다. getXml 함수로 넘어가서 결과값을 String xmlVal으로 받습니다.

> **2-2. getXml 함수**

```java
public static final String XML_PROLOG="<?xml version='1.0' encoding='euc-kr'?>"; // 선언부
StringBuffer strBuffer = new StringBuffer(XML_PROLOG);		
```

XML의 선언부를 StringBuffer 클래스에 strBuffer 참조변수에 추가해줍니다. (StringBuffer 클래스는 String 클래스와는 다르게 append 함수로 이어붙일 시 객체를 하나만 사용해서 계속 이어붙일 수 있습니다.

```java
con = DBPropertyConn.getConnection();
stmt = con.createStatement();
rsRs = stmt.executeQuery("SELECT * FROM "+ tableName);	
logger.info("10. 입력한 쿼리문 >>> \n"+"SELECT * FROM "+ tableName);
// 10. 입력한 쿼리문 >>> 
// SELECT * FROM emp
			
resultMeta = rsRs.getMetaData();
colCount = resultMeta.getColumnCount();
```          

DBPropertyConn 클래스에는 Oracle DB 관련 데이터들이 담겨 있는 클래스입니다. 해당 클래스로 가서 ojdbc를 통해 Oracle DB와 Java를 연결한 뒤, 쿼리문을 입력하여, 결과를 리턴해옵니다.

```java
strBuffer.append("\n");	
strBuffer.append("<" +  tableName.toUpperCase() + ">");	
// <EMP>로 루트 태그를 생성해줍니다.
strBuffer.append("\n");	
			
while (rsRs.next()){
for ( int i=0; i < colCount; i++){
	strBuffer.append("<"+resultMeta.getColumnName(i+1)+ ">");
	// < 칼럼이름 >
	strBuffer.append(rsRs.getString(i+1));
	strBuffer.append("</"+resultMeta.getColumnName(i+1)+ ">");
	strBuffer.append("\n");
	}	
}		
strBuffer.append("</" +  tableName.toUpperCase()  + ">");	
...
return strBuffer.toString();
```            

해당 로직을 통해 XML문서 내용을 작성하여 StringBuffer클래스의 참조변수에 저장한 뒤, 이를 String으로 클래스 형변환을 하여 리턴시킵니다.

> **2-3. xmlParse 함수 **

```java
BufferedWriter bw = new BufferedWriter(
					new FileWriter(OracleXmlTest_1.XML_FILE_PATH + "/" + fileName.toLowerCase() + ".xml"));
			
			
bw.write(xmlVal);
bw.flush();
bw.close(); 
			
bool = true;
```            

해당 로직은 해당 클래스의 xml파일 디렉토리에 파일이름을 소문자로 변환하여 .xml  파일로 작성하게 시키는 로직입니다. 해당 로직이 잘 수행된다면 이제 emp.xml  파일이 생성됩니다.

> **3. BufferedReader 활용하기**

다시, test_xml_table.jsp 파일로 돌아와서, OracleXmlTest_1 자바 클래스가 성공적으로 로직을 수행했으면, emp.xml이 있는 경로에서 파일을 불러와 읽습니다.

해당 내용은 BufferedReader의 참조변수의 readLine() 함수를 통해 읽은 뒤, strHtml저장하여 줍니다.

> **4. JavaScript에서 DOMParser() 활용하기**

```javascript
xmlParser = new DOMParser();
xmlDoc=xmlParser.parseFromString(xmlText, "text/xml")
```
 자바스크립트에서 DOMParser 객체를 인스턴스 한 뒤, 인스턴스된 DOMParser를 xml파일 형식으로 파싱합니다.
 
 > **5. 클릭이벤트로 원하는 결과 콘솔창 혹은 화면에 출력시키기**
 
 ```javascript
$("#parseText").click(function(){})
$("#parseFind").click(function(){})
```

이제, HTML에서 버튼을 클릭했을 시, 

```html
<button id="parseText">DOM Parser로 XML 파싱하기</button>
<button id="parseFind">find() 함수로 파싱하기</button>
```

DOM Parser로 XML 파싱하기를 클릭하면 콘솔창에 EMP 테이블의 데이터들을 출력시킬 수 있습니다. 한 편, find() 함수로 파싱하기를 클릭하면 사원의 이름만 화면으로 출력시킬 수 있습니다.

**😓 더 쉽게 할수는 없을까?**

## 2번째 방법

이번에는 javax.naming, java.sql, javax.sql 패키지에 있는 클래스들로 해당 로직을 더 단순하게 만들어보도록 하겠습니다. (이클립스 기준)

먼저, 이클립스에서 Servers 폴더에서 context.xml을 들어갑니다.

그 다음, Oracle DB와 관련된 코드를 추가하여 줍니다.

> **context.xml**

```xml
  <WatchedResource>WEB-INF/web.xml</WatchedResource>
   <WatchedResource>${catalina.base}/conf/web.xml</WatchedResource>
    
   <Resource 	auth="Container" 				 
				maxActive="100" 
				maxIdle="30" 
				maxWait="10000"  
				type="javax.sql.DataSource" 
				
				name="jdbc/jndi_SERVICE_NAME"
				driverClassName="oracle.jdbc.driver.OracleDriver"
				url="jdbc:oracle:thin:@127.0.0.1:PORT번호:SERVICE_NAME"
				username="계정이름" 
				password="비밀번호" />

```

```
C:\app\product\11.2.0\dbhome_1\NETWORK\ADMIN
```

name, url, username, password는 위의 경로에서 tnsnames.ora 파일을 참고하여 본인의 정보를 작성해줍니다. (SERVICE_NAME, PORT번호, 계정이름, 비밀번호를 차례로 입력해줍니다.)

> **xml_jndiTest.jsp**

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!--  JDBC 객체 import -->
<%@ page import="java.sql.Connection" %>
<%@ page import= "java.sql.PreparedStatement" %>
<%@ page import="java.sql.ResultSet" %>
<%@ page import="java.sql.SQLException" %>
<%@ page import="java.sql.DriverManager" %>
<%@ page import="javax.sql.DataSource" %>

<!-- JNDI 객체 import -->
<%@ page import="javax.naming.Context" %>
<%@ page import="javax.naming.InitialContext" %>
<%@ page import="javax.naming.NamingException" %>

<!--  log4j -->
<%@ page import="org.apache.log4j.LogManager" %>
<%@ page import="org.apache.log4j.Logger" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h3>
JNDI InitialContext <br>
JNDI : Java Naming and Directory Interface
</h3>
<hr>
<%
	Logger logger=LogManager.getLogger(this.getClass());
	Context initCtx=new InitialContext();

	logger.info("initCtx >>> : "+initCtx);
	out.println("initCtx >>> : "+initCtx+"<br>");

	// initCtx의 lookup 메서드를 이용해서 "java:comp/env"에 해당하는 객체를 찾아서  evnCtx에 삽입
	Context envCtx=(Context)initCtx.lookup("java:comp/env");
	
	logger.info("envCtx >>> : "+envCtx);
	out.println("envCtx >>> : "+envCtx+"<br>");
	
	// Look up our data source
	// envCtx의 lookup 메서드를 이용해서 "jdbc/Oracle11g_SERVICE_NAME에 해당하는 객체를 찾아서
	// ds에 삽입
	
	DataSource ds = (DataSource)envCtx.lookup("jdbc/jndi_SERVICE_NAME");
	// 다시 한번, lookup 함수를 써서 명명된 개체를 검색
	// Object로 리턴된 값을 클래스 다운 캐스팅을 통해 DataSource 클래스의 참조변수로 선언
	/*
	javax.sql.DataSource
	*/
	
	
	logger.info("ds >>> : "+ds);
	out.println("ds >>> : "+ds+"<br><hr>");
	
	// getConnection 메서드를 이용해서 커넥션 풀로 부터 커넥션 객체를 얻어내어 conn변수에 저장
	Connection conn=ds.getConnection();
	PreparedStatement stmt=conn.prepareStatement("SELECT * FROM EMP");
	ResultSet rsRs=stmt.executeQuery();
	
	while(rsRs.next()){
		out.println(rsRs.getString(1)+" ");
		out.println(rsRs.getString(2)+" ");
		out.println(rsRs.getString(3)+" ");
		out.println(rsRs.getString(4)+" ");
		out.println(rsRs.getString(5)+" ");
		out.println(rsRs.getString(6)+" ");
		out.println(rsRs.getString(7)+" ");
		out.println(rsRs.getString(8)+"<br>");	
	}
%>
</body>
</html>
```

### 화면 결과와 추가 설명

![](https://velog.velcdn.com/images/yunyoseob/post/d5e4a32c-edff-4e33-a1d6-be8600ccfad0/image.png)

> **javax.naming.Context 참조변수 선언**

```java
Context initCtx=new InitialContext();
```

- InitialContext를 [JAVA API](https://docs.oracle.com/javase/8/docs/api/)에서 찾아보면,  javax.naming.InitialContext 클래스는 public class InitialContext extends Object implements Context 인 것을 볼 수 있습니다. 

InitialContext클래스에 생성자를 생성한뒤, Context 클래스에 참조변수를 선언합니다.

> **java:comp/env 객체 찾아서 Context 참조변수에 삽입**

```java
Context envCtx=(Context)initCtx.lookup("java:comp/env");
```

lookup 함수는 리턴형이 Object이므로, 클래스 다운 캐스팅 연산자를 사용하여 줍니다.

> **DataSource**

```java
DataSource ds = (DataSource)envCtx.lookup("jdbc/jndi_SERVICE_NAME");
```

다시 한번, lookup 함수를 써서 명명된 개체를 검색 후, Object로 리턴된 값을 클래스 다운 캐스팅을 통해 DataSource 클래스의 참조변수로 선언합니다.

> **DB 연동 후, 쿼리문 입력한 뒤, 결과 출력**

```java
Connection conn=ds.getConnection();
PreparedStatement stmt=conn.prepareStatement("SELECT * FROM EMP");
ResultSet rsRs=stmt.executeQuery();
...
out.println(rsRs.getString()+"")
```

이제 DB에 연동한 뒤, 쿼리문을 작성하여 원하는 결과를 출력시킵니다.


이번 시간에는 xml파일을 이용하여 DB에 연동 후, 원하는 테이블의 정보를 검색하여 화면에 출력시키는 2가지 방법에 대해 포스팅하였습니다. 다음 시간에는 마지막으로 XML을 이용하여 java에서 다른 java 파일의 내용을 콘솔창에 출력시키는 것을 마지막으로 XML 포스팅을 마치도록 하겠습니다.
