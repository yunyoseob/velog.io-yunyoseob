안녕하세요. 😀 오늘은 Oracle DB SQL 기초문법에 대해 포스팅하도록 하겠습니다.

## 들어가기 전에

```sql
version : Oracle Database 11.2.0
```

SQL에서 SELECT 문장은 크게 6개의 절로 구성됩니다.

```sql
SELECT : 테이블에서 데이터 질의하는 키워드 

FROM : 데이터를 조회하고 싶은 테이블의 이름을 정하는 키워드

WHERE : 데이터를 조회하는 조건을 적는 키워드

GRUOP BY : 특정 속성을 기준으로 그룹화 하여 검샋할 때 속성 키워드

HAVING : 그룹 함수를 포함한 조건 키워드

ORDER BY : 정렬시 사용하는 키워드
```

> **SELECT문의 실행 순서**

SELECT문은 **FROM-WHERE-GROUP BY-HAVING-SELECT-ORDER BY** 순으로 실행됩니다.

```sql
1. FROM : 발췌 대상 테이블 참조
2. WHERE : 발췌 대상 데이터가 아닌 것은 제거
3. GROUP BY : 행들을 소그룹화 한다.
4. HAVING :  그룹핑된 값의 조건에 맞는 것만을 출력한다.
5. SELECT : 데이터 값을 출력/계산한다.
6. ORDER BY :  데이터를 정렬한다.
```

> **포스팅에 사용할 테이블**

SQL 프로그램의 최소 단위는 테이블입니다. 테이블은 행(튜플, 레코드)과 열(컬럼, 속성)의 관계로 표현됩니다.

SQL 포스팅에서 다룰 테이블은 EMP 테이블과 DEPT 테이블을 다루도록 하겠습니다.

> **EMP TABLE**

EMP 테이블은 다음과 같이 구성되어 있습니다.

![](https://images.velog.io/images/yunyoseob/post/aebd21b3-dbe0-460e-a3d5-3991ebf24c9c/image.png)


EMP 테이블의 데이터는 다음과 같습니다.

![](https://images.velog.io/images/yunyoseob/post/6c45a099-caf3-4088-aff4-8cb2f6a1ef17/image.png)

EMP 테이블의 제약조건은 다음과 같습니다.

![](https://images.velog.io/images/yunyoseob/post/20664b34-80f1-41b1-85a9-8fe83540abb8/image.png)

기본 키(PK)가 EMPNO이며, 외래 키(FK)가 DEPTNO입니다.

EMP 테이블의 외래 키인 DEPTNO는 DEPT 테이블의 기본 키입니다.

![](https://images.velog.io/images/yunyoseob/post/c43af838-aaf6-4045-a206-9238c69bbd92/image.png)

SCOTT는 계정 이름이며, EMP, DEPT는 테이블 이름 입니다.

> **DEPT TABLE**

DEPT 테이블은 다음과 같이 구성되어 있습니다.

![](https://images.velog.io/images/yunyoseob/post/4bcef7bf-076a-4fd0-aec3-307c37535fb0/image.png)

DEPT 테이블의 데이터는 다음과 같습니다.

![](https://images.velog.io/images/yunyoseob/post/513cbccc-2f70-47f9-9d89-7c4297aba9f7/image.png)

그럼 이제 본격적으로 SQL 기초 문법에 대해 포스팅 하도록 하겠습니다.


## SQL 기초문법 1편

> **테이블의 총 레코드 수 구하기**

테이블 전체를 보고 싶을 때는 FULL SCAN(*) 표시를 통해 볼 수 있습니다.

```sql
SELECT*FROM EMP;
```

테이블 전체의 레코드 수를 보기 위해서는 COUNT() 함수를 사용하여 볼 수 있습니다.

```sql
SELECT COUNT(*) FROM EMP;
-- 14
```

그러나, EMP처럼 소수의 데이터가 아니라 대량의 데이터가 있는 테이블을 다뤄야 할 경우, 이는 비효율적입니다. 이를 더 효율적으로 계산하려면 테이블의 PK의 수를 조회하면 됩니다.

- 이유 : 기본키는 null 값이 입력될 수 없으므로, 테이블의 전체 레코드 수와 동일하게 나오기 때문입니다.


```sql
SELECT COUNT(EMPNO) FROM EMP;
-- 14
```

> **Aliase(별칭) 사용하기**

```sql
SELECT 
        A.EMPNO     AS EMPNO    -- 사원번호
       ,A.ENAME     AS ENAME    -- 사원이름
       ,A.JOB       AS JOB      -- 사원직책
       ,A.MGR       AS MCR      -- 상관사원번호
       ,A.HIREDATE  AS HIREDATE -- 입사일
       ,A.SAL       AS SAL      -- 급여    
       ,A.COMM      AS COMM     -- 수당
       ,A.DEPTNO    AS DEPTNO   -- 부서번호 
FROM 
        SCOTT.EMP A;
```

aliase(별칭)이란 AS 키워드를 사용하여 쿼리에서 반환된 열에 새 이름을 지정하는 것을 해당 열의 별칭 지정(aliasing)이라고 하며, 사용자가 지정한 새 이름을 별칭(aliase)라고 합니다.

> **Aliase(별칭) 주의사항**

```sql
SELECT 
        A.EMPNO     AS EMPNO    -- 사원번호
       ,A.ENAME     AS ENAME    -- 사원이름
       ,A.JOB       AS JOB      -- 사원직책
       ,A.MGR       AS MCR      -- 상관사원번호
       ,A.HIREDATE  AS HIREDATE -- 입사일
       ,A.SAL       AS SAL      -- 급여    
       ,A.COMM      AS COMM     -- 수당
       ,A.DEPTNO    AS DN   -- 부서번호 
FROM 
        SCOTT.EMP A
WHERE DN=10;        
```

해당 문을 실행할 경우 "부서번호" : 부적합한 식별자 오류가 나오게 됩니다. 이유는 SELECT문은 **FROM-WHERE-GROUP BY-HAVING-SELECT-ORDER BY** 순으로 실행되기 때문입니다. 

따라서, 순서를 잘 인지하고 WHERE절에 A.DEPTNO=10으로 다시 입력하면 해결 됩니다.

```sql
SELECT 
        A.EMPNO     AS EMPNO    -- 사원번호
       ,A.ENAME     AS ENAME    -- 사원이름
       ,A.JOB       AS JOB      -- 사원직책
       ,A.MGR       AS MCR      -- 상관사원번호
       ,A.HIREDATE  AS HIREDATE -- 입사일
       ,A.SAL       AS SAL      -- 급여    
       ,A.COMM      AS COMM     -- 수당
       ,A.DEPTNO    AS DN   -- 부서번호 
FROM 
        SCOTT.EMP A
WHERE A.DEPTNO=10; 
```

만약, WHERE절에 꼭 DN으로 작성하여 출력하고 싶다면, FROM절에 서브쿼리문을 사용해서 해결할 수 있습니다.


```sql
SELECT 
         A.EMPNO    -- 사원번호
        , A.ENAME    -- 사원이름
       , A.JOB      -- 사원직책
       , A.MCR      -- 상관사원번호
       ,A.HIREDATE -- 입사일
       , A.SAL      -- 급여    
       , A.COMM     -- 수당
       , A.DN   -- 부서번호 
FROM 
        (SELECT 
        	EMPNO     AS EMPNO    -- 사원번호
       		,ENAME     AS ENAME    -- 사원이름
       		,JOB       AS JOB      -- 사원직책
       		,MGR       AS MCR      -- 상관사원번호
       		,HIREDATE  AS HIREDATE -- 입사일
       		,SAL       AS SAL      -- 급여    
       		,COMM      AS COMM     -- 수당
       		,DEPTNO    AS DN   -- 부서번호 
       FROM  EMP) A
WHERE  A.DN=10;        
```

FROM  절은 WHERE절보다 더 먼저 실행되기 때문입니다.


> **WHERE 절 활용하기**

WHERE절은 조건절로 할용할 수 있습니다. 예시로, 1981년 1월 1일부터 1981년 12월 31일까지 입사한 사원을 조회하는 경우, 다음과 같이 검색할 수 있습니다.

```sql
SELECT A.* FROM SCOTT.EMP A
WHERE  1=1
AND    TO_CHAR(TO_DATE(A.HIREDATE), 'YYYYMMDD') <= TO_CHAR(TO_DATE('1981/12/31'), 'YYYYMMDD')
AND    TO_CHAR(TO_DATE(A.HIREDATE), 'YYYYMMDD') >= TO_CHAR(TO_DATE('1981/01/01'), 'YYYYMMDD'); 
```

SCOTT는 계정, EMP는 테이블 이름, A는 aliase 입니다.

WHERE 절은 반드시 해당 내용이 참일 때만 수행 됩니다. 가령 WHERE 절의 첫 번째가 1=2면 참이 아니기 때무에 실행되지 않습니다. 
( WHERE 절의 1=1은 실무에서는 보안의 위험이 있으므로 사용을 지양합니다.)


TO_DATE는 소괄호 내의 칼럼을 DATE 형식으로 바꾼다는 의미이며, TO_CHAR는 첫 번째 날짜 칼럼을 특정 문자열로 변환하는 함수 입니다.

AND는 전후로 모든 조건이 만족하는 값만 참으로 반환합니다.


> **결측치 대체하기**

사원의 이름별로 급여와 연봉, 수당, 수당을 포함한 연봉을 구한 뒤 이를 내림차순 정렬을 한다고 할 때, COMM (수당) 칼럼의 결측치가 있는 것을 확인 할 수 있습니다.

결측치는 COUNT가 되지 않기 때문에 연산과 카운팅이 불가합니다. 따라서, 결측치를 0으로 바꾸고 SELECT문을 실행시켜줍니다.

```sql
SELECT 
    	 A.ENAME                      AS ENAME  -- 사원이름
        ,A.SAL                       AS SAL    -- 급여
       ,A.SAL * 12                  AS TSAL    -- 연봉
       ,NVL(A.COMM, 0)              AS COMM    -- 수당 
       ,A. SAL * 12 + NVL(COMM, 0)  AS CSAL   -- 수당을포함한 연봉
FROM 
        EMP A
ORDER BY TSAL DESC;     
```

ORDER BY는 정렬 키워드로 DESC는 내림차순 정렬, ASC는 오름차순 정렬을 의미합니다. (DEFAULT값은 ASC입니다.)


> **LIKE**

특정 글자가 들어가는 지 확인하는 키워드에는 LIKE 키워드가 있습니다.

```sql
SELECT ENAME FROM EMP WHERE ENAME LIKE '%S';
SELECT ENAME FROM EMP WHERE ENAME LIKE '_A%';
```

첫 번째 쿼리문은 마지막 글자가 S로 끝나는 사람을 출력시키라는 의미이고,

두 번째 쿼리문은 두 번째 글자가 A인 사람을 출력하라는 의미입니다.


**이상으로 [Oracle DB] SQL 기초문법 1편 포스팅을 마치도록 하겠습니다. 😁**
