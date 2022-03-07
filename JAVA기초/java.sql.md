안녕하세요. 😀 오늘은 Oracle DB와 JAVA를 연결할 때 필요한, java.sql에 대해 알아보도록 하겠습니다.

필자는 현재 Oracle 11g 2 Release이며, JAVA의 경우 jdk 1.8.0_202를 사용하고 있습니다. 이 때, Oracle DB와 java를 연결할 때 필요한 파일은 ojdbc6.jar 파일입니다. 

해당 파일을 통해 Oracle DB와 java를 연동할 때, java.sql패키지에 있는 인터페이스 클래스와 클래스를 사용하는데, 오늘 알아볼 java.sql 패키지에 있는 클래스는 Connection, DriverManager, ResultSet, StateMent 클래스입니다. 

- [Java™ Platform Standard Ed. 8](https://docs.oracle.com/javase/8/docs/api/)에서 java.sql을 클릭 후, 해당 클래스에 대해 확인할 수 있습니다.


## Interface Connection

![](https://images.velog.io/images/yunyoseob/post/fb2f1396-ef70-4188-9dd3-1c4b6dfbd444/image.png)

Connection 클래스는 Interface 클래스입니다. Interface는 메서드의 구현부가 존재하지 않는 클래스를 의미합니다.

> **method**

![](https://images.velog.io/images/yunyoseob/post/4adbc85f-c38b-4bce-82e0-72d993084d2e/image.png)

createStatement 메서드는 데이터베이스에 SQL statements를 보내기 위한 Statement를 생성하는 메서드입니다.

## DriverManager

![](https://images.velog.io/images/yunyoseob/post/61bcca63-9c63-4f71-9e22-dc3c4554c710/image.png)

DriverManager 클래스는 일반 클래스입니다.

> **method**

![](https://images.velog.io/images/yunyoseob/post/1dd133b3-2319-46a6-ae0f-39ca6ffbf14a/image.png)

DriverManager 클래스의 getConnection(String url, String user, String password)
메서드는 데이터베이스의 URL과 유저, password를 입력하여 static한 Connection클래스로 
반환하여 주는 메서드입니다.

## Statement

![](https://images.velog.io/images/yunyoseob/post/c9639cc9-5777-4b5d-81eb-6062740c90cc/image.png)

Statement 클래스는인터페이스 클래스입니다.

> **method**

![](https://images.velog.io/images/yunyoseob/post/730ac990-0b6a-4a75-a840-91eb39f07644/image.png)

Statement 클래스의 executeQuery(String sql)은 쿼리문을 전달하여 ResultSet object로 반환하는 메서드입니다.

## ResultSet

![](https://images.velog.io/images/yunyoseob/post/acd7b84d-05b6-43d7-a00e-57642f238d6a/image.png)

ResultSet 클래스는 인터페이스 클래스입니다.

> **method**

![](https://images.velog.io/images/yunyoseob/post/96e9cc64-6260-4b03-9636-22483ed07a8b/image.png)

커서를 현재 위치에서 다음 행으로 이동하는 method입니다.


![](https://images.velog.io/images/yunyoseob/post/49754bf9-ef1c-4ae5-886b-685f1c916050/image.png)

ResultSet 객체의 현재 행에 있는 지정된 칼럼을 java의 String으로 검색하는 메서드입니다.


## 예제를 통해 살펴보는 JAVA와 Oracle DB 연동

> **요구사항**

Oracle DB의 DEPT 테이블을 JDBC 연동하여 테이블을 조회하시오.

단, JAVA에서 DeptTest클래스의 deptSelect() 메서드를 사용해서

DEPT 테이블에 있는 칼럼 전체를 조회한 뒤, main 함수에서 콘솔에 출력하시오.

단, DeptVO 클래스에 세터 메서드와 게터 메서드를 만들어, Information Hiding된 private변수인 deptno, dname, loc 변수를 public 생성자를 호출하여 출력시키시오.

> **DeptVO**

```java
package a.b.c.oracle.vo;

public class DeptVO {

	private String deptno;
	private String dname;
	private String loc;
	
	// constructor 
	public DeptVO() {
	}

	public DeptVO(String deptno, String dname, String loc) {
	
		this.deptno = deptno;
		this.dname = dname;
		this.loc = loc;
	}
	
	// getter
	public String getDeptno() {
		return deptno;
	}
	public String getDname() {
		return dname;
	}
	public String getLoc() {
		return loc;
	}
	
	// setter
	public void setDeptno(String deptno) {
		this.deptno = deptno;
	}
	public void setDname(String dname) {
		this.dname = dname;
	}
	public void setLoc(String loc) {
		this.loc = loc;
	}
}
```

> **DeptTest**

```java
package a.b.c.oracle;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.ArrayList;

import a.b.c.oracle.vo.DeptVO;

public class DeptTest {

	// DataSource 정보 : 데이터베이스 연결 정보
	public static final String JDBC_DRIVER = "oracle.jdbc.driver.OracleDriver";
	public static final String JDBC_URL = "jdbc:oracle:thin:@HOST:PORT:SERVICE_NAME";
	public static final String JDBC_USER = USER;
	public static final String JDBC_PASSWORD = PASSWORD;
	
	
	
	// sql Query 
	public static String sqlQuery = "SELECT DEPTNO, DNAME, LOC  FROM DEPT";	
	
	// 생성자 
	public DeptTest() {

		try {
			Class.forName(JDBC_DRIVER);
		}catch(Exception e) {
			System.out.println("JDBC 드라이버를 찾지 못했서요 >>> : " + e.getMessage());
		}
	}
	
	// deptSelect() 함수
	public ArrayList<DeptVO> deptSelect(){
		
		ArrayList<DeptVO> aList = null;
		Connection conn = null;
		Statement stmt = null;
		ResultSet rsRs = null;
		
		try {
			// 커넥션 연결
			conn = DriverManager.getConnection(	DeptTest.JDBC_URL, 
												DeptTest.JDBC_USER, 
												DeptTest.JDBC_PASSWORD);
			// 쿼리문전달통로 만들기
			stmt = conn.createStatement();
			
			// 쿼리문 전달 및 질의결과 받아오기 
			rsRs = stmt.executeQuery(DeptTest.sqlQuery);
			
			// 데이터베이스에 받아온 질의 결과 DeptVO 와 ArrayList에 넣기 
			
			// 데이터가 있으면 수행하기 
			if (rsRs !=null) {
				// DeptVO 클래스 담은 배열객체 ArrayList 를 인스턴스 한다. 
				aList = new ArrayList<DeptVO>();
				
				// rsRs 에서 데이터 추출해서 DeptVO 에 넣고 ArrayList에 담기
				// 1. while 구문으로 next() 함수 리절트셋에서 레코드 추출하기 
				while (rsRs.next()) {
					// DetpVO 클래스 선언 및 인스턴스 : 데이터베이스에서 가져온 데이터 담기 위해서 
					DeptVO dvo = new DeptVO();
					dvo.setDeptno(rsRs.getString(1));
					dvo.setDname(rsRs.getString(2));
					dvo.setLoc(rsRs.getString(3));
					
					// ArrayList 에 DeptVO 클래스 담기 
					aList.add(dvo);
				}
				
			}else {
				System.out.println("데이터베이스에서 가져온 데이터가 없습니다. >>> : ");
			}
			
		}catch(Exception e) {
			System.out.println("에러가 >>> : " + e.getMessage());
		}
		
		return aList;
	}
		

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		DeptTest dt = new DeptTest();
		
		ArrayList<DeptVO> aList = dt.deptSelect();
		
		if (aList !=null && aList.size() > 0) {
			System.out.println("몇 건인가  >>> : " + aList.size());
			
			for (int i=0; i < aList.size(); i++) {
				DeptVO _dvo = aList.get(i);
				System.out.print(_dvo.getDeptno() + " : ");
				System.out.print(_dvo.getDname() + " : ");
				System.out.println(_dvo.getLoc());
			}
		}		
	}
}
```

## 예제 풀이

> **DeptVO**

|코드|설명|
|--|--|
|package a.b.c.oracle.vo|해당 클래스의 패키지입니다.|
|private 변수|해당 변수는 원칙상 클래스 밖에서 사용이 불가합니다. 그러나, public 생성자와 this변수를 통해 해당 변수를 외부에서 사용할 수 있습니다.|
|public DeptVO()|기본 생성자를 오버로딩합니다.|
|public DeptVO(String deptno, String dname, String loc)|매개변수가 있는 생성자를 오버로딩합니다.|
|public String get~~|게터 메서드를 생성하여 return값으로 현재 클래스의 변수를 반환합니다.|
|public void set~~|세터 메서드를 생성하여 인수를 현재 클래스의 private 변수에 대입하여 줍니다.|

> **DeptTest**

|코드|설명|
|--|--|
|public static final String JDBC_DRIVER|oracle.jdbc.driver.OracleDriver 클래스를 찾아야 하므로 해당 값을 JDBC_DRIVER 변수로 지정해줍니다.|
|public static final String JDBC_URL|jdbc.oracle.thin@HOST:PORT:SERVICE_NAME를 입력하여 줍니다.|
|public static final String JDBC_USER|계정을 입력하여 줍니다.|
|public static final String JDBC_PASSWORD|비밀번호를 입력하여 줍니다.|

**해당 정보는 product -> dbhome_1 -> jdbc -> lib -> NETWORD -> ADMIN 파일에서
listener.ora, tnsnames.ora 파일을 통해 살펴볼 수 있습니다.**

```sql
# tnsnames.ora Network Configuration File: C:\app\product\11.2.0\dbhome_1\network\admin\tnsnames.ora
# Generated by Oracle configuration tools.

ORCLYYS00 =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = 호스트)(PORT = 포트))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = 서비스이름)
    )
  )
```

**호스트와 포트번호, 서비스이름을 잘 확인하여 코드를 작성해야, 향후, DB에 연결이 됩니다.**

|코드|설명|
|--|--|
|public static String sqlQuery|SELECT DEPTNO, DNAME, LOC FROM DEPT =>  DEPT 테이블에서 DEPTNO, DNAME, LOC 칼럼을 조회하는 쿼리문을 작성합니다.|
|public DeptTest()|기본생성자를 만드는데, 이 때, Class.forName(JDBC_DRIVER) 명령문을 통해 oracle.jdbc.driver.OracleDriver 클래스가 있는지 확인 후 없으면, JDBC 드라이버를 찾지 못했다고 예외처리합니다.|
|conn=DriverManager.getConnection|java.sql.Connection 인터페이스를 상속해서 Oracle Vender에서 jdbc 드라이버를 만드는 팀에서 실현한 클래스로 인수로 들어온 정보를 통해, 자바어플과 DB가 연결되면, 자동커밋으로 세션이 열립니다.|
|stmt=conn.createStatement()|java.sql.Statement를 상속한 오라클 벤더 구현체 클래스가 createStatement() 함수에 적재된 커리문 문자열을 가지고 오라클 DB에 전달합니다.|
|rsRs=stmt.executeQuery(DeptTest.sqlQuery)|오라클 DB에 전달된 쿼리문을 오라클 Optimizer가 실행을 해서 결과가 발생이 되면 해당 결과를 java.sql.ResultSet 인터페이스를 상속한 오라클 벤더 구현체 클래스가 결과를 받습니다. (그 결과를 파일 형태의 메모리 구조로 가지고 있습니다.)|
|while(rsRs.next())|while 구문으로 next() 함수로 레코드를 추출합니다.|
|DeptVO dvo=new DeptVO|DeptVO 클래스에 기본 생성자를 만듭니다.|
|dvo.set~~(rsRs.getString(i)|ResultSet 객체의 현재 행에 있는 지정된 칼럼을 java의 String으로 검색하는 메서드입니다. i가 입력되면, SQL의 테이블에 지정된 i 칼럼 정보를 DeptVO 클래스의 세터메서드로 선언하여줍니다.|
|aList.add(dvo)|DeptVO 클래스의 참조변수 dvo의 정보를 ArrayList < DeptVO> 배열 클래스에 추가하여 줍니다.|
|System.out.println("몇 건인가 >>> : "+aList.size());|aList.size()가 4인 것을 확인 할 수 있는데, 이는 Dept 테이블에 행의 수와 동일합니다.|
| _ dvo.get~()|DeptVo 클래스의 게터메서드를 통해 현재 세팅된, this변수들을 출력시킵니다.| 

> **출력 결과**

몇 건인가  >>> : 4
10 : ACCOUNTING : NEW YORK
20 : RESEARCH : DALLAS
30 : SALES : CHICAGO
40 : OPERATIONS : BOSTON


**이상으로 java.sql 포스팅을 마치도록 하겠습니다. 😀**
