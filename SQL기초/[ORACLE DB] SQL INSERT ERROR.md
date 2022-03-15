안녕하세요. 😊 오늘은 SQL의 DML에서 INSERT 구문 활용시 발생하는 ORACLE ERROR에 대해서 포스팅하도록 하겠습니다.

- SQL Structured Query Language의 DML에 대한 포스팅은 [[Oracle DB] SQL 기초문법 2편](https://velog.io/@yunyoseob/Oracle-DB-SQL-%EA%B8%B0%EC%B4%88%EB%AC%B8%EB%B2%95-2%ED%8E%B8)에서 확인하실 수 있습니다.

> **INSERT 명령어를 사용시에 주의해야할 사항**

|번호|주의할 내용|
|--|--|
|**1**|**컬럼 갯수, 순서와 값 갯수 순서 일치시키기**|
|**2**|**데이터 타입 확인하기**|
|**3**|**데이터 사이즈 확인하기**|
|**4**|**NULL 데이터 확인하기**|

> **오늘 포스팅에 사용할 TABLE**

```sql
CREATE TABLE VELOG(
    T1 VARCHAR2(20) PRIMARY KEY,
    T2 VARCHAR2(20) NOT NULL,
    T3 NUMBER (7,2),
    T4 VARCHAR2(1),
    T5 DATE
);
```

데이터 입력하기

```sql
INSERT INTO VELOG(T1, T2, T3, T4, T5)
VALUES ('1', 'VELOG',1,'Y',SYSDATE);

INSERT INTO VELOG
VALUES('2','VELOG_2',2,'Y',SYSDATE);
-- 테이블 이름 뒤에 (칼럼1,...칼럼N)을 생략해도 입력이 됩니다.
```

규칙을 잘 지켜서 입력할 경우, 데이터가 잘 입력되는 것을 확인 할 수 있습니다.

**✔ 질의 결과**

||T1|T2|T3|T4|T5|
|--|--|--|--|--|--|
|1|1|VELOG|1|Y|22/03/15|
|2|2|VELOG 2|2|Y|22/03/15|

## INSERT ERROR

### **COLUMN 누락(ORA-00947)**

```sql
INSERT INTO VELOG
VALUES('3','VELOG_2','Y',SYSDATE);

/*
오류 보고 -
SQL 오류: ORA-00947: 값의 수가 충분하지 않습니다
00947. 00000 -  "not enough values"
*/

DESC VELOG;

/*
이름 널?       유형           
-- -------- ------------ 
T1 NOT NULL VARCHAR2(20) 
T2 NOT NULL VARCHAR2(20) 
T3          NUMBER(7,2)  
T4          VARCHAR2(1)  
T5          DATE       
*/
```

칼럼 T3에 데이터를 입력하지 않으면서 **ORA-00947** 에러가 출력됩니다. 

- 따라서, 테이블 뒤에 칼럼이름을 적는 것을 지향하는 것이 좋습니다.

```sql
INSERT INTO VELOG (T1, T2, T4, T5)
VALUES('3','VELOG_2',SYSDATE);


/*
오류 보고 -
SQL 오류: ORA-00947: 값의 수가 충분하지 않습니다
00947. 00000 -  "not enough values"
*/
```

동일한 에러가 출력되는 것을 확인 할 수 있습니다. 테이블 옆 소괄호 안에 칼럼을 입력하여도 해당 칼럼을 누락한 것이 없는지 확인해야 합니다.

```sql
INSERT INTO VELOG (T1, T2, T4, T5)
VALUES('3','VELOG_2','Y',SYSDATE);
```
위 코드를 실행했을 때, 스크립트에서 **1 행 이(가) 삽입되었습니다.** 라고 출력이 됩니다.

**✔ 질의 결과**

||T1|T2|T3|T4|T5|
|--|--|--|--|--|--|
|1|1|VELOG|1|Y|22/03/15|
|2|2|VELOG 2|2|Y|22/03/15|
|3|3|VELOG 2|(null)|Y|22/03/15|

마지막에 입력시, T3 칼럼에 값을 입력하지 않았는데, 해당 칼럼에 데이터가 (null)으로 출력되는 것을 볼 수 있습니다.


### **COLUMN 데이터 타입 에러**

> **열 사용 에러(ORA-00984)**

```sql
/*
이름 널?       유형           
-- -------- ------------ 
T1 NOT NULL VARCHAR2(20) 
T2 NOT NULL VARCHAR2(20) 
T3          NUMBER(7,2)  
T4          VARCHAR2(1)  
T5          DATE  
*/

INSERT INTO VELOG (T1, T2, T4, T5)
VALUES('4',VELOG_2,'Y',SYSDATE);

/*
오류 보고 -
SQL 오류: ORA-00984: 열을 사용할 수 없습니다
00984. 00000 -  "column not allowed here"
*/
```

VELOG_2 데이터를 입력할 때, 싱글쿼테이션(' ')을 누락하면서 **ORA-00984**에러가 출력됩니다. 

> **NUMBER와 VARCHAR()은 다르게 입력해도 입력이 될 때가 있다.**

```sql
DESC VELOG;

/*
이름 널?       유형           
-- -------- ------------ 
T1 NOT NULL VARCHAR2(20) 
T2 NOT NULL VARCHAR2(20) 
T3          NUMBER(7,2)  
T4          VARCHAR2(1)  
T5          DATE        
*/

INSERT INTO VELOG (T1, T2, T4, T5)
VALUES(4,'VELOG_2','Y',SYSDATE);
```

비록, T1의 데이터 타입이 VARCHAR2(20)이지만, NUMBER를 입력해도 문제 없이 스크립트에서 **1 행 이(가) 삽입되었습니다.**라고 출력되는 것을 확인 할 수 있습니다. 

```sql
INSERT INTO VELOG (T1, T2, T3, T5)
VALUES(5,'VELOG_2','4',SYSDATE);
```

마찬가지로 NUMBER 타입에 문자숫자를 입력해도 정상적으로 입력이 됩니다.


**✔ 질의 결과**

||T1|T2|T3|T4|T5|
|--|--|--|--|--|--|
|1|1|VELOG|1|Y|22/03/15|
|2|2|VELOG 2|2|Y|22/03/15|
|3|3|VELOG 2|(null)|Y|22/03/15|
|4|4|VELOG 2|(null)|Y|22/03/15|
|5|5|VELOG 2|4|(null)|22/03/15|

> **DATE 타입 입력 에러**

```sql
/*
이름 널?       유형           
-- -------- ------------ 
T1 NOT NULL VARCHAR2(20) 
T2 NOT NULL VARCHAR2(20) 
T3          NUMBER(7,2)  
T4          VARCHAR2(1)  
T5          DATE  
*/

INSERT INTO VELOG (T1, T2, T3, T5)
VALUES(6,'VELOG_2','4','A');

/*
오류 보고 -
ORA-01841: 년은 영이 아닌 -4713 과 +4713 사이의 값으로 지정해야 합니다.
*/
```

T5 칼럼에 DATE 타입의 값을 입력하지 않아, **ORA-01841** 에러가 출력되는 것을 확인 할 수 있습니다.

```sql
INSERT INTO VELOG (T1, T2, T3, T5)
VALUES(6,'VELOG_2','4',20220315);

/*
오류 보고 -
SQL 오류: ORA-00932: 일관성 없는 데이터 유형: DATE이(가) 필요하지만 NUMBER임
00932. 00000 -  "inconsistent datatypes: expected %s got %s"
*/
```

T5 칼럼에 DATE 타입이 NUMBER여서 입력이 되지 않아, **ORA-00932** 에러가 스크립트에 출력되었습니다.

```sql
INSERT INTO VELOG (T1, T2, T3, T5)
VALUES(6,'VELOG_2','4','2022315');

/*
오류 보고 -
ORA-01861: 리터럴이 형식 문자열과 일치하지 않음
*/
```

데이터 입력시 리터럴이 형식 문자열('yyyyMMdd')과 맞지 않아 **ORA-01861** 에러가 출력되는 것을 볼 수 있습니다.



> **DATE 타입 입력이 되는 경우**

```sql
INSERT INTO VELOG (T1, T2, T3, T5)
VALUES(6,'VELOG_2','4',TO_CHAR(SYSDATE));
```
그러나 다음과 같이, SYSDATE를 TO_CHAR로 입력하는 것은 가능합니다.

```sql
INSERT INTO VELOG (T1, T2, T3, T5)
VALUES(7,'VELOG_2','4',TO_CHAR(TO_DATE(SYSDATE)));
```

SYSDATE를 TO_DATE 한 다음, TO_CHAR로 입력해도 입력됩니다.

```sql
INSERT INTO VELOG (T1, T2, T3, T5)
VALUES(8,'VELOG_2','4','22/03/15');
```

오늘 날짜를 '22/03/15' 날짜 형식으로 입력해도 입력이 됩니다.

```sql
INSERT INTO VELOG (T1, T2, T3, T5)
VALUES(9,'VELOG_2','4','22/3/15');
```

월에 0을 생략해도 입력이 됩니다.

```sql
INSERT INTO VELOG (T1, T2, T3, T5)
VALUES(10,'VELOG_2','4','20220315');
```

이전에 '2022315'인 경우, ORA-01861에러가 출력되었으나, 리터럴이 형식 문자열에 맞는 경우에는 정상적으로 입력이 됩니다.


**✔ 질의 결과**

||T1|T2|T3|T4|T5|
|--|--|--|--|--|--|
|1|1|VELOG|1|Y|22/03/15|
|2|2|VELOG 2|2|Y|22/03/15|
|3|3|VELOG 2|(null)|Y|22/03/15|
|4|4|VELOG 2|(null)|Y|22/03/15|
|5|5|VELOG 2|4|(null)|22/03/15|
|6|6|VELOG 2|4|(null)|22/03/15|
|7|7|VELOG 2|4|(null)|22/03/15|
|8|8|VELOG 2|4|(null)|22/03/15|
|9|9|VELOG 2|4|(null)|22/03/15|
|10|10|VELOG 2|4|(null)|22/03/15|

## **COLUMN 데이터 사이즈 에러**


> **NUMBER SIZE 에러(ORA-01438)**

```sql
/*
이름 널?       유형           
-- -------- ------------ 
T1 NOT NULL VARCHAR2(20) 
T2 NOT NULL VARCHAR2(20) 
T3          NUMBER(7,2)  
T4          VARCHAR2(1)  
T5          DATE    
*/

INSERT INTO VELOG (T1, T2, T3, T5)
VALUES(11,'VELOG_3',123456789,'20220315');

/*
오류 보고 -
ORA-01438: 이 열에 대해 지정된 전체 자릿수보다 큰 값이 허용됩니다.
*/
```

NUMBER(7,2) 데이터 타입의 T3 칼럼에서 사이즈를 초과 하는 경우, **ORA-01438** 에러가 출력됩니다.


**✔ 주의사항**

```sql
INSERT INTO VELOG (T1, T2, T3, T5)
VALUES(11,'VELOG_3',1.12345,'20220315');
```

다음과 같이 명령어를 입력할 때, NUMBER(7,2) 규칙을 위배했으나, 1행이 입력됩니다.

||T1|T2|T3|T4|T5|
|--|--|--|--|--|--|
|11|11|VELOG 3|1.12|(null)|22/03/15|

그러나, 이 때 소수점 2번째 자리 이하는 입력이 되지 않습니다.

> **VARCHAR2(20) SIZE 에러(ORA-12899)**

```sql
/*
이름 널?       유형           
-- -------- ------------ 
T1 NOT NULL VARCHAR2(20) 
T2 NOT NULL VARCHAR2(20) 
T3          NUMBER(7,2)  
T4          VARCHAR2(1)  
T5          DATE    
*/


INSERT INTO VELOG (T1, T2, T3, T5)
VALUES(12,'VELOGVELOGVELOGVELOGVELOGVELOG',1.12,'20220315');

/*
오류 보고 -
ORA-12899: "SCOTT"."VELOG"."T2" 열에 대한 값이 너무 큼(실제: 30, 최대값: 20)
*/

SELECT LENGTH('VELOGVELOGVELOGVELOGVELOGVELOG') FROM DUAL;

-- 30
```

VARCHAR2(20)인 T2 칼럼에 사이즈가 초과되는 데이터가 들어가면서, **ORA-12899** 에러가 발생하게 됩니다.

```sql
INSERT INTO VELOG (T1, T2, T4, T5)
VALUES(12,'VELOG_3','YES',SYSDATE);

/*
오류 보고 -
ORA-12899: "SCOTT"."VELOG"."T4" 열에 대한 값이 너무 큼(실제: 3, 최대값: 1)
*/

SELECT LENGTH('YES') FROM DUAL;
-- 3
```

마찬가지로, VARCHAR2(1)인 T1 칼럼에 사이즈가 초과되는 데이터가 들어가면서, **ORA-12899** 에러가 발생하게 됩니다.


**✔ 주의사항**


```sql
/*
이름 널?       유형           
-- -------- ------------ 
T1 NOT NULL VARCHAR2(20) 
T2 NOT NULL VARCHAR2(20) 
T3          NUMBER(7,2)  
T4          VARCHAR2(1)  
T5          DATE    
*/

SELECT LENGTH('벨로그벨로그벨로그벨로그벨로그') FROM DUAL;
-- 15

INSERT INTO VELOG (T1, T2, T4, T5)
VALUES(12,'벨로그벨로그벨로그벨로그벨로그','Y',SYSDATE);


/*
오류 보고 -
ORA-12899: "SCOTT"."VELOG"."T2" 열에 대한 값이 너무 큼(실제: 30, 최대값: 20)
*/
```

한글의 경우, LENGTH 함수로 확인하였을 때, VARCHAR2(20)보다 작은 15가 출력되어도 ORA-12899 오류가 날 수 있습니다.

```sql
INSERT INTO VELOG (T1, T2, T4, T5)
VALUES(12,'벨로그','Y',SYSDATE);
```
3글자로 입력했을 때는 정상적으로 입력되는 것을 확인할 수 있습니다.

## 기타 에러


> **누락된 콤마(ORA-00917)**

```sql
INSERT INTO VELOG (T1, T2, T4, T5)
VALUES(12'벨로그','Y'SYSDATE);
```

데이터 사이즈 에러와는 별개로 다음과 같이 콤마(,)로 구분하지 않았을 때, ORA-00917 에러가 출력되는 것을 확인 할 수 있습니다.

> **명령어 누락**

```sql
NSERT INTO VELOG (T1,T2, T3, T5)
VALUES(13,'벨로그',1.12,SYSDATE);

/*
오류 보고 -
알 수 없는 명령
*/
```

INSERT 명령어에 I를 누락하여, 명령어를 제대로 입력하지 않았을 때 발생하는 에러입니다.

> **NULL 입력 에러(ORA-01400)**

```sql
/*
이름 널?       유형           
-- -------- ------------ 
T1 NOT NULL VARCHAR2(20) 
T2 NOT NULL VARCHAR2(20) 
T3          NUMBER(7,2)  
T4          VARCHAR2(1)  
T5          DATE       
*/

INSERT INTO VELOG (T1, T3, T5)
VALUES('13',1.12,SYSDATE);

/*
오류 보고 -
ORA-01400: NULL을 ("SCOTT"."VELOG"."T2") 안에 삽입할 수 없습니다
*/
```

T2 컬럼은 NOT NULL 조건이 있습니다. 데이터를 입력할 때, NULL이면 안 된다는 의미입니다. 따라서, T1, T3, T5를 데이터 형식에 맞게 그리고 사이즈에 맞게 입력하여도, **ORA-01499** 에러가 스크립트에 출력됩니다.

> **PRIMARY KEY 데이터 입력시 주의사항**


![](https://images.velog.io/images/yunyoseob/post/7073af7c-fe2e-4ba4-b75e-42a7a1dce9b9/image.png)

SCOTT 계정의 VELOG 테이블에서 T1 칼럼은 PRIMARY KEY입니다. 

PRIMARY KEY의 특징은 다음과 같습니다.

**1. NULL값이 있으면 안 된다.**
**2. 값이 UNIQUE 해야한다.**

```sql
INSERT INTO VELOG (T2, T3, T5)
VALUES('벨로그',1.12,SYSDATE);

오류 보고 -
ORA-01400: NULL을 ("SCOTT"."VELOG"."T1") 안에 삽입할 수 없습니다
```

따라서, 값을 입력할 때, PK를 입력하지 않으면 NULL 입력 에러인 ORA-01400 에러가 출력됩니다.

```sql
INSERT INTO VELOG (T1, T2, T3, T5)
VALUES('1','벨로그',1.12,SYSDATE);

/*
오류 보고 -
ORA-00001: 무결성 제약 조건(SCOTT.SYS_C0011062)에 위배됩니다
*/
```

||T1|T2|T3|T4|T5|
|--|--|--|--|--|--|
|1|1|VELOG|1|Y|22/03/15|

현재 PK인 T1 칼럼에는 1값이 이미 입력이 되어있습니다. PK 값은 UNIQUE 해야하므로, 중복값을 입력시 **ORA-00001** 에러가 출력되는 것을 볼 수 있습니다.

## INSERT ERROR 수정방법

에러가 발생했을 때, 수정하는 방법을 마

```sql
/*
이름 널?       유형           
-- -------- ------------ 
T1 NOT NULL VARCHAR2(20) 
T2 NOT NULL VARCHAR2(20) 
T3          NUMBER(7,2)  
T4          VARCHAR2(1)  
T5          DATE       
*/

INSERT INTO VELOG(T1, T2, T3, T4, T5)
VALUES ('1', '벨로그벨로그벨로그벨로그벨로그','YES',SYYSDATE);

/*
SQL 오류: ORA-00947: 값의 수가 충분하지 않습니다
00947. 00000 -  "not enough values"
*/
```

예시로 다음과 같은 쿼리문을 입력했을 때, 누락 에러(ORA-00984)가 발생하였습니다.

```sql
INSERT INTO VELOG(T1, T2, T3, T4, T5)
VALUES ('1', '벨로그벨로그벨로그벨로그벨로그',NULL,'YES',SYYSDATE);

/*
SQL 오류: ORA-00984: 열을 사용할 수 없습니다
00984. 00000 -  "column not allowed here"
*/
```

T3 칼럼이 누락된 것을 확인하고 NULL 값을 입력하고 나니, 열 사용 에러(ORA-00984) 에러가 출력됩니다.

```sql
INSERT INTO VELOG(T1, T2, T3, T4, T5)
VALUES (NULL, NULL, NULL, NULL, NULL);

/*
오류 보고 -
ORA-01400: NULL을 ("SCOTT"."VELOG"."T1") 안에 삽입할 수 없습니다
*/
```

어떤 컬럼에서 값을 잘못 넣었는지 확인하기 위해, NULL 값으로 전부 입력하자, T1칼럼에 NULL 입력 에러인 ORA-01400 에러가 출력됩니다.

```sql
/*
이름 널?       유형           
-- -------- ------------ 
T1 NOT NULL VARCHAR2(20) 
T2 NOT NULL VARCHAR2(20) 
T3          NUMBER(7,2)  
T4          VARCHAR2(1)  
T5          DATE       
*/

INSERT INTO VELOG(T1, T2, T3, T4, T5)
VALUES ('1', NULL, NULL, NULL, NULL);

/*
오류 보고 -
ORA-01400: NULL을 ("SCOTT"."VELOG"."T2") 안에 삽입할 수 없습니다
*/
```

이번엔 T2 칼럼에 NULL 입력에러 ORA-01400 에러가 출력됩니다.

```sql
INSERT INTO VELOG(T1, T2, T3, T4, T5)
VALUES ('1', 'V', NULL, NULL, NULL);

/*
오류 보고 -
ORA-00001: 무결성 제약 조건(SCOTT.SYS_C0011062)에 위배됩니다
*/
```

T2 칼럼에도 값을 넣고 나니, 무결성 조건에 위배되는ORA-00001 에러가 출력됩니다. (PK 중복값 에러)

**🤔 SCOTT 계정의 SYS_C0011062에 위배된다고 하는데, SYS_C0011062는 어떤 칼럼일까요?**

```sql
SELECT  A.TABLE_NAME,  A.COLUMN_NAME, A.INDEX_NAME 
FROM    ALL_IND_COLUMNS A
WHERE   A.TABLE_NAME IN ('VELOG');
```

다음과 같은 명령어를 입력했을 때 결과는 다음과 같습니다.

|TABLE_NAME|COLUMN_NAME|INDEX_NAME|
|---|---|---|
|VELOG|T1|SYS C0011062|

SYS C0011062는 INDEX_NAME으로, COLUMN_NAME은 T1인 것을 확인하였습니다.

명령어 없이 테이블에서 Oracle SQL Devloper에서 테이블 중VELOG 테이블을 클릭하여 인덱스를 클릭해도 볼 수 있습니다.

```sql
INDEX_OWNER|INDEX_NAME	|UNIQUENESS|....
SCOTT	   |SYS C0011062|UNIQUE	   |
```

```sql
SELECT*FROM VELOG;
```
현재 VELOG의 T1 칼럼에는 1부터 12까지 순차적으로 입력이 되있는 것을 확인했습니다.

```
INSERT INTO VELOG(T1, T2, T3, T4, T5)
VALUES ('13', 'V', NULL, NULL, NULL);
```

다음과 같이 T1 칼럼에 UNIQUE하면서 NULL이 아닌 '13'을 입력하니 정상적으로 입력이 되는 것을 확인 할 수 있습니다.

> **최종 결과**

||T1|T2|T3|T4|T5|
|--|--|--|--|--|--|
|1|1|VELOG|1|Y|22/03/15|
|2|2|VELOG 2|2|Y|22/03/15|
|3|3|VELOG 2|(null)|Y|22/03/15|
|4|4|VELOG 2|(null)|Y|22/03/15|
|5|5|VELOG 2|4|(null)|22/03/15|
|6|6|VELOG 2|4|(null)|22/03/15|
|7|7|VELOG 2|4|(null)|22/03/15|
|8|8|VELOG 2|4|(null)|22/03/15|
|9|9|VELOG 2|4|(null)|22/03/15|
|10|10|VELOG 2|4|(null)|22/03/15|
|11|11|VELOG 3|1.12|(null)|22/03/15|
|12|12|벨로그|(null)|Y|22/03/15|
|13|13|V|(null)|(null)|(null)|


**이상으로 [ORACLE DB] SQL INSERT ERROR 포스팅을 마치도록 하겠습니다. 😀**
