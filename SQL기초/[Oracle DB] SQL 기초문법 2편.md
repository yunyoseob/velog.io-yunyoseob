안녕하세요. 😃 오늘은 Oracle DB SQL 기초문법 2편에 대해 포스팅하도록 하겠습니다.

## SQL Structured Query Language

SQL의 Structured Query Language에는 크게 DQL, DML, DDL, TCL, DCL이 있습니다.

> **DQL**

DQL는 Data Query Language의 약자로, 테이블의 데이터를 조회 및 검색하는 명령어로 **SELECT** 명령어가 있습니다.

```sql
SELECT
```

[[Oracle DB] SQL 기초문법 1편](https://velog.io/@yunyoseob/Oracle-DB-SQL-%EA%B8%B0%EC%B4%88%EB%AC%B8%EB%B2%95-1%ED%8E%B8)에 SQL의 SELECT 키워드에 대해 포스팅 되어있으니 참고하시면 좋을 듯 합니다. 😁

> **DDL (데이터 정의어)**

DDL은 Data Definition Language의 약자로, 테이블을 포함한 여러 객체를 생성, 수정, 삭제하는 명령어입니다. DDL으로는 **CREATE, ALTER, DROP**이 있습니다. 

- **DDL 쿼리는 트랜잭션이 바로 적용됩니다.**

> **DCL (데이터 제어어)**

DCL은 Data Control Language의 약자로, 데이터 사용 권한 부여 및 취소를 하는 명령어입니다.
DCL으로는 **GRANT, REVOKE**가 있습니다.


> **DML (데이터 조작어)**

DML은 Data Manipulation Language의 약자로, 테이블의 데이터를 저장, 수정, 삭제하는 명령어입니다. DML으로는 **INSERT, UPDATE, DELETE**가 있습니다.


> **TCL (트랜잭션 제어어)**

TCL은 Transaction Control Language로 트랜잭션 데이터의 영구 저장, 취소 등의 명령어 입니다. TCL으로는 **COMMIT, ROLLBACK, SAVEPOINT**가 있습니다.

## DCL (데이터 제어어)

> **CREATE TABLE**

CREATE TABLE 명령어는 데이터 베이스 엔진에게 테이블 공간을 만들어달라는 명령어 입니다.

```sql
CREATE TABLE 계정이름.테이블이름(
	칼럼명1 	데이터타입1(사이즈)
    ,칼럼명2	데이터타입2
    ,칼럼명3	데이터타입3(사이즈)
    , ...
    , 칼럼명N	데이터타입N(사이즈)
)
```

계정이름은 생략이 가능하며, 계정이름이 없는 경우 현재의 계정에 테이블을 생성합니다.

```sql
CREATE TABLE SCOTT.TEST_T1(
    TC1 VARCHAR2(10) PRIMARY KEY
    ,TC2 VARCHAR2(20) NOT NULL
    ,TC3 NUMBER
    ,TC4 DATE
);
```

위의 SQL 명령어 의미는 다음과 같습니다.

```
1. 스코트 계정에 테이블 이름이 TEST_T1 인 테이블을 생성합니다.
2. 컬럼은 총 4개입니다.
3. 첫 번째 칼럼이름은 TC1이고, 데이터 타입은 VARCHAR2, 사이즈는 10, 기본키로 지정했으므로, UNIQUE해야 하고, NULL값이 있으면 안 됩니다.
4. 두 번째 칼럼이름은 TC2이고, 데이터 타입은 VARCHAR2, 사이즈는 20, NULL값이 있으면 안 됩니다.
5. 세 번째 칼럼이름은 TC3이고, 데이터 타입은 NUMBER, 사이즈는 기본값입니다.
6. 네 번째 칼럼이름은 TC4이고, 데이터 타입은 DATE입니다.
-- DATE 타입은 사이즈를 적지 않습니다.
```
> **CREATE TABLE 테이블이름 AS SELECT*FROM 테이블이름**

다음과 같은 명령어를 입력할 경우, 다른 테이블에 있는 값을 그대로 복사하여 가져올 수 있습니다. 

- 단, Primary Key, Index 등등 Object는 복사가 되지 않습니다.

```sql
CREATE TABLE EMP_T2 AS
SELECT*FROM EMP; 
```

![](https://images.velog.io/images/yunyoseob/post/d85bff41-9718-4295-b0ff-534ab85c4973/image.png)

만약, 칼럼만 가져오고 싶다면 WHERE절을 통해, 칼럼만 가져오는 방법도 있습니다.

```sql
CREATE TABLE EMP_T1 AS
SELECT*FROM EMP WHERE 1=2; 
```
![](https://images.velog.io/images/yunyoseob/post/a89019c1-2969-4eeb-b00b-741b86fa1b31/image.png)

- WHERE 절은 참일 경우에만 실행 되므로, 이럴 경우, 칼럼만 가져오게 됩니다.


> **테이블 이름 바꾸기**

RENAME 명령어를 통해 테이블의 이름을 바꿀 수도 있습니다.

```sql
RENAME TEST_T1 TO TEST_1;
```

해당 명령어를 통해 TEST_T1 이라는 테이블이름을 TEST_1이라는 테이블 이름으로 바꿀 수 있습니다.

> **테이블 변경**

ALTER와 ADD 명령어를 통해 테이블에 칼럼을 추가할 수도 있습니다.

```sql
ALTER TABLE TEST_1
ADD TT VARCHAR2(100);
```

데이터 타입이 VARCHAR2이면서 사이즈가 100이고, 칼럼이름이 TT인 칼럼을 TEST_1 테이블에 추가합니다.

- 이 때, 주의해야 할 점은 새로 생성되는 칼럼은 마지막 칼럼으로 생성됩니다.

> **테이블 칼럼 이름 변경**

ALTER와 RENAME 명령어를 통해 칼럼이름을 바꿀 수도 있습니다.

```sql
ALTER TABLE TEST_1
RENAME COLUMN TT TO TT_RENAME;
```

TEST_1 테이블의 TT 칼럼의 이름을 TT_RENAME 칼럼으로 바꿀 수 있습니다.

> **테이블 칼럼 사이즈 변경**

ALTER와 MODIFY 명령어를 통해 테이블의 칼럼 사이즈를 변경할 수 있습니다.

```sql
ALTER TABLE TEST_1
MODIFY TT_RENAME VARCHAR2(200);
```

VARCHAR2(100)인 TT_RENAME 칼럼을 VARCHAR2(200)으로 사이즈를 변경할 수 있습니다.

> **테이블 칼럼 삭제**

ALTER와 DROP 명령어를 통해서 테이블의 칼럼을 삭제 할 수 있습니다.

```sql
ALTER TABLE TEST_1
DROP COLUN TT_RENAME;
```

> **테이블 지우기**

DROP 명령어를 통해 테이블을 DROP 할 수도 있습니다.

```sql
DROP TABLE TEST_1;
```

## DML (데이터 조작어)

DML은 테이블의 데이터를 저장, 수정, 삭제하는 명령어로 INSERT, UPDATE, DELETE 명령어가 있습니다. DML은 다음과 같은 특징이 있습니다.

> **DML 특징**

**1. DML 쿼리의 경우, 트랜잭션은 처리해야 한다.**
**2. DML은 메모리에 적재된다. 이 때, TCL 명령어인 COMMIT을 하지 않을 경우, 외부 응용프로그램에서는 테이블 내용 중 조회가 불가능하다.**
**3. TCL 명령어인 COMMIT을 할 경우, 메모리에 적재된 내용을 파일에 적재하므로, 외부 응용프로그램에서 테이블 내용중 파일에 적재된 내용만 조회가 가능하다.**

> **INSERT**

```sql
CREATE TABLE SCOTT.TEST_2(
    TC2_1 NUMBER(7, 2)
    ,TC2_2 VARCHAR2(30)
    ,TC2_3 DATE
);
```

위의 코드로 TEST_2라는 TABLE을 생성한 뒤, 해당 테이블에 INSERT 명령어를 통해 데이터를 입력할 수 있습니다.

```sql
INSERT INTO TEST_2(TC2_1, TC2_2, TC2_3)
VALUES (1.3, '바차 2 문자열', SYSDATE);
```

**이 때, 유의사항은 칼럼 순서와 데이터 타입에 맞게 데이터를 입력해야 합니다.**

> **DELETE**

DELETE 명령어로 특정 데이터를 삭제할 수 있습니다.

```sql
INSERT INTO TEST_2(TC2_1, TC2_2, TC2_3)
VALUES (1.33, '바차 2 문자열1',SYSDATE);

DELETE FROM TEST_2
WHERE TC2_1 >= 1.32;
```

TEST_2 테이블에 TC2_1 : 1.33, TC2_2 : '바차 2 문자열1', TC2_3 : SYSDATE 데이터가 생성되었다가 DELETE 명령어에서 TC2_1가 1.32 이상이므로, 삭제 되었습니다.

> **UPDATE**

UPDATE 명령어로 특정 데이터를 업데이트 할 수 있습니다.

```sql
INSERT INTO TEST_2(TC2_1, TC2_2, TC2_3)
VALUES (1.33, '바차 2 문자열1',SYSDATE);

UPDATE TEST_2 
SET TC2_1=1.30
WHERE TC2_1>=1.32;
```

TEST_2 테이블에 TC2_1 : 1.33, TC2_2 : '바차 2 문자열1', TC2_3 : SYSDATE 데이터가 생성되었다가 

UPDATE 명령어에서 TC2_1가 1.32 이상이므로, 1.30으로 수정되었습니다.


## TCL (트랜젝션 제어어)

앞서, 언급한 DML의 특징의 경우, 트랜잭션 제어어 없이 외부 응용프로그램에서 테이블 내용 중 파일에 적재된 내용을 조회할 수 없습니다.

또한, DML 명령어로 작업하다가 이전으로 돌아가고 싶을 때에도 TCL 명령어를 통해 돌아갈 수 있습니다.

> **COMMIT**

```sql
INSERT INTO TEST_2(TC2_1, TC2_2, TC2_3)
VALUES (1.33, '바차 2 문자열1',SYSDATE);

UPDATE TEST_2 
SET TC2_1=1.30
WHERE TC2_1>=1.32;

COMMIT;
```

이전의 명령어를 작성한 뒤, COMMIT을 하게 될 경우, 메모리에 적재된 내용을 파일에 적재합니다.

> **ROLLBACK**

```sql
COMMIT;

INSERT INTO TEST_2(TC2_1, TC2_2, TC2_3)
VALUES (1.35, '바차 2 문자열5',SYSDATE);

ROLLBACK;
```

TEST_2 테이블에 TC2_1 : 1.35, TC2_2 : '바차 2 문자열5', TC2_3 : SYSDATE 데이터가 생성했는데, 이를 다시 데이터를 생성하기 전으로 돌리고 싶으면, ROLLBACK 명령어를 사용할 수 있습니다.


**ROLLBACK 명령어는 가장 최근 COMMIT했을 때의 상태로 돌아가게 해주는 명령어 입니다.**


> **주의사항**

COMMIT 명령어를 사용하면, 그 이전상태로 ROLLBACK이 되지 않습니다.

```sql
INSERT INTO TEST_2(TC2_1, TC2_2, TC2_3)
VALUES (1.35, '바차 2 문자열5',SYSDATE);

COMMIT;

ROLLBACK;
```

예시로 위와 같이 쿼리문을 작성하게 된다면, TC2_1 : 1.35, TC2_2 : '바차 2 문자열5', TC2_3 : SYSDATE 데이터가 생성하기 전으로 돌아갈 수 없습니다.


**이상으로 [Oracle DB] SQL 기초문법 2편 포스팅을 마치도록 하겠습니다. 😃**
