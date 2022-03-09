안녕하세요 😀. 오늘은 java.sql의 PreparedStatement에 대해 알아보도록 하겠습니다. 

- 저번 [java.sql편](https://velog.io/@yunyoseob/JAVA-java.sql)을 못 보신 분은 보고 오시는 걸 권장합니다.

## PreparedStatement

[Java™ Platform Standard Ed. 8](https://docs.oracle.com/javase/8/docs/api/)에서 java.sql에서 PreparedStatement를 클릭하시면 다음과 같은 화면이 나옵니다.

![](https://images.velog.io/images/yunyoseob/post/217e4563-68e3-486a-a7ef-b2d14c678cbb/image.png)

PreparedStatement 클래스는 인터페이스 클래스(구현부가 없는 클래스)로 Statement의 상속관계에 있는 클래스입니다. (Statement 클래스 또한 인터페이스 클래스입니다. )


## Statement vs PreparedStatement

> **Statement 코드 예시** 

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

// sqlQuery
public static String sqlQuery="SELECT B.DEPTNO AS DEPTNO, B.DNAME AS DNAME, B.LOC AS LOC FROM SCOTT.DEPT B";

//  기타 멤버변수와 클래스, 메서드 생략...

// 지역변수
Connection conn=null;
Statement stmt=null;
ResultSet rsRs=null;

conn=DriverManager.getConnection(JDBC_URL, JDBC_USER, JDBC_PASSWORD);
stmt=conn.createStatement();
rsRs=stmt.executeQuery(sqlQuery);
```

**Statement의 경우, 쿼리문을 Statement 클래스의 executeQuery 메서드에 
인수로 쿼리문을 작성하여, ResultSet 클래스의 참조변수로 리턴합니다.**

> **PreparedStatement 코드 예시** 

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

//  sqlQuery
public static String sqlQuery="SELECT EMPNO, ENAME, JOB, MGR FROM EMP WHERE EMPNO=? AND ENAME=UPPER(?) ";
//  기타 멤버변수와 클래스, 메서드 생략...

// 지역변수
Connection conn=DriverManager.getConnection(JDBC_URL, JDBC_USER, JDBC_PASSWORD);

PreparedStatement pstmt = conn.prepareStatement(sqlQuery);

pstmt.setString(1, empno)
pstmt.setString(2,  ename);

ResultSet rsRs = pstmt.executeQuery();

// empno : 7499
// ename : ALLEN
```

**반면, PreparedStatement의 경우, Connection 클래스의 
prepareStatement 메서드에 인수로 쿼리문을 작성하여 
PrepareStatement 클래스로 보냅니다.** 

![](https://images.velog.io/images/yunyoseob/post/4a1d6bee-ce32-4a14-aa2f-fa2705bd5d92/image.png)


**그 이후, PreparedStatement 클래스의 setString 메서드를 통해 
파라미터인덱스 인수와 String 값을 입력합니다.**

![](https://images.velog.io/images/yunyoseob/post/89cdc8e3-7318-4b1a-8c05-35adb830abc0/image.png)

**그리고, Statement 클래스의 메서드인 executeQuery를 통해 
객체를 ResultSet 클래스의 참조변수로 리턴합니다.**

![](https://images.velog.io/images/yunyoseob/post/28ce95c0-4ef8-4101-a471-ae2c2c33968a/image.png)


> **Statement와 PreparedStatement 차이**

**위에서 코드로 보았듯, Statement와 PreparedStatement는 쿼리문을 어디서 작성하는 지에 따라 그 쓰임이 다른 것을 볼 수 있습니다.**

**1. Statement의 경우, Statement 클래스의 executeQuery 메서드에서 작성하는 반면,** 
**PreparedStatement의 경우,  Connection 클래스의 prepareStatement 메서드에서 작성합니다.**

**2. PreparedStatement의 참조변수.executeQuery() 메서드를 통해, ResultSet 클래스의 참조변수에 결과값을 대입합니다.**


## Placeholder

```java
//  sqlQuery
public static String sqlQuery="SELECT EMPNO, ENAME, JOB, MGR FROM EMP WHERE EMPNO=? AND ENAME=UPPER(?) ";
//  기타 멤버변수와 클래스, 메서드 생략...

PreparedStatement pstmt = conn.prepareStatement(sqlQuery);

pstmt.setString(1, empno)
pstmt.setString(2,  ename);

// empno : 7499
// ename : ALLEN
```

위의 PreparedStatement 코드 예시를 보면 ?가 있는 것을 볼 수 있습니다. 

> **JAVA에서 ? 코드는 place holder를 의미합니다.**

PreparedStatement의 setString 메서드의 인수를 첫 번째 인수에 int 자료형을 두 번째 인수에 String 자료형을 입력한 뒤, placeholder에 setString으로 세팅한 인수를 입력하여 쿼리문을 채웁니다.


[JAVA : Scanner와 연산자](https://velog.io/@yunyoseob/JAVA-Scanner%EC%99%80-%EC%97%B0%EC%82%B0%EC%9E%90) 포스팅에서 삼항 연산자에 대한 내용을 잠시 다뤘던 적이 있는데요.

```java

int A=10;
int B=11;

char ch=' ';
ch = (A>B) ? 'T' : 'F';
System.out.println("A>B :::: "+ch);

// A>B :::: F
```

삼항 연산자에서도 A가 B보다 큰지 아닌 지의 결과를 T 혹은 F로 char ch에 대입하여 출력시키는 예제를 다뤄보기도 했습니다.

이처럼 어떤 결과를 placeholder에 담아 쿼리문 내에 대입시켜 활용할 수도 있습니다.


**이상으로 JAVA : PreparedStatement 포스팅을 마치도록 하겠습니다 😊**
