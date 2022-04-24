안녕하세요. 😀 오늘은 저번  [[XML] XML 활용 기초 2편](https://velog.io/@yunyoseob/XML-XML-%ED%99%9C%EC%9A%A9-%EA%B8%B0%EC%B4%88-2%ED%8E%B8) 포스팅에 이어서, XML 활용하는 기초 3편을 포스팅해보도록 하겠습니다.

오늘은 xml파일을 통해서 다른 Java 파일의 내용을 콘솔창에 출력하는 실습을 하도록 하겠습니다.

> **velog.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ROOT>
	<testclass>
		<test>a.b.c.test.xml_p.TestClass</test>
	</testclass>
</ROOT>
```

먼저, xml파일의 TEXT 태그에 출력하고자 하는 JAVA의 클래스의 Name Space(패키지+클래스이름)을 적어줍니다.

> **TestClass.java**

```java
package a.b.c.test.xml_p;
import org.apache.log4j.LogManager;
import org.apache.log4j.Logger;
import java.util.ArrayList;

public class TestClass {
	public void test(){
		// Logger logger = LogManager.getLogger(TestClass.class);
		System.out.println("a.b.c.test.xml.TestClass 클래스에 있는 test() 메소드 입니다.");
		System.out.println("Hello >>>>>>>>>> : ");
		
		ArrayList<String> aList=new ArrayList<String>();
		aList.add("벨로그");
		aList.add("웹");
		aList.add("포스팅");
		aList.add("입니다");
		
				
		for (int i=0; i<aList.size(); i++){
			System.out.println(" >>> : "+aList.get(i));
		}
		
	}
	public static void main(String args[]){
		TestClass tc= new TestClass();
		tc.test();
	}
}
```

출력시켜야 하는 내용은 다음과 같습니다.

```
벨로그
웹
포스팅
입니다
```

## XML Class 읽어올 Java 파일 만들기

> **ReadXMLClass.java**

```java
package a.b.c.test.xml_p;

import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.parsers.DocumentBuilder;
import org.w3c.dom.Document;
import org.w3c.dom.NodeList;
import org.w3c.dom.Node;
import org.w3c.dom.Element;
import java.io.File;
import org.apache.log4j.LogManager;
import org.apache.log4j.Logger;

public class ReadXMLClass {
	public static final String XML_FILE_PATH="xml 파일이 있는 패키지의 절대 경로";
	public static void main(String args[]){
		String testClass="";
		try {
			Logger logger = LogManager.getLogger(ReadXMLClass.class);
			// Tomcat 서버에서 웹 서버(코요태) 위치에 있는 velog.xml 파일을
			// Tomcat 서버가 설치된 로컬 경로에 있는 물리적 파일 위치를 찾아서
			// java.io.File 객체로 읽어 오는 것이다.
			// java.io.File 객체를 물리적 경로를 읽는 객체이다.
			String xmlFilePath=ReadXMLClass.XML_FILE_PATH;
			logger.info("xmlFilePath >>> : "+xmlFilePath);
			 
			File fXmlFile=new File(xmlFilePath+"/velog.xml");
			logger.info("fXmlFile >>> : "+fXmlFile);
			
			// 팩토리 디자인 패턴: 형식: xml파일을 읽어서 파싱
			// 물리적인 xml 파일을 xml 객체로 변환하기 위해서 팩토리 디자인 패턴을 이용한다.
			DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
			
			logger.info("dbFactory >>> : "+dbFactory);		
			DocumentBuilder dBuilder=dbFactory.newDocumentBuilder();
			
			logger.info("dBuilder >>> : "+dBuilder);
			
			// parse() 함수가 물리적인 xml 파일을 파싱해서 메모리에 xml 객체로 변환시킨다.
			Document doc=dBuilder.parse(fXmlFile);
			
			logger.info("doc >> : "+doc);
			
			// xml 문서를 깨끗하게 만드세요
			doc.getDocumentElement().normalize();
			logger.info("doc >>> : "+doc);
			
			logger.info("Root element : "+doc.getDocumentElement().getNodeName());
            
			NodeList nList=doc.getElementsByTagName("testclass");
			logger.info("nList >>> : "+nList);
			System.out.println("--------------------");
			
			logger.info("nList.getLenth() >>> : "+nList.getLength());
			
			for(int temp=0; temp<nList.getLength(); temp++){
				 
				Node nNode=nList.item(temp);
                
				if(nNode.getNodeType()==Node.ELEMENT_NODE) {				
					Element eElement = (Element) nNode;

					testClass = getTagValue("test", eElement);
					System.out.println("test : "+testClass);
					// test : a.b.c.test.xml_p.TestClass
				}
			}
			
			try {
				Class cla_1=Class.forName(testClass);
				logger.info("Class cla_1 >>> : "+cla_1);
				
				TestClass classAction=(TestClass)cla_1.newInstance();

				
				System.out.println("classAction >>> : "+classAction);
				// classAction >>> : a.b.c.test.xml_p.TestClass@37f8bb67
				classAction.test();
				// a.b.c.test.xml_p.TestClass에 있는 test 함수안의 내용이 출력된다.
			}catch(Exception e){
				System.out.println("error >>> : "+e.getMessage());
			}
			
			// catch(ClassNotFoundException e){}
			// catch(InstantiationException i){}
			// catch(IllegalAccessException i1){}
			
		}catch(Exception e){
			System.out.println(e);
		}
	} // end of main
	
	private static String getTagValue(String sTag, Element eElement){
		Logger logger = LogManager.getLogger(ReadXMLClass.class);
		logger.info("getTagValue 함수 진입 >>> : ");
		logger.info("String sTag >> : "+sTag);
		logger.info("Element eElement >>> : "+eElement);

		NodeList n1List=eElement.getElementsByTagName(sTag).item(0).getChildNodes();
		logger.info("n1List >>> : "+n1List);

		Node nValue=(Node) n1List.item(0);
		logger.info("nValue >>> : "+nValue);

		return nValue.getNodeValue();
	}
} // end of ReadXMLClass
```

## ReadXMLClass.java 코드 해설

> **1. xml 파일 경로 설정하기**

```java
public static final String XML_FILE_PATH="xml 파일이 있는 패키지의 절대 경로";
	public static void main(String args[]){
		String testClass="";
		try {
			Logger logger = LogManager.getLogger(ReadXMLClass.class);
			// Tomcat 서버에서 웹 서버(코요태) 위치에 있는 velog.xml 파일을
			// Tomcat 서버가 설치된 로컬 경로에 있는 물리적 파일 위치를 찾아서
			// java.io.File 객체로 읽어 오는 것이다.
			// java.io.File 객체를 물리적 경로를 읽는 객체이다.
			String xmlFilePath=ReadXMLClass.XML_FILE_PATH;
			logger.info("xmlFilePath >>> : "+xmlFilePath);
			 
			File fXmlFile=new File(xmlFilePath+"/velog.xml");
			logger.info("fXmlFile >>> : "+fXmlFile);
```  

먼저, xml 파일이 있는 패키지의 절대 경로를 상수로 지정합니다. 이후, File 클래스의 참조변수 선언 시, xml의 절대경로+velog.xml을 넣어 File 클래스에 생성자를 생성합니다.

> **2. jdk에서 지원하는 Parser : org.w3c.dom.**

```java
DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
			
logger.info("dbFactory >>> : "+dbFactory);		
DocumentBuilder dBuilder=dbFactory.newDocumentBuilder();
			
logger.info("dBuilder >>> : "+dBuilder);
			
// parse() 함수가 물리적인 xml 파일을 파싱해서 메모리에 xml 객체로 변환시킨다.
Document doc=dBuilder.parse(fXmlFile);
```


- jdk에서는 org.w3c.dom 패키지에 있는 클래스들로 xml 문서 전체를 한 번에 읽어서 동작할 수 있습니다.


[Java™ Platform Standard Ed. 8](https://docs.oracle.com/javase/8/docs/api/)에서 javax.xml.parsers 패키지에 있는 DocumentBuilderFactory 클래스는 추상 클래스(abstract class)입니다.

따라서, 해당 클래스에 newInstance() 함수를 통해 인스턴스합니다. 그 다음, newDocumentBuilder() 함수를 통해 DocumentBuilder 클래스에 참조변수로 선언 합니다.

마지막으로, DocumentBuilder 클래스에 parse 함수를 사용하여, xml파일의 절대 경로+xml파일을 parse 함수의 인수로 넣은 뒤, Document 클래스의 참조변수로 선언합니다.


- Document 클래스는 org.w3c.dom 패키지에 있으므로, 이제 xml 문서 전체를 한 번에 읽어서 동작할 수 있습니다.

> **3. org.w3c.dom. 자원을 사용하여 Element 참조변수 만들기**

```java
NodeList nList=doc.getElementsByTagName("testclass");
logger.info("nList >>> : "+nList);
System.out.println("--------------------");
			
logger.info("nList.getLenth() >>> : "+nList.getLength());
			
for(int temp=0; temp<nList.getLength(); temp++){
				 
	Node nNode=nList.item(temp);
                
	if(nNode.getNodeType()==Node.ELEMENT_NODE) {				
		Element eElement = (Element) nNode;

		testClass = getTagValue("test", eElement);
		System.out.println("test : "+testClass);
		// test : a.b.c.test.xml_p.TestClass

```

- velog.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ROOT>
	<testclass>
		<test>a.b.c.test.xml_p.TestClass</test>
	</testclass>
</ROOT>
```

해당 xml 파일에서 testclass 태그를 찾아 NodeList 클래스의 참조변수로 선언합니다.

그 다음, 해당 NodeList 클래스의 getLength() 함수를 통해 목록에 있는 노드 수만큼 반복시킵니다.

그 이후, Collection에 있는 indexth item을 Node 클래스의 참조변수로 선언 한 뒤, 이를 Element 클래스의 참조변수로 지정합니다.

이렇게 만들어진, eElement와 test 태그를 getTagValue 함수에 인수로 입력하여 testClass String 변수에 대입합니다.

> **4. getTagValue 함수에서 Node 클래스의 getNodeValue 함수로 노드값 리턴시키기**

```java
private static String getTagValue(String sTag, Element eElement){
		Logger logger = LogManager.getLogger(ReadXMLClass.class);
		logger.info("getTagValue 함수 진입 >>> : ");
		logger.info("String sTag >> : "+sTag);
		logger.info("Element eElement >>> : "+eElement);

		NodeList n1List=eElement.getElementsByTagName(sTag).item(0).getChildNodes();
		logger.info("n1List >>> : "+n1List);

		Node nValue=(Node) n1List.item(0);
		logger.info("nValue >>> : "+nValue);

		return nValue.getNodeValue();
```        

이제 getTagValue의 매개변수들에 값을 입력받아, 매개변수의 tag 이름(test)를 입력한 후, collection의 indexth item을 Node로 리턴시킨 후, Node클래스의 getChildNodes() 함수를 통해 이를 NodeList클래스의 참조변수 n1List로 대입시킵니다.

그렇게 만들어진 n1List에 item함수를 사용하여, Node 클래스의 참조변수로 대입합니다.

```
nValue >>> : [#text: a.b.c.test.xml_p.TestClass]
```

그렇게 Node 클래스의 참조변수는 text 태그에 a.b.c.test.xml_p.TestClass가 입력된 것을 확인 할 수 있습니다.

마지막으로 nValue에 Node클래스의 getNodeValue() 함수를 써서 노드의 값을 리턴시킵니다.

> **5. Class.forName으로 TestClass 클래스를 찾아 안에 있는 내용 출력시키기**

```java
Class cla_1=Class.forName(testClass);
logger.info("Class cla_1 >>> : "+cla_1);
				
TestClass classAction=(TestClass)cla_1.newInstance();

				
System.out.println("classAction >>> : "+classAction);
// classAction >>> : a.b.c.test.xml_p.TestClass@37f8bb67
classAction.test();
// a.b.c.test.xml_p.TestClass에 있는 test 함수안의 내용이 출력된다.
```                
4번에서 nValue에 Node클래스의 getNodeValue() 함수를 써서 노드의 값을 리턴시킨 값은 

```
System.out.println("test : "+testClass);
test : a.b.c.test.xml_p.TestClass
```

찾고자 하는 a.b.c.test.xml_p.TestClass가 나왔습니다.

이제, Class.forName으로 TestClass를 찾아 Class 클래스의 참조변수로 지정한 뒤, Class 클래스의 newInstance() 함수를 통해 TestClass 클래스에 참조변수를 만들고, TestClass에 있는 test 함수를 호출합니다.

> **6. TestClass 클래스와 콘솔창 최종 결과**

**✔ TestClass.java**

```java
package a.b.c.test.xml_p;
import org.apache.log4j.LogManager;
import org.apache.log4j.Logger;
import java.util.ArrayList;

public class TestClass {
	public void test(){
		// Logger logger = LogManager.getLogger(TestClass.class);
		System.out.println("a.b.c.test.xml.TestClass 클래스에 있는 test() 메소드 입니다.");
		System.out.println("Hello >>>>>>>>>> : ");
		
		ArrayList<String> aList=new ArrayList<String>();
		aList.add("벨로그");
		aList.add("웹");
		aList.add("포스팅");
		aList.add("입니다");
		
				
		for (int i=0; i<aList.size(); i++){
			System.out.println(" >>> : "+aList.get(i));
		}
		
	}
	public static void main(String args[]){
		TestClass tc= new TestClass();
		tc.test();
	}
}
```

**💻 콘솔창 마지막 출력 결과**

```
a.b.c.test.xml.TestClass 클래스에 있는 test() 메소드 입니다.
Hello >>>>>>>>>> : 
 >>> : 벨로그
 >>> : 웹
 >>> : 포스팅
 >>> : 입니다
 ```
 
 xml에 있는 클래스의 name space를 통해 원하는 클래스의 내용을 ReadXMLClass 클래스에서 출력 시켰습니다.
 
 **✔ 이번 포스팅에서 다룬 내용을 응용한다면 xml에 원하는 클래스들을 전부 로드해놓고 해당 로직을 통해 원하는 클래스의 내용을 출력시킬 수 있을 것입니다.**
 
 이상으로 [XML] XML 활용 기초 3편 포스팅을 마치도록 하겠습니다. 🙂
