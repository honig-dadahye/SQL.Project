# SQL.Project

## < INTRO. SQLD 자격증 취득 >
- 강의 : 제로베이스 SQL 완주반
- 기간 : 2021/7/5(MON) ~ 8/20(FRI)
- 시험일정 : 2021/9/5(SUN)
- 시험결과 : Y

## < DEV. 이론과 실전, 간극을 좁히다. > 
- 교재 : 초보자를 위한 SQL 200제, SQL 시작을 위한 최고의 입문서
- 기간 : 2021/10/25(MON) ~ 12/26(SUN)
- 성장목표 : SQL 실무 시뮬레이션 & Kaggle 데이터 분석 도전
- 증명목표 : SQL 코딩 테스트 & SQLP 자격증 취득

### PART 1 입문. SQL 첫발 내딛기
#### 001. 테이블에서 특정 열(COLUMN) 선택하기
사원테이블에서 사원번호와 이름, 월급을 출력

```sql
SELECT
    empno,
    ename,
    sal
FROM
    emp
;
```

#### 002. 테이블에서 모든 열(COLUMN) 출력하기
사원 테이블을 모든 열(column) 출력

```sql
SELECT
    *
FROM
    emp
;
```

사원 테이블의 모든 열, 추가로 부서번호를 출력
```sql
SELECT
    emp.*,
    deptno
FROM
    emp
;
```

#### 003. 컬럼 별칭을 사용하여 출력되는 컬럼명 변경하기
사원 테이블의 사원번호, 이름, 월급 출력 시 컬럼명 '사원번호' '사원이름' 'Salary'으로 출력

```sql
SELECT
    empno AS 사원번호,
    ename AS "사원 이름",
    sal   AS "Salary"
FROM
    emp
;
```  

#### DAY 01 REVIEW.
a struggle in installing and setting up ORACEL & ORACLE SQL DEVELOPER

a few tips for readibility of SQL script

column alias, double quatation mark for upper/lower case, space, and special characters. (do not ues single quotation mark)

column alias in a formula (not function), avaliavle in ORDER BY clause 

Using ORACLE SQL DEVELOPER KEYBOARD SHORTCUT


#### 004. 연결 연산자 사용하기 ( || )
사원테이블의 이름과 월급을 서로 붙여서 출력

```sql
SELECT
    ename || sal
FROM
    emp;
```

연결 연산자 이용하여 문자열과 연결해서 출력

```sql
SELECT
    ename
    || '의 월급은'
    || sal
    || '입니다.' AS 월급정보
FROM
    emp;
```

#### 005. 중복된 데이터를 제거해서 출력하기 (DISTINCT)
사원테이블에서 중복 데이터 제외하고 직업 출력

```sql
SELECT DISTINCT
    job
FROM
    emp;
```

```sql
SELECT UNIQUE
    job
FROM
    emp;
```
     
#### 006. 데이터를 정렬해서 출력하기 (ORDER BY)
월급이 낮은 순으로 이름과 월급 출력

```sql
SELECT
    ename,
    sal
FROM
    emp
ORDER BY
    sal;

SELECT
    ename,
    sal
FROM
    emp
ORDER BY
    sal asc;

SELECT
    ename,
    sal
FROM
    emp
ORDER BY
    sal ascending;    
```
    
```sql
 SELECT
    ename,
    sal AS 월급
FROM
    emp
ORDER BY
    "월급";
```
    
```sql
SELECT
    ename,
    deptno,
    sal
FROM
    emp
ORDER BY
    2 ASC,
    3 DESC;
```
    
#### 007. WHERE절 배우기 (숫자 데이터 검색)
월급이 3000인 사원들의 이름, 월급, 직업 출력

```sql
SELECT
    ename,
    sal,
    job
FROM
    emp
WHERE
    sal = 3000;
```

WHERE절에서는 컬럼 별칭 사용 X
```sql
SELECT
    ename AS 이름,
    sal   AS 월급
FROM
    emp
WHERE
    월급 >= 3000;
```

#### 008. WHERE절 배우기 (문자와 날짜 검색)  
```sql
SELECT
    ename,
    sal,
    job,
    hiredate,
    deptno
FROM
    emp
WHERE ename = 'SCOTT';
```

현재 접속한 세션의 날짜 형식 조회
```sql
SELECT
    *
FROM
    nls_session_parameters
WHERE
    parameter = 'nls_date_format';
```
    
```sql
SELECT
    ename,
    sal
FROM
    emp
WHERE
    hiredate = '81/11/17';
```
    
#### 009. 산술 연산자 배우기 (*, /, +, -)
```sql
SELECT
    ename,
    sal * 12 AS 연봉
FROM
    emp
WHERE
    sal * 12 >= 36000;
```
 
NVL (컬럼, 0) 
```sql
SELECT
    ename,
    sal,
    nvl(comm, 0),
    sal + nvl(comm, 0)
FROM
    emp
WHERE
    deptno = 10;
```

#### 010. 비교 연산자 배우기 (>, <, >=, <=, =, !=, ^=, <>)
```sql
SELECT
    ename,
    sal,
    job,
    deptno
FROM
    emp
WHERE
    sal <= 1200;
```

#### DAY 02 REVIEW.
single vs double quotation

distinct vs unique

query plan : FROM the first, then WHERE, then SELECT, ORDER BY the last


#### 011. 비교 연산자 배우기 (BETWEEN AND) 두 값 사이의 값들을 검색
월급이 1000에서 3000 사이인 사원들의 이름과 월급 출력
```sql
SELECT
    ename,
    sal
FROM
    emp
WHERE
    sal BETWEEN 1000 AND 3000;
    
SELECT
    ename,
    sal
FROM
    emp
WHERE
    ( 1000 <= sal AND sal <= 3000);    
```
    
월급이 1000 미만, 3000 초과인 사원들의 이름과 월급 출력
```sql
SELECT
    ename,
    sal
FROM
    emp
WHERE
    sal NOT BETWEEN 1000 AND 3000;
    
SELECT
    ename,
    sal
FROM
    emp
WHERE
    ( sal < 1000
      OR 3000 < sal );
```
      
1982년도에 입사한 사원들의 이름과 입사일 출력
```sql
SELECT
    *
FROM
    nls_session_parameters
WHERE
    parameter = 'nls_date_format';

SELECT
    ename,
    hiredate
FROM
    emp
WHERE
    hiredate BETWEEN '82/01/01' AND '82/12/31';
```
    
 #### 012. 비교 연산자 배우기 (LIKE) 문자 패턴이 일치하는 행 검색
 이름의 첫 글자가 S로 시작하는 사원들의 이름과 월급 출력
 ```sql
SELECT
    ename,
    sal
FROM
    emp
WHERE
    ename LIKE 'S%';
```
    
두번째 철자가 M인 사원들의 이름 출력
```sql
SELECT
    ename
FROM
    emp
WHERE
    ename LIKE '_M%';
```
    
이름에 A를 포함하고 있는 사원들의 이름 출력
```sql
SELECT
    ename
FROM
    emp
WHERE
    ename LIKE '%A%';
```

#### 013. 비교 연산자 배우기 (IS NULL) null 값 검색
커미션이 null인 사원들의 이름과 커미션을 출력
```sql
SELECT
    ename,
    comm
FROM
    emp
WHERE
    comm IS NULL;
```    
    
#### 014. 비교 연산자 배우기 (IN) 여러 개의 리스트 값을 검색
직업이 SALESMAN, ANALYST, MANAGER인 사원들의 이름, 월급, 직업을 출력
```sql
SELECT
    ename,
    sal,
    job
FROM
    emp
WHERE
    job IN ( 'SALESMAN', 'ANALYST', 'MANAGER' );
    
SELECT
    ename,
    sal,
    job
FROM
    emp
WHERE
    ( job = 'SALESMAN'
      OR job = 'ANALYST'
      OR job = 'MANAGER' );
```      
      
#### 015. 논리 연산자 배우기 (AND, OR, NOT)   
직업이 SALESMAN 이고 월급이 1200 이상인 사원들의 이름, 월급, 직업을 출력
```sql
SELECT
    ename,
    sal,
    job
FROM
    emp
WHERE
        1200 <= sal
    AND job = 'SALESMAN';
```

#### DAY 03. REVIEW
두 값 사이 검색할 경우, '최소값 < < 최대값' 이 아닌 'between 최소값 and 최대값' '최소값 <= sal and sal <= 최대값'으로 작성해야 함

문자열 : 입사날짜, 이름, job > single quotation mark

%는 와일드 카드 ('S%')
LIKE 연산자가 아닌 = 이퀄 연산자 사용할 경우, 와일드 카드가 아닌 %로 작용.
'%A%' 맨 앞 또는 맨 뒤에 A가 와도 조회 가능

is null : null 은 알 수 없는 값이기 때문에 =  null, != null 등 이퀄 연산자 사용 불가능

산술 연산자 vs 비교 연산자 vs 논리 연산자

1) 산술 연산자 :  * / + -

2) 비교 연산자 : < > <= >= , != ^= <>, between and, like, in, is null  (=< =>)

3) 논리 연산자 : - AND, OR, NOT


#### 016. 대소문자 변환 함수 배우기 (UPPER, LOWER, INITCAP)
대문자, 소문자, 첫 철자만 대문자로 출력

```sql
SELECT
    ename,
    upper(ename),
    lower(ename),
    initcap(ename)
FROM
    emp;

문자 데이터가 대문자인지 소문자인지 확실하지 않을 때
SELECT
    ename,
    sal
FROM
    emp
WHERE
    lower(ename) = 'scott';
```

#### 017. 문자에서 특정 철자 추출하기 (SUBSTR) 
이름 첫 3개 철자만 출력

```sql
SELECT
    substr('smith', 1, 3)
FROM
    dual;
    
--DUAL이라는 테이블은 SYS 사용자가 소유하는 오라클의 표준 테이블로서 오직 한 행(row)에 한 컬럼만 담고 있는 dummy 테이블로서 일시적인 산술연산이나 날짜 연산을 위하여 주로 쓰인다.

 특정 순서 철자부터 끝까지 출력
SELECT
    substr('smith', 2)
FROM
    dual;
``` 

 #### 018. 문자열의 길이를 출력하기 (LENGTH)
 이름을 출력하고 그 옆에 이름의 철자 개수를 출력
 
 ```sql
 SELECT
    ename,
    length(ename)
FROM
    emp;
    
SELECT
    length('abcdef')
FROM
    dual;
```    
    
#### 019. 문자에서 특정 철자의 위치 출력하기 (INSTR)
사원이름 smith에서 알파벳 철자 M이 몇번째 자리에 있는지 출력

```sql
SELECT
    instr('smith', 'm')
FROM
    dual;

-- 대/소문자 구분없이 함수 출력 시 0 출력됨

SELECT
    substr('smtith@gmail.com', instr('smtith@gmail.com', '@') + 1)
FROM
    dual;
```    

#### 020. 문자든 숫자든 특정 철자를 다른 철자로 변경하기 (REPLACCE)
이름과 월급을 출력하되, 숫자0을 *로 출력

```sql
SELECT
    ename,
    replace(sal, 0, '*')
FROM
    emp;
    
SELECT
    ename,
    regexp_replace(sal, '[0-3]', '*') AS salary
FROM
    emp;

SELECT
    replace(ename, 'S', 's')
FROM
    emp;
    
개인정보 마킹하여 출력
SELECT
    replace(ename, substr(ename, - 3), '***')
FROM
    emp;
```    
    
#### 021. 특정 철자를 N개 만큼 채우기 (LPAD, RPAD)
 이름과 월급을 출력하는데, 월급 컬럼의 자릿수를 default 10자리로 하고 남은 자리에 *로 채워 출력
 
```sql 
SELECT
    ename,
    LPAD(sal, 10, '*') as salary1, RPAD(sal, 10, '*')as salary2 
FROM 
    emp;
    
SELECT
    ename,
    sal,
    lpad('★', round(sal / 100), '★')
FROM
    emp;    
    
-- SQL에서 시각화 경우, LPAD(A, B, C) A가 아닌 B에 컬럼 기입하여 출력해야 함  
-- ★ 특수문자로 '' singel quatation 사용 시 문자로 활용 가능함
```

#### 022. 특정 철자 잘라내기 (TRIM, RTRIM, LTRIM)
철자 위치 알아내기 INSTR 위치 기준으로 잘라내기 SUBSTR 가장 끝 철자 잘라내기 TRIM
smith에서 각각 s, h, 양쪽 s 잘라서 출력

```sql
SELECT
    'smith',
    ltrim('smith', 's'),
    rtrim('smihh', 'h'),
    trim('s' from 'smith')
FROM
    emp;
    
-- 가장 끝 철자만 잘라서 출력함.
-- 단, the last & the 2nd last가 같은 철자일 경우, 함께 잘라서 출력됨  
```

#### 023. 반올림해서 출력하기 (ROUND)

```sql
SELECT
    '876.567' AS 숫자,
    round(856.567, 1)
FROM
    dual;
    
SELECT
    sal,
    round(sal, -1)
FROM
    emp;    

-- 876.567은 컬럼 특성이 아닌 숫자 특성이기에 single quatation으로 표현, [숫자]는 문자열이 아닌 컬럼 특성이므로 그대로 기입 가능
-- 단, round 함수 안에서 문자, 철자가 아닌 숫자열이므로 single quatation 안해도 됨. 컬럼도 안해도 됨.
```

#### DAY 04. REVIEW
**ORACLE SQl DEVELOPER Keyborad Shortcut**
- 커밋과 롤백 : F11, F12
- 자동정렬 : ctrl + F7
- 쿼리 히스토리 창 : F8
- 일반행 주석 : ctrl + / 
  범위 주석  :alt + shift + c
- 행 잘라내기 : ctrl + x , ctrl +v
- 대소문자 변경 : 블럭처리 + Alt + '


#### 024. 숫자를 버리고 출력하기 (TRUNC)
숫자 출력 시 특정 자리의 숫자를 버리고 출력

```sql
SELECT
    '876.567' AS 숫자,
    round(876.567, 1)
FROM
    dual;

SELECT
    sal,
    round(sal, - 2)
FROM
    emp;
```

#### 025. 나눈 나머지 값/몫 출력하기 (MOD/FLOOR)
```sql
SELECT
    mod(10, 3)
FROM
    dual;

SELECT
    floor(10/ 3)
FROM
    dual;
```

사원번호 홀짝으로 출력
```sql
SELECT
    empno,
    mod(empno, 2)
FROM
    emp;
```

#### 026. 날짜 간 개월 수 출력하기 (MONTHS_BETWEEN)
이름을 출력하고, 입사 날짜부터 오늘까지 몇 달 근무했는지 출력

```sql
SELECT
    ename,
    round(months_between(sysdate, hiredate) ,0)
FROM
    emp;
    
SELECT
    TO_DATE('2019-06-01', 'rrrr-mm-dd') - TO_DATE('2018-10-01', 'rrrr-mm-dd')
FROM
    dual;
    
 -- TO_DATA 문자를 날짜형 데이터로 변환, '2019-06-01'는 문자형 데이터이기에 sigle quatation 사용. 
 -- 날짜형 데이터로 변환한 뒤 산술 연산 가능함.
```

#### 027. 개월 수 더한 날짜 출력하기 (ADD_MONTHS)
2019년 5월 1일로부터 100달 뒤의 날짜는 어떻게 되는지 출력

```sql
SELECT
    add_months('2019-01-01', 100)
FROM
    dual;

SELECT
    add_months(TO_DATE('2019-01-01', 'rrrr-mm-dd'), 100)
FROM
    dual;

-- 꼭 날짜형으로 바꿔주지 않아도 함수 계산 가능함.
-- 단, 산술 연산을 사용할 시, 꼭 문자형으로 날짜형 데이터로 변환해야 함.
```

#### 028. 특정 날짜 뒤에 오는 요일 날짜 출력하기 (NEXT_DAY)
2019년 5월 22일로부터 바로 돌아올 월요일의 날짜가 어떻게 되는지 출력

```sql
SELECT
    '2019-05-23',
    next_day('2019-05-23', 2)
FROM
    dual;
    

SELECT
    '2019-05-23',
    next_day('2019-05-23', '월요일')
FROM
    dual;
```

#### 029. 특정 날짜가 있는 달의 마지막 날짜 출력하기 (LAST_DAY)
2019년 5월 22일 해당 달의 마지막 날짜가 어떻게 되는지 출력

```sql
SELECT
    '2019-05-22' AS 날짜,
    last_day('2019-05-22') as "마지막 날짜"
FROM
    dual;
    
-- 컬럼 별칭 alias 사용 시, 특수문자/대소문자/공백문자 구별하려면 double quatation 써야 함.
```

#### 030. 날짜, 숫자형 데이터를 문자형으로 변환하기 (TO_CHAR)
이름이 SCOTT인 사원의 이름과 입사요일, 월급을 출력

```sql
SELECT
    ename,
    to_char(hiredate, 'DAY') AS 요일,
    to_char(sal, '999,999')
FROM
    emp
WHERE
    ename = 'SCOTT';
    
SELECT
    ename,
    EXTRACT(YEAR FROM hiredate)  AS 연도,
    EXTRACT(MONTH FROM hiredate) AS 달,
    EXTRACT(DAY FROM hiredate)   AS 요일
FROM
    emp;
```

#### 031. 문자를 날짜형으로 데이터 유형 변환하기 (TO_DATE)
81년 11월 17일 입사한 사원의 이름, 입사일 출력

```sql
SELECT
    ename,
    hiredate
FROM
    emp
WHERE
    hiredate = TO_DATE('81-11-17', 'rr/mm/dd');
    
-- hiredate 날짜형 컬럼의 날짜 형식을 알지 못할 때, 문자 '81-11-17' 데이터를 날짜 데이터로 바꾸면 쉽게 조회 가능
```

#### DAY 05. REVIEW
Partially confused with data types : numeric, date, character

#### 032. 암시적 형 변환 이해하기
```sql
SELECT
    ename,
    sal
FROM
    emp
WHERE
    sal = '3000';
    
-- sal은 숫자형 데이터 컬럼이나 '3000' 문자형을 조회하였어도, 오라클이 암시적으로 숫자형 = 숫자형으로 형 변화하여 출력   
```

#### 033. NULL 값 대신 다른 데이터 출력하기 (NVL, NVL2)
이름과 커미션을 출력하되, 커미션이 NULL인 사원은 O으로 출력

```sql
SELECT
    ename,
    nvl(comm, 0)
FROM
    emp;
```
    
커미션이 NULL이 아닌 사원들은 sal+comm을 출력하고, NULL 사원들은 sal 출력

```sql
SELECT
    ename,
    sal,
    comm,
    nvl2(comm, sal + comm, sal)
FROM
    emp;
```

#### 034.IF문을 SQL로 구현하기 (DECODE)
부서번호가 10번이면 300, 부서번호가 20번이면 400을 나머지 부서 번호는 0을 출력

```sql
SELECT
    deptno,
    decode(deptno, 10, 300, 20, 400,
           0) as 보너스
FROM
    emp;
    
SELECT
    empno,
    decode(mod(empno, 2), 0, '짝수', 1, '홀수',
           0)
FROM
    emp;
    
-- if 조건, else if 조건, else 조건 (default값)
```

#### 035. IF문을 SQL로 구현하기 (CASE)
보너스는 월급이 3000 이상이면 500을 출력, 월급이 2000 이상이고 3000보다 작으면 300을 출력, 월급이 1000 이상이고 2000보다 작으면 200을 출력, 나머지 사원들은 0을 출력

```sql
SELECT
    ename,
    job,
    sal,
    CASE
        WHEN sal >= 3000 THEN
            500
        WHEN sal >= 2000 THEN
            300
        WHEN sal >= 1000 THEN
            200
        ELSE 0 END AS 보너스
FROM
    emp;
    
-- 마지막 else 조건 명시 후, end (as 보너스) 기입해야 함.   
-- 2000 이상 3000보다 작은 경우, 굳이 3000 >= sal >= 2000 이라고 쓰지 않았음. 
-- DECODE는 등호 비교만 가능하지만, CASE는 부등호와 등호 둘 다 가능함
```

이름, 직업, 커미션, 보너스를 출력하되, 보너스는 커미션이 NULL이면 500을 출력하고 NULL이 아니면 0을 출력

```sql
SELECT
    ename,
    job,
    comm,
    CASE
        WHEN comm IS NULL THEN
            500
        ELSE
            0
    END AS 보너스
FROM
    emp;
```

#### 036. 최대값 출력하기 (MAX)
직업이 salesman인 사원들의 직업과 최대 월급을 출력

```sql
SELECT
    job,
    MAX(sal)
FROM
    emp
WHERE
    job = 'SALESMAN'
GROUP BY
    job;
    
-- 여러 개의 행이 출력될 때, 최대/최소 함수는 하나의 값만 출력되기 때문에 에러 발생하여 그루핑해야 함.
-- FROM > WHERE > GROUP BY > SELECT > ORDER BY 순으로 SQL 실행됨.
```

#### 037. 최소값 출력하기 (MIN)
```sql
SELECT
    MIN(sal)
FROM
    emp
WHERE
    1 = 2;


-- 최대/최소 함수는 그룹에서 하나의 값 출력, 즉 그룹함수는 WHERE절이 거짓이어도 결과 항상 결과를 출력함.
-- 이처럼 함수는 no row select이 아닌 항상 결과(NULL값)를 리턴함.
```

#### 038. 평균값 출력하기 (AVG)
NULL값을 0으로 치환해 커미션 평균 출력

```sql
SELECT
    AVG(nvl(comm, 0))
FROM
    emp;
    
-- AVG가 아닌 SUM에서 NVL은 성능만 느려질 뿐이라 사용X
```

#### 039. 토탈값 출력하기 (SUM)
직업과 직업별 토탈 월급을 출력하는데 직업별 토탈 월급이 높은 것부터 출력

```sql
SELECT
    job,
    SUM(sal) AS "토탈 월급"
FROM
    emp
GROUP BY
    job
ORDER BY
    "토탈 월급" DESC;

SELECT
    job,
    SUM(sal) AS "토탈 월급"
FROM
    emp
GROUP BY
    job
HAVING SUM(sal) >= 4000
ORDER BY
    "토탈 월급" DESC;

-- SQL 실행순서에 따라 WHERE절에 그룸함수를 사용할 수 없어 HAVING절 사용해야 함.
-- 오로지 ORDER BY절만 SELECT절 이후에 실행되기 떄문에, 컬럼별칭을 사용 가능함.
```

#### 040. 건수 출력하기 (COUNT)
사원수 카운트, 전체행 카운트 출력

```sql
SELECT
    COUNT(ename)
FROM
    emp;

SELECT
    COUNT(*)
FROM
    emp;
```

#### DAY 06. REVIEW
a few rules based on SQL query order
no group funtion at WHERE query


#### 041. 데이터 분석 함수로 순위 출력하기 (RANK)
직업이 ANALYST, MANAGER인 사원들의 이름, 직업, 월급, 월급의 순위를 출력

```sql
SELECT
    ename,
    job,
    sal,
    RANK()
    OVER(
        ORDER BY
            sal DESC
    ) 월급순위
FROM
    emp
WHERE
    job IN ( 'ANALYST', 'MANAGER' );
    
SELECT
    ename,
    job,
    sal,
    RANK()
    OVER( partition by job
        ORDER BY
            sal DESC
    ) as 월급순위
FROM
    emp;    
```

#### 042. 데이터 분석 함수로 순위 출력하기 (DENSE_RANK)
직업이 ANALYST, MANAGER인 사원들의 이름, 직업, 월급, 월급의 순위를 출력

```sql
SELECT
    ename,
    job,
    sal,
    DENSE_RANK()
    OVER(
        ORDER BY
            sal DESC
    ) 월급순위
FROM
    emp
WHERE
    job IN ( 'ANALYST', 'MANAGER' );
```

월급이 2975인 사원의 순위 출력
```sql
SELECT
    DENSE_RANK(2975) WITHIN GROUP(ORDER BY sal DESC) 월급순위
FROM
    emp
WHERE
    job IN ( 'ANALYST', 'MANAGER' );
    
-- WITHIN GROUP 즉, 어느 그룹 이내 2975 순위가 어떻게 되는지 조회
```

#### 043. 데이터 분석 함수로 등급 출력하기 (NTILE)
이름, 월급, 직업, 월급의 등급을 출력

```sql
SELECT
    ename,
    sal,
    job,
    NTILE(4)
    OVER(
        ORDER BY
            sal DESC NULLS LAST
    )
FROM
    emp;
    
-- 오라클에서는 null이 가장 최상값이므로, nulls last를 기입해야 함.
```

#### 044. 데이터 분석 함수로 순위의 비율 출력하기 (CUME_DIST)
이름과 월급, 월급의 순위, 월급의 순위비율을 출력

```sql
SELECT
    ename,
    sal,
    RANK() OVER(ORDER BY sal DESC),
    CUME_DIST() OVER(ORDER BY sal DESC)
FROM
    emp;
```

####045. 데이터 분석 함수로 데이터를 가로로 출력하기 (LISTAGG)
부서번호를 출력하고, 부서번호 옆에 해당 부서에 속하는 사원들의 이름 가로로 출력

```sql
SELECT
    deptno,
    listagg(ename, ',') within GROUP ( ORDER BY ENAME ASC )
from emp
group by deptno;

SELECT
    deptno,
    LISTAGG(sal, '/') WITHIN GROUP(
        ORDER BY
            sal DESC
        )
FROM
    emp
GROUP BY
    deptno;

--GROUP BY절은 LISTAGG 함수를 사용하려면 필수로 기술해야 하는 절
```

#### 046. 데이터 분석 함수로 바로 전 행과 다음 행 출력하기(LAG, LEAD)
사원번호, 이름, 월급을 출력하고 전/다음 행의 월급을 함께 출력

```sql
SELECT
    empno,
    ename,
    sal,
    lag(sal,1) over (order by sal asc) as previous,
    lead(sal,1) over (order by sal asc) as next
FROM
    emp;

SELECT
    deptno,
    empno,
    ename,
    sal,
    lag(sal,1) over (partition by deptno order by sal asc) as previous,
    lead(sal,1) over (partition by deptno order by sal asc) as next
FROM
    emp;

-- 데이터 분석 함수의 문법 : 함수() over (order by )
-- 데이터 분석 함수의 종류 : 순서, 순위, 가로 나열, 전/다음 행 출력
-- partition by 추가 기입 시, GROUP BY절을 기입하지 않아도 됨. 엄밀히 따지면, GROUP BY절 기입 시, 한 변수 한 행이 나오는 거라 다른 함수임.
```

#### 047. ROW을 COLUMN로 출력하기 (SUM+DECODE)
부서번호, 부서번호별 토탈 월급을 출력하는데, 가로로 출력

```sql
SELECT
    SUM(decode(deptno,10,sal)) as "10",
    sum(decode(deptno,20,sal)) as "20",
    sum(decode(deptno,30,sal)) as "30" 
FROM
    emp;
    
-- 왜 singel이 아닌 double quatation 사용한거지..?
```

#### 048. ROW을 COLUMN로 출력하기 (PIVOT)
부서번호, 부서번호별 토탈 월급을 Pivot 문을 사용하여 출력

```sql
SELECT
    *
FROM
    (
        SELECT
            deptno,
            sal
        FROM
            emp
    ) PIVOT (
        SUM ( sal )
        FOR deptno IN ( 10, 20, 30 )
    );
    
-- PIVOT함수를 사용하려면 FROM절에 필요 컬럼으로만 구성된 테이블 생성해야 함.
```

#### DAY 07. REVIEW
MORE delay in reviewing, MORE unfamiliar with the query


#### 049. COLUMN을 ROW로 출력하기 (UNPIVOT)
이름별 아이템별 건수를 출력

```sql
select *
from order2
unpivot (건수 for 아이템 in (BICYCLE, CAMERA, NOTEBOOK));

-- 값이 아니라 컬럼명/변수명이라 그런지 single quatation이 없는감..? 
-- '건수' '아이템' 임의로 지정한 열이름, 전자는 테이블의 데이터를 세로로 출력, 후자는 테이블의 컬럼명을 세로로 출력
```

#### 050. 데이터 분석 함수로 누적 데이터 출력하기 (SUM OVER)
직업이 ANALYST, MANAGER인 사원들의 사원번호, 이름, 월급, 월급의 누적치를 출력

```sql
SELECT
    empno,
    ename,
    sal,
    SUM(sal) OVER(ORDER BY empno ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) as 누적치
FROM
    emp
WHERE
    job IN ( 'ANALYST', 'MANAGER' );
    
-- UNBOUNDED PRECEDING : 맨 첫번째 행, UNBOUNDED FOLLOWING : 맨 마지막 행, CURRENT ROW : 현재 행
```

#### 051. 데이터 분석 함수로 비율 출력하기 (RATIO_TO_REPORT)
부서번호 20번인 사원들의 사원번호, 이름, 월급 출력하고, 부서 내 자신의 월급비율이 어떻게 되는지 출력

```sql
SELECT
    empno,
    ename,
    sal,
    RATIO_TO_REPORT(sal)
    OVER() AS 월급비율
FROM
    emp
WHERE
    deptno = 20;

-- 함수 문법에서 order by를 작성하지 않아도 되는 분석 함수 등장
```

#### 052. 데이터 분석 함수로 집계 결과 출력하기 (ROLL UP)
직업과 직업별 토탈 월급 출력, 맨 마지막 행에 토탈월급 출력

```sql
SELECT
    job,
    SUM(sal)
FROM
    emp
GROUP BY
    ROLLUP(job);
    
SELECT
    deptno,
    job,
    SUM(sal)
FROM
    emp
GROUP BY
    ROLLUP(deptno, job);    
    
-- GROUP BY ROLLUP 안에는 데이터값(sal,hiredate)의 컬럼은 들어갈 수 없음.    
```

#### 053. 데이터 분석 함수로 집계 결과 출력하기 (CUBE)
직업,직업별 토탈 월급 출력하는데, 첫번째 행에 토탈 월급을 출력

```sql
select job, sum(sal)
from emp
group by cube(job);
```

#### 054. 데이터 분석 함수로 집계 결과 출력하기 (GROUPING SETS)
부서번호와 직업, 부서번호별 토탈월급과 직업별 토탈월급, 전체 토탈월급 출력

```sql
SELECT
    deptno,
    job,
    SUM(sal) AS 토탈월급
FROM
    emp
GROUP BY
    GROUPING SETS ( ( deptno ),( job ), ( ) );
```

#### 055. 데이터 분석 함수로 출력 결과 넘버링하기 (ROW_NUNBER)    
```sql
SELECT
    empno,
    ename,
    sal,
    ROW_NUMBER()
    OVER(
        ORDER BY
            sal DESC
    )
FROM
    emp;
```

#### DAY 08.REVIEW
Recap! Distinction between what i may know and what i really know

#### 056. 출력되는 행 제한하기 (ROWNUM)
사원번호, 이름, 직업, 월급을 상단 5개 행만 출력

```sql
SELECT
    empno,
    ename,
    job,
    sal
FROM
    emp
WHERE
    ROWNUM <= 5;
    
-- ROWNUM은 (*)로 검색해서는 출력되지 않는 감춰진 컬럼, 출력되는 행에 번호를 부여하는 컬럼
```

#### 057. 출력되는 행 제한하기 (SIMPLE TOP-N QUERIES)
월급이 높은 사원순으로 사원번호, 이름, 직업, 월급 4개의 행으로 제한해서 출력

```sql
SELECT
    empno,
    ename,
    job,
    sal
FROM
    emp
ORDER BY
    sal DESC
FETCH FIRST 4 ROWS ONLY;

SELECT
    empno,
    ename,
    job,
    sal
FROM
    emp
ORDER BY
    sal DESC
FETCH FIRST 2 ROWS WITH TIES

SELECT
    empno,
    ename,
    job,
    sal
FROM
    emp
ORDER BY
    sal DESC
OFFSET 3 ROWS;
```

#### 058. 여러 테이블의 데이터를 조인해서 출력하기 (EQUI JOIN)
사원 테이블과 부서 테이블을 조인하여 이름, 부서 위치를 출력

```sql
SELECT
    ename,
    loc
FROM
    emp,
    dept
WHERE
    emp.deptno = dept.deptno;
    
-- 조인 조건 활용 시 테이블 별칭을 사용하는 이유 : 어떤 테이블의 컬럼을 츨력할지 몰라 에러가 남. 테이블 별칭을 접두어로 붙여줌 
```

#### 059. 여러 테이블의 데이터를 조인해서 출력하기 (NON EQUI JOIN)
사원 테이블과 급여 등급 테이블을 조인하여 이름, 월급, 급여 등급을 출력

```sql
SELECT
    e.ename,
    e.sal,
    s.grade
FROM
    emp      e,
    salgrade s
WHERE
    sal BETWEEN s.losal AND s.hisal;
```

#### 060. 여러 테이블의 데이터를 조인해서 출력하기 (OUTER JOIN)
사원 테이블과 부서 테이블을 조인하여 이름, 부서 위치 출력 (BOSTON도 함께 출력)

```sql
SELECT
    e.ename,
    d.loc
FROM
    emp  e,
    dept d
WHERE
    e.deptno (+) = d.deptno;
```

#### 061. 여러 테이블의 데이터를 조인해서 출력하기 (SELF JOIN)
사원 테이블 자기 자신과 조인하여 이름, 직업, 관리자 이름, 관리자 직업을 출력

```sql
SELECT
    e.ename,
    e.job,
    d.ename,
    d.job
FROM
    emp e,
    emp d
WHERE
    e.mgr = d.empno; 
 ```
 
 #### 062. 여러 테이블의 데이터를 조인해서 출력하기 (ON절)
 이름, 직업, 월급, 부서 위치 출력
 
 ```sql
 SELECT
    e.ename,
    e.job,
    e.sal,
    d.loc
FROM
         emp e
    JOIN dept d ON ( e.deptno = d.deptno );
 
-- 오라클 EQUI JOIN vs ANSI/ISO SQL ON절
-- ㄴ 오라클 조인 : EQUI JOIN, NON EQUI JOIN, OUTER JOIN, SELF JOIN
-- ㄴ ANSI/ISO SQL : ON절, LEFT/RIGHT/FULL OUTER JOIN, USING, NATURAL, CROSS
```

#### DAY 09.REVIEW
Deeply and Sincerely understanding ORACLE JOIN vs ANSI/ISO SQL JOIN


#### 063. 여러 테이블의 데이터를 조인해서 출력하기 (WHERE절 대신 USING절)
이름, 직업, 월급, 부서 위치 출력

```sql
SELECT
    e.ename,
    e.job,
    e.sal,
    d.loc
FROM
         emp e
    JOIN dept d USING ( deptno );

-- 테이블명, 테이블 별칭 없이 괄호로 조인 컬럼만 기술
-- EQUI JOIN의 WHERE절에서는 동일 컬럼에 꼭 테이블명을 접두어로 붙여줘야 함
```

#### 064. 여러 테이블의 데이터를 조인해서 출력하기 (NATURAL JOIN)
이름, 직업, 월급과 부서 위치 출력

```sql
SELECT
    e.ename,
    e.job,
    e.sal,
    d.loc
FROM
         emp e
    NATURAL JOIN dept d;

-- 오라클이 동일 컬럼을 알아서 찾아 암시적으로 조인 수행
-- 단, WHERE절에서 검색 조건 사용 시, 동일 컬럼은 절대 테이블명, 테이블 별칭없이 작성해야 함.
-- EQUI JOIN의 WHERE절에서는 동일 컬럼에 꼭 테이블명을 접두어로 붙여줘야 함
```

#### 065. 여러 테이블의 데이터를 조인해서 출력하기 (LEFT/RIGHT OUTER JOIN)
EQUI JOIN으로 조인이 안되는 결과를 포함해 이름, 직업, 월급, 부서위치를 출력

```sql
SELECT
    e.ename,
    e.job,
    e.sal,
    d.loc
FROM
    emp  e
    RIGHT OUTER JOIN dept d ON (e.deptno = d.deptno);
    
SELECT
    e.ename,
    e.job,
    e.sal,
    d.loc
FROM
    emp  e, dept d
WHERE e.deptno (+) = d.deptno;

-- 오라클 OUTER JOIN과 1999 ANSI/ISO RIGHT OUTER JOIN 차이, 먼저 머릿속으로 벤다이어그램을 그려볼 것
```

#### 066. 여러 테이블의 데이터를 조인해서 출력하기 (FULL OUTER JOIN)
이름, 직업, 월급, 부서 위치를 출력

```sql
SELECT
    e.ename,
    e.job,
    e.sal,
    d.loc
FROM
    emp  e
    FULL OUTER JOIN dept d ON ( e.deptno = d.deptno );

-- 오라클에서는 RIGHT OUTER JOIN, LEFT OUTER JOIN 동시에 수행하고픈 경우 UNION(중복제거, 내림차순 정렬)을 수행해야 함
-- 테이블, 컬럼, 절, 연산자, 분석함수 등 SQL 언어적 특성 개념을 갖춰가는 중
```

#### 067. 집합 연산자로 데이터를 위아래로 연결하기 (UNION ALL)
부서번호와 부서번호별 토탈 월급을 출력

```sql
SELECT
    deptno,
    SUM(sal)
FROM
    emp
GROUP BY
    deptno
UNION ALL
SELECT
    to_number(NULL),
    SUM(sal)
FROM
    emp;

-- 컬럼 갯수, 데이터 타입을 맞춰 주기 위해 to_number(null), null as 컬럼명 기입
-- ORDER BY절은 제일 아래쪽 쿼리에만 작성 가능함.
```

#### 068. 집합 연산자로 데이터를 위아래로 연결하기 "중복제거 & 내림차순 정렬" (UNION)
부서 번호와 부서 번호별 토탈 월급 출력

```sql
SELECT
    deptno,
    SUM(sal)
FROM
    emp
GROUP BY
    deptno
UNION
SELECT
    null as deptno,
    SUM(sal)
FROM
    emp;
```

#### 069. 집합 연산자로 데이터의 교집합을 출력하기 "중복제거 & 내림차순 정렬" (INTERSECT)
사원명, 월급, 직업, 부서번호를 출력하되 부서번호 10번, 20번 사원들과 20번, 30번 사원들의 교집합 출력

```sql
SELECT
    ename,
    sal,
    job,
    deptno
FROM
    emp
WHERE
    deptno IN ( '10', '20' )
INTERSECT
SELECT
    ename,
    sal,
    job,
    deptno
FROM
    emp
WHERE
    deptno IN ( '20', '30' );
```
    
#### 070. 집합 연산자로 데이터의 차이를 출력하기 "중복제거 & 내림차순 정렬" (MINUS)
사원명, 월급, 직업, 부서번호를 출력하되 부서번호 10번, 20번 사원들과 20번, 30번 사원들의 차이 출력

```sql
SELECT
    ename,
    sal,
    job,
    deptno
FROM
    emp
WHERE
    deptno IN ( '10', '20' )
MINUS
SELECT
    ename,
    sal,
    job,
    deptno
FROM
    emp
WHERE
    deptno IN ( '20', '30' );
    
-- "중복제거 & 내림차순 정렬" 할 필요가 없다면 UNOIN ALL 집합 연산자를 통해 검색 성능을 높일 수 있음
```

#### DAY 10. REVIEW
SQL TREADMILL, willing to work on it  


#### 071. 서브쿼리 사용하기 (단일행 서브쿼리)
특정 쿼리에서 검색 값(1개의 행)을 받아 다른 쿼리에서 검색
JONES보다 더 많은 월급을 받는 사원들의 이름과 월급 출력
```sql
SELECT
    ename,
    sal
FROM
    emp
WHERE
    sal >= (SELECT
                sal
            FROM
                emp
            WHERE
                ename = 'JONES');
```

#### 072. 서브쿼리 사용하기 (다중행 서브쿼리)
특정 쿼리에서 검색 값(N개의 행)을 받아 다른 쿼리에서 검색
직업이 SALESMAN인 사원들과 같은 월급을 받는 사원들의 이름과 월급을 출력
```sql
SELECT
    ename,
    sal
FROM
    emp
WHERE
    sal IN (SELECT
                sal
            FROM
                emp
            WHERE
                job = 'SALESMAN');

-- 다중행을 리턴할 때 = 이퀄 연산자가 아니라 in 연산자를 활용해야 함
```

#### 073. 서브쿼리 사용하기 (WHERE절 NOI IN)
관리자가 아닌 사원들의 이름과 월급, 직업을 출력
```sql
SELECT
    ename,
    sal,
    job
FROM
    emp
WHERE
    empno NOT IN (
            SELECT
                mgr
            FROM
                emp
            WHERE
                mgr IS NOT NULL);
                
-- 서브쿼리에 null이 리턴되는 경우, 메인 쿼리 결과 출력되지 않음
```

#### 074. 서브쿼리 사용하기 (WHERE절 EIXSTS와 NOI EXISTS)
사원이 존재하는 부서의 부서번호, 부서명, 부서위치를 출력
```sql
SELECT
    deptno,
    dname,
    loc
FROM
    dept d
WHERE
    EXISTS (
        SELECT
            deptno
        FROM
            emp e
        WHERE
            e.deptno = d.deptno);
 
-- WHERE절에 따로 컬럼명 기술없이 바로 EXISTS, NOT EXISTS 기술
-- 부서테이블에도 사원테이블에도 있는 부서번호를 검색 조건으로 작성해야 함.
-- 오답
SELECT
    deptno,
    dname,
    loc
FROM
    dept d
WHERE
    EXISTS (
        SELECT
            deptno
        FROM
            emp e
        WHERE
            e.ename is not null);
```

#### 075. 서브 쿼리 사용하기 (HAVING절)      
직업과 직업별 토탈 월급 출력, 직업이 SALESMAN 사원들의 토탈월급보다 큰 값들만 출력
```sql
SELECT
    job,
    SUM(sal)
FROM
    emp
GROUP BY
    job
HAVING
    SUM(sal) >= (
        SELECT
            SUM(sal)
        FROM
            emp
        WHERE
            job = 'SALESMAN'
    );
    
-- SQL 실행순서로 인해 그룹함수를 이용한 쿼리에서는 WHERE절이 아닌 HAVING절에 서브쿼리 작성해야 함
-- GORUP BY절 제외한 'SELECT문'의 모든 5가지 절(SELECT, FROM, WHERE, HAVIGN, ORDER BY)에서 서브쿼리 사용 가능.
```

#### 076. 서브쿼리 사용하기 (FROM 절 IN LINE VIEW)
이름과 월급, 순위를 출력하는데 순위가 1위인 사원만 출력
```sql
SELECT
    a.ename,
    a.sal,
    a.순위
FROM
    (
        SELECT
            ename,
            sal,
            RANK()
            OVER(
                ORDER BY
                    sal DESC
            ) AS 순위
        FROM
            emp
    ) a
WHERE
    a.순위 = 1;

-- 윈도우 함수/분석 함수는 메인쿼리의 WHERE절에서 사용할 수 없어, 서브쿼리에서 먼저 실행해야 함.
-- 서브쿼리 내에서도 WHERE절에서 윈도우 함수/분석 함수를 활용해 조회할 수 없기에, 메인쿼리에서 새로운 컬럼별칭 활용해 1위조건 검색해야 함.
-- 즉, 윈도우 함수/분석 함수는 메인쿼리, 서브쿼리의 WHERE절에서 사용할 수 없기에, 서브쿼리에서 생성한 컬럼별칭으로 메인쿼리에서 1위조건 검색해야 함.
```

#### 077. 서브 쿼리 사용하기 (SELECT절 스칼라 서브쿼리 단.일.값 조회)
직업이 SALESMAN인 사원들의 이름과 월급 출력하되, 직업이 SALESMAN인 사원들의 최대 월급과 최소 월급도 같이 출력
```sql
SELECT
    ename,
    sal,
    (
        SELECT
            MAX(sal) AS 최대월급
        FROM
            emp
        WHERE
            job = 'SALESMAN'
    ),
    (
        SELECT
            MIN(sal) AS 최소월급
        FROM
            emp
        WHERE
            job = 'SALESMAN'
    )
FROM
    emp
WHERE
    job = 'SALESMAN';

-- 스칼라 서브 쿼리에서는 단일값 조회 가능함. 다중행 or 여러 컬럼 리턴은 불가능함    
-- 2~4행에서 메모리에 올려둔 최대월급, 최소월급을 재출력하는 것으 서브 쿼리 캐싱이라고 함.    
```

#### DAY 11. REVIEW 
FINALLY, sloving the pain of the neck

#### 078. 데이터 입력하기 (INSERT문)
사원번호 2812, 사원이름 JACK, 월급 3500, 입사일 2019년 6월 5일, 직업 ANALYST
```sql
INSERT
    INTO emp (
        empno,
        ename,
        sal,
        hiredate,
        job)
values ( 2812, 'JACK', 3500, TO_DATE('2019/06/05', 'RRRR/MM/DD'),'ANALYST');


INSERT
    INTO emp
values ( 2812, 'JACK','ANALYST', null, TO_DATE('2019/06/05', 'RRRR/MM/DD'), 3500, null, 20);

INSERT
    INTO emp
values ( 2812, 'JACK','ANALYST', '', TO_DATE('2019/06/05', 'RRRR/MM/DD'), 3500, '', 20);

-- DML문(Data Multipulation Language) : INSERT INTO, UPDATE SET, DELETE FROM WHERE, MERGE INTO 
```

#### 079. 데이터 수정하기 (UPDATE문)
SCOTT의 월급은 3200으로 수정
```sql
UPDATE emp
SET
    sal = 3200
WHERE
    ename = 'SCOTT';

-- 데이터를 수정하는 UPDATE문은 모든 절에서 서브 쿼리 작성이 가능함
```

#### 080. 데이터 삭제하기 (DELETE, TRUNCATE, DROP문)
SCOTT 행 데이터 삭제
```sql
DELETE FROM emp
where ename = 'SCOTT';

-- DELETE문 : 저장 공간/구조 남김, 취소/플래쉬백 가능 > DML문
-- TRUNCATE문 : 저장 공간 삭제/ 구조 남김(데이터 삭제하지만 테이블 구조 남김), 취소/플래쉬백 불가능(속도 빠름) > DDL문
-- DROP문 : 저장 공간/구조 삭제, 취소 불가능/플래쉬백 가능(테이블 복구 가능) > DDL문
--- DDL문(DATA Definition Language)은 암시적으로 COMMIT 발생, CREATE/ALTER/DROP/TRUNCATE/RENAME
```

#### 081. 데이터 저장 및 취소하기 (COMMIT or ROLLBACK)
SCOTT의 사원번호, 월급, 부서번호를 입력. 월급을 4000으로 변경했다고 취소
```sql
insert into emp (empno, sal, deptno, ename)
values (1122, 3000, 20, 'SCOTT');

commit;

update emp set sal = 4000
where ename = 'SCOTT';

ROLLBACK;

-- TCL문(Transaction Control Language)문 데이터베이스에 영구히 반영. COMMIT/ROLLBACK/SAVEPOINT
```

#### 082. 데이터 입력, 수정, 삭제 한번에 하기(MERGE)
사원 테이블에 부서 위치 컬럼 추가하고, 부서 테이블을 이용하여 사원의 부서위치 값 갱신
```sql
MERGE INTO emp e
USING dept d
ON( e.deptno =d.deptno)
WHEN MATCHED THEN
UPDATE SET e.loc= d.loc
WHEN NOT MATCHED THEN
INSERT (e.empno, e.deptno, d.loc) VALUES (1111, d.deptno, d.loc)

-- TARGET 테이블과 SOURCE 테이블을 통합 시, 데이터 입력/수정/삭제 한번에 가능
```

#### 083. 락(LOCK)이해하기
데이터 일관성을 유지하기 위해 같은 데이터를 동시에 갱신할 수 없도록 LOCK!
```sql
-- DDL문은 암시적으로 COMMIT 수행하는 반면, DML문은 데이터 갱신 시 COMMIT이나 ROLLBACK을 수행하지 않으면 해당 행 ROCK!
-- 관련 행 전체를 잠그기 때문에, 특정 컬럼이 아닌 전체 컬럼들의 데이터 변경 못하고 WAITING
-- 터미널 2창에서 데이터 변경된 소식을 터미널 1창에서 모를 수도 있어서, 데이터 일관성이 깨질 수도 있어 ROCK!
```

#### 084. 검색하는 행의 락(ROCK) 걸기 (SELECT FOR UPDATE)
JONES의 이름과 월급, 부서번호를 조회/검색하는 동안 다른 세션/터미널 창에서 JONES의 데이터 갱신(수정,삭제 등)하지 못하도록 ROCK!
```sql
SELECT
    ename,
    sal,
    deptno
FROM
    emp
WHERE
    ename = 'JONES'
FOR UPDATE;

-- 조회/검색 중인 세션/터미널 창에서 COMMIT이 수행되어야, 다른 세션/터미널 창에서 데이터 갱신이 가능함
```

#### DAY 12. REVIEW
Beyond writing a complex SQL query, deeply understanding how it works 


#### 085. 서브 쿼리를 사용하여 데이터 입력하기 (INSERT INTO)
emp 테이블 구조를 그대로 복제한 emp2 테이블에 부서번호가 10번인 사원들의 사원번호, 이름, 월급, 부서번호 출력
```sql
INSERT INTO emp2 (empno, ename, sal, deptno)
select e.empno, e.ename, e.sal, e.deptno
from emp e
where e.deptno = 10;

-- VALUES절 대신 서브 쿼리문 기술
-- 기본 INSERT문은 한번에 하나의 행만 데이터 입력 가능함
-- CREATE TABLE문은 테이블 구조만 생성하고 데이터 입력X
-- WHERE 1=1 : 제외조건없이 모든 결과값 리턴, WHERE 1=2 : 아무 결과도 리턴 X
```

#### 086. 서브 쿼리를 사용하여 데이터 수정하기 (UPDATE SET)
직업이 SALESMAN인 사원들의 월급을 ALLEN의 월급으로 변경
```sql
UPDATE emp
SET
    sal = (
        SELECT
            sal
        FROM
            emp
        WHERE
            ename = 'ALLEN')
WHERE
    job = 'SALESMAN';
    
-- SET절 컬럼명 = '값' 대신 서브 쿼리문 기술, 이때 SET (컬럼명1, 컬럼명2) = (서브쿼리문)을 통해 여러개의 컬럼들을 기술하여 한번에 갱신
-- UPDATE문의 모든 구절(UPDATE, SET, WHERE절)에 서브쿼리 사용 가능
```

#### 087. 서브 쿼리를 사용하여 데이터 삭제하기 (DELETE FROM)
SCOTT보다 더 많은 월급을 받는 사원들을 삭제
```sql
DELETE FROM emp
WHERE
    sal > (
        SELECT
            sal
        FROM
            emp
        WHERE
            ename = 'SCOTT');
            
월급이 해당 사원이 속한 부서 번호의 평균 월급보다 크면 삭제

DELETE FROM emp e
WHERE
    e.sal > (
        SELECT
            AVG(m.sal)
        FROM
            emp m
        WHERE
            e.deptno = m.deptno);
            
-- 특정 행에서 부서번호를 서브 쿼리의 m.deptno에 넣고 평균 월급 리턴, 메인 쿼리문 WHERE절 검색조건에 맞으면 삭제
```

#### 088. 서브 쿼리를 사용하여 데이터 합치기 (MERGE INTO, USING ON, WHEN MATCHED, UPDATE/INSERT)
부서테이블에 숫자형으로 SUMSAL(부서 번호별 토탈월급) 추가, 이후 사원 테이블을 이용하여 SUMSAL 컬럼의 데이터를 부서 테이블의 부서 번호별 토탈 월급으로 갱신
```sql
ALTER TABEL dept
ADD sumsla mumber(10);
-- 데이터 입력없이 우선적으로 컬럼 추가, 소스테이블의 함수 데이터값을 새로 생성한 컬럼에 입력할 예정

MERGE INTO dept d USING (   SELECT
                                SUM(sal) AS sumsal
                            FROM
                                emp
                            GROUP BY
                                deptno) as v
ON d.deptno = v.deptno
WHEN MATCHED
UPDATE SET
    d.sumsal = v.sumsal;
-- 타겟 테이블은 dept d, 소스 테이블은 emp e, 소스 테이블에서 sumsal 컬럼만 추출한 테이블 v 

UPDATE dept d
SET d.sumsal = (select sum((sal) fro, emp WHERE e.deptno = d.deptno);
```

#### 089. 계층형 질의문으로 서열을 주고 데이터 출력하기
사원이름, 월급, 직업 출력하되 사원들 간의 서열(레벨)을 같이 출력
```sql
SELECT
    ename,
    level,
    sal,
    job
FROM
    emp
START WITH
    ename = 'KING'
CONNECT BY
    PRIOR empno = mgr;

-- 트리 구조에서 노드(항목) / 레벨(계층) / 루트(최상의 노드) / 부모(상위노드) / 자식(하위노드)
-- START WITH 절에서 루트(최상위) 노드 데이터 지정
-- CONNECT BY 절에서 부모 노드와 자식 노드 간의 관계 지정, 순방향 전개 : prior 자식 = 부모, 부모 = prior 자식
```

#### 090. 계층형 질의문으로 서열을 주고 데이터 출력하기 (전개 과정 중 제외 출력)
BLAKE와 BLAKE의 팀원 모두(직속 부하들) 제외하여 출력
```sql
SELECT
    ename,
    level,
    sal,
    job
FROM
    emp
START WITH
    ename = 'KING'
CONNECT BY
    PRIOR empno = mgr AND ename != 'BLAKE';

-- CONNECT BY절에서 부모, 자식 노드 관계 지정 시, BLAKE 제외하면 BLAKE 사원번호를 MGR 번호로 갖는 직속 부하들은 모두 출력 X
```

#### 091. 계층형 질의눔으로 서열을 주고 데이터 출력하기 (ORDER SIBLINGS BY절)
사원이름, 월급, 직업을 서열과 같이 출력하되, 서열 순서 유지하며 월급 높은 사원부터 정렬
```sql
SELECT
    ename,
    level,
    sal,
    job
FROM
    emp
START WITH
    ename = 'KING'
CONNECT BY
    PRIOR empno = mgr
ORDER SIBLINGS BY sal desc;
```

#### 092. 계층형 질의문으로 서열을 주고 데이터 출력하기 (SYS_CONNECT_BY_PATH 함수)
서열 순서대로 사원이름을 가로로 출력
```sql
SELECT
    ename,
    sys_connect_by_path(ename, ',') AS path
FROM
    emp
START WITH
    ename = 'KING'
CONNECT BY
    PRIOR empno = mgr;
```

#### DAY 13. REVIEW
Consistently remind why I develop SQL analytics skill, imagine specifically business case


#### 093. 일반 테이블 생성하기 (CREATE TABLE)
사원번호, 이름, 월급, 입사일을 저장할 수 있는 테이블 생성 (데이터 입력 X)
```sql
CREATE TABLE emp01
( empno NUMBER(10)
  ename varchar2 (10) 
  sal number(10, 2) 
  hiredate date);
  
-- 테이블 생성 시, 테이블명/컬럼명은 반드시 문자로 시작/30자 이하/대소문자 숫자 포함 가능/특수문자 $_#
-- number(10,2) : 전체 10자리 숫자 허용하되, 그 중 소수점 2자리 허용
-- varchar2(10) : 알파벳 철자 10개 포함. 가변 길이 문자 데이터 유형 vs 고정 길이 문자 데이터 유형 CHAR
-- date 다음에 길이 작성하지 않음.
```

#### 094. 임시 테이블 생성하기 (CREATE TEMPORARY TABLE)
사원번호, 이름, 월급을 저장할 수 있는 테이블 생성, COMMIT할 때까지만 데이터 저장
```sql
CREATE GLOBAL TEMPORARY TABLE emp02
( empno NUMBER(10)
  ename varchar2(10)
  sal number(10,2))
  ON COMMIT DELETE ROWS;  
  
-- GLOBAL TEMPORARY '임시' 테이블임을 명시함.
-- ON COMMIT DELETE ROWS : commit할 때까지만 임시테이블에 입력한 데이터 보관
-- ON COMMIT PRESERVE ROWS : 세션이 종료될 때까지만 임시테이블에 입력한 데이터 보관
```

#### 095. 복잡한 쿼리를 단순하게 하기 (CREATE VIEW AS)
직업이 SALESMAN인 사원들의 사원번호, 이름, 월급, 직업, 부서번호를 출력
```sql
CREATE VIEW emp_view AS
    SELECT
        empno,
        ename,
        sal,
        job,
        deptno
    FROM
        emp
    WHERE
        job = 'SALESMAN';
        
-- CREATE VIEW 테이블명 : view 테이블 생성하지만, 데이터 출력 결과를 보여주진 않음.
-- VIEW 테이블은 보안상 공개하면 안되는 데이터(커미션 등) 제외하고 테이블 데이터를 보여줌.
-- VIEW는 단순히 테이블을 바로보는 객체이기 때문에 수정 가능.(UPDATE문 실행 시, emp_view 테이블 갱신하면 emp 테이블도 갱신됨) 
```

#### 096. 복잡한 쿼리를 단순하게 하기 (CREATE VIEW AS)
부서 번호와 부서 번호별 평균 월급을 출력하는 VIEW 생성
```sql
CREATE VIEW emp_view2 AS
    SELECT
        deptno,
        round(AVG(sal)) 평균월급
    FROM
        emp
    GROUP BY
        deptno;

-- VIEW 쿼리문에 함수, 그룹 함수 사용 시 꼭 컬럼 별칭을 사용해야 함. 
-- 해당 VIEW 테이블을 복합 VIEW라고 하며, 단순하게 쿼리 작성할 수 있으나 수정 불가능 할 수 있음.       
```

#### 097. 데이터 검색 속도를 높이기 (CREATE INDEX ON)
월급을 조회할 때 검색 속도를 높이기 위해 월급에 인덱스 생성
```sql
CREATE INDEX emp_sal 
ON emp(sal);

-- 인덱스명 : 테이블명_컬럼명, 지정문법 : ON 테이블명(컬럼명)
-- 인덱스는 검색속도를 높이는 데이터 베이스 객체(OBJECT). FULL SCAN 없이 인덱스의 ROWID를 통해 INDEX SCAN
-- ROWID는 데이터가 위치가 행의 물리적 주소로 인덱스 테이블의 ROWID 컬럼값으로 구성됨.
```

#### 098. 절대로 중복되지 않는 번호 만들기 (CREATE SEQUENCE)
숫자 1번부터 100까지 출력하는 시퀀스 생성
```sql
CREATE SEQUENCE seq01
START WITH 1
INCREMENT BY 1
MAXVALUE 100
NOCYCLE;

-- 신규 사원번호 생성 시, 사원번호 중 가장 큰 수 조회 후, 더 큰 수를 데이터 입력하기 보단 SEQUENCE 활용
-- SEQUENCE는 데이터 베이스 객체(OBJECT)
-- 생성한 시퀀스 활용하여 데이터 입력 시, INSERT INTO emp02 VALUES(seq01.NEXTVAL, 값, 값)
```

#### 099. 실수로 지운 데이터 복구하기 (FLASHBACK QUERY)
커밋 후 백업을 복구하지 않고 과거 시점의 데이터를 '조회'하는 것 : AS OF TIMESTAMP, 골든타임은 15분
```sql
SELECT
    *
FROM
    emp
as of timestamp ( systimestam - interval '5' mintute)
where ename = 'KING';
```

#### 100. 실수로 지운 데이터 복구하기 (FLASHBACK TABLE)
커밋 후 과거 시점의 데이터를 '복구'하는 것 : TO TIMESTAMP, 골든타임은 15분
```sql
ALTER TABLE emp enable row movemetn;
flashback table emp 
to timestamp ( systimestam - interval '5' mintute);

-- 플래시백 전, 플래시백이 가능한 상태로 변경 : ALTER TABLE 테이블명 ENABLE ROW MOVEMENT
-- 플래시백 후, COMMIT해야 변경된 상태가 데이터베이스에 영구히 반영됨
-- 단, DROP 제외 DDL문, DCL문은 암시적으로 자동 COMMIT 되므로, FLASHBACK 에러 발생
```

#### DAY 14. REVIEW
The very unfamiliar chapter.FLASHBACK


#### 101. 실수로 지운 데이터 복구하기 (FLASHBACK DROP)
DROP된 사원 테이블을 휴지통에서 복원
```sql
FLASHBACK TABLE emp TO BEFORE DROP;

FLASHBACK TABLE emp TO BEFORE DROP RENAME TO emp2;

-- 테이블을 DROP한 경우 테이블이 휴지통(USER_RECYBLEBIN)에 들어가게 됨
-- 커밋 후 백업을 복구하지 않고 과거 시점의 데이터를 '조회'하는 것 : AS OF TIMESTAMP, 골든타임은 15분
-- 커밋 후 과거 시점의 데이터를 '복구'하는 것 : TO TIMESTAMP, 골든타임은 15분 이후 commit 수행
```

#### 102. 실수로 지운 데이터 복구하기 (FLASHBACK VERSION QUERY)
사원 테이블의 데이터가 과거 특정 시점부터 지금까지 어떻게 변경되어 왔는지 이력 정보를 출력
```sql
SELECT ename, sal, versions_starttime, versions_endtime, versions_operation
from emp
versions between timestamp
 to_timestamp ( '기간' , 'RRRR-MM-DD HH24:MI:SS')
 and maxvalue
order by versions_starttime;

-- versions_starttime : 변경시작시간, versions_endtime : 변경종료시간, versions_operation : 변경수행여부
-- "VERSIONS절"에 변경이력 정보를 보고 싶은 기간 지정 : VERSIONS BETWEEN TIMESTAMP  TO_TIMESTAMP (   ) AND MAXVALUE 
```

#### 103. 실수로 지운 데이터 복구하기 (FLASHBACK TRANSACTION QUERY)
사원 테이블을 5분 전으로 되돌리기 위한 DML문 출력
```sql
SELECT undo_SQL
FROM flashback_transaction_query
where table_owner = 'SCOTT1' and table_anme = 'emp'
and commit_SCN between ~ and ~
order by start_timestamp desc;

-- TRANSACTION QUERY 테이블에서 UNDO(취소)할 수 있는 SQL 조회
-- SCN(system change number) commit할 때 생성되는 번호
-- 데이터 베이스 모드를 아카이브 모드로 변경해야 함. 오류 발생 시, DB 복구할 수 있는 로그 정보를 자동으로 저장하게 하는 모드.
-- SQL PLUS에서 DB를 마운트 상태(STARTUP MOUNT ORACLE)로 올린 뒤, 아카이브 모드(DML문이 모두 redo log file에 자동 저장)로 변경 가능.
-- SQL PLUS...?
```

#### 104. 데이터 품질 높이기 (PRIMARY KEY 제약)
PRIMARY KEY 제약으로 특정 컬럼에 중복 X, null X 설정
```sql
CREATE TABLE dept02
 (DEPTNO NUMBER(10) CONSTRANINT dept02_DEPTNO_PK PRIMARY KEY,
  DNAME VARCHAR2(10)
  LOC VARCHAR2(10));
  
 ALTER TABLE dept02
 ADD CONSTRAINT dept02_DEPTNO_PK PRIMARY KEY(DEPTNO);

-- 테이블 생성 시점 제약 설정 : 컬럼명 "데이터유형" CONSTRAINT "제약이름 : 테이블명_컬럼명_제약종류축약어" "제약종류"
-- 테이블 생성 후 제약 설정 : ALTER TABLE 테이블명  ADD CONSTRAINT "제약이름 : 테이블명_컬럼명_제약종류축약어" "제약종류(컬럼명)"
-- 제약 종류와 축약어 : UN(unique) NN(not null) ck(check) FK(foreign kwy, references)
```

#### 105. 데이터 품질 높이기 (UNIQUE 제약)
UNIQUE 제약으로 특정 컬럼에 중복 X 설정
```sql
CREATE TABLE dept03
 (DEPTNO NUMBER(10)
  DNAME VARCHAR2(10) CONSTRAINT dept03_DNAME_UN UNIQUE,
  LOC VARCHAR2(10));
  
ALTER TABLE dept03
ADD CONSTRAINT dept03_DNAME_UN UNIQUE(DNAME); 
  
-- 테이블 생성 시점 제약 설정 : 컬럼명 "데이터유형" CONSTRAINT "제약이름 : 테이블명_컬럼명_제약종류축약어" "제약종류"
-- 테이블 생성 후 제약 설정 : ALTER TABLE 테이블명  ADD CONSTRAINT "제약이름 : 테이블명_컬럼명_제약종류축약어" "제약종류(컬럼명)"
```

#### 106. 데이터 품질 높이기 (NOT NULL)
NOT NULL 제약으로 특정 컬럼에 null X 설정
```sql
CREATE TABLE dept04
 (DEPTNO NUMBER(10)
  DNAME VARCHAR2(10)
  LOC VARCHAR2(10) CONSTRAINT dept04_LOC_NN NOT NULL);

ALTER TABLE dept04
MODIFY LOC CONSTRAINT dept04_LOC_NN NOT NULL;
```

#### 107. 데이터 품질 높이기 (CHECK)
월급이 0에서 6000 사이의 데이터만 입력되거나 수정될 수 있도록 제약 설정
```sql
CREATE TABLE emp02
 (EMPNO NUMBER(10)
  ENAME VARCHAR2(20)
  SAL NUMBER(10) CONSTRAINT demp02_SAL_CK CHECK(SAL BETWEEN 0 an 6000 ));
  
ALTER TABLE emp02
 ADD CONSTRAINT emp02_SAL_CK;
 
-- 테이블 생성 시점 제약 설정 : 컬럼명 "데이터유형" CONSTRAINT "제약이름 : 테이블명_컬럼명_제약종류축약어" "제약종류(컬럼명 BETWEEN ~ and ~)"
-- 테이블 생성 후 제약 삭제 : ALTER TABLE 테이블명  DROP CONSTRAINT "제약이름 : 테이블명_컬럼명_제약종류축약어"
```

#### 108. 데이터 품질 높이기 (FOREIGN KEY)
부서 테이블(부모)에 존재하는 부서번호만, 사원 테이블(자식)에 부서번호(자식키) 입력하는 제약 설정
```sql
CREATE TABLE dept05
 (DEPTNO NUMBER(10) CONSTRAINT dept05_DEPTNO_PK PRIMARY KEY,
  DNAME VARCHAR2(10)
  LOC VARCHAR(10));
  
CREATE TABLE emp03
 (EMPNO NUMBER(10)
  ENAME VARCHAR2(10)
  DEPTNO NUMBER(10) CONSTRAINT emp03_DEPTNO_FK REFERENCES dept05(DEPTNO)
    
ALTER TABLE dept05
 DROP CONSTRAINT dept05_DEPTNO_PK cascade;
 
-- 테이블 생성 시점 제약 설정 : 컬럼명 "데이터유형" CONSTRAINT "제약이름 : 테이블명_컬럼명_제약종류축약어" "제약종류 : REFERENCES 부모 테이블명(부모 컬럼명)"
-- 부모 테이블 참조컬럼에 존재하지 않는 데이터는 자식 테이블에 입력/수정 불가능
-- 부모 테이블 참조컬럼(부모키)은 삭제 불가능, cascade 옵션 작성할 경우 자식 테이블 참조컬럼(자식키) 삭제 가능
-- 부모 테이블 참조컬럼 삭제 : ALTER TABLE 테이블명  DROP CONSTRAINT "제약이름 : 테이블명_컬럼명_제약종류축약어" cascade
```

#### DAY 15.REVIEW
MORE explanation on SPQ PLUS and FLASHBACK(Archive log mode)


#### 109. WITH절 사용하여 성능 높이기 (WITH AS)
동일 SQL 반복될 시, WITH절로 임시 저장 영역에 테이블명 생성
```sql
WITH job_sumsal AS (
    SELECT
        job,
        SUM(sal) AS 토탈
    FROM
        emp
    GROUP BY
        job)
SELECT
    job,
    토탈
FROM
    job_sumsal
WHERE
    토탈 > (
        SELECT AVG(토탈)
        FROM job_sumsal);

-- 임시 저장 영역에 TEMP 테이블 생성, 단 WITH절에서만 사용 가능.
```

#### 110. WITH절 사용하기 (SUBQUERY FACTORING)
서브 쿼리 2개가 서로 데이터를 참고할 수 있게 WITH절에 TEMP 테이블 2개 생성
직업별 토탈 값의 평균값에 3000을 더한 값보다 더 큰 부서 번호별 토탈 월급 출력
```sql
WITH job_sumsal AS (
    SELECT
        job,
        SUM(sal) AS 토탈
    FROM
        emp
    GROUP BY
        job)

DEPT_SUMSAL AS ( SELECT
                     deptno,
                     SUM(sal) AS 토탈
                 FROM
                     emp
                 GROUP BY
                     deptno
                 HAVING
                     토탈 > (
                         SELECT AVG(토탈) + 3000
                         FROM job_sumsal);

-- 원래는 특정 서브 쿼리문의 컬럼을 다른 서브 쿼리문에서 참조하는 것은 불가능
-- SUBQUERY FACTORING : WITH절 쿼리 결과로 임시 테이블 생성
```

#### 111. SQL로 알고리즘 문제 풀기 (구구단 2단 출력)
WITH절과 계층형 질의문을 사용하여 LOOP문 구현
```sql
SELECT
    level AS num
FROM
    dual
CONNECT BY
    level <= 9;

WITH loop_table AS (
    SELECT
        level AS num
    FROM
        dual
    CONNECT BY
        level <= 9)
        
SELECT
    '2' || 'x' || num || '=' || 2 * num AS "2단"
FROM
    loop_table;
    
-- 계층형 쿼리(Hierarchical Query)는 오라클에서만 지원하는 기능
-- 숫자 1~9 출력 결과를 LOOP_TABLE 임시 테이블로 저장
```

#### 112. SQL로 알고리즘 문제 풀기 (구구단 1단 ~ 9단 출력)
```sql
WITH loop_table AS (
    SELECT
        level AS num
    FROM
        dual
    CONNECT BY
        level <= 9)

    GUGU_TABLE AS (
    SELECT
        level + 1 AS gugu
    FROM
        dual 
    connect by level <=8)

SELECT
    to_char(a.num) || 'x' || to_char(b.gugu) || '=' to_char ( B . GUGU * A . NUM ) AS "구구단"
FROM 
    LOOP_TABLE A, GUGU_TABLE B;
```

#### 113. SQL로 알고리즘 문제 풀기 (직각 삼각형 출력)
WITH절과 계층형 질의문, LPAD 사용해 시각화 하기
```sql
SELECT LEVEL as NUM
FROM DUAL
CONNECT BY LEVEL <= 8;

WITH loop_table AS (
    SELECT
        level AS num
    FROM
        dual
    CONNECT BY
        level <= 8)
        
SELECT
    lpad('☆', num, '★') AS star
FROM
    loop_table;

-- LPAD를 이해하기 쉬운 방법으로 SQL 시각화함
```

#### 114. SQL로 알고리즘 문제 풀기 (삼각형 출력)
```sql
undefine 숫자1
undefine 숫자2

WITH loop_table AS (
    SELECT
        level AS num
    FROM
        dual
    CONNECT BY
        level <= &숫자1)
SELECT
    lpad(' ', &숫자2 - num, ' ') || Rpad('☆', num, '★') AS triangle
FROM
    loop_table;
    
-- 공백 문자의 경우, ''가 아닌 ' '로 작성해야 정상 출력 됨
-- 두번째 LPAD, RPAD 함수는 거꾸로 작성되는지 이해가 안됨...
-- 치환변수(&)를 사용하면, 입력받은 숫자만금 SQL 시각화함
-- 치환변수 초기화 : undefine 숫자1/p_num, 쿼리 내 치환변수 입력 방법 : &숫자1, &p_num
```

#### 115. SQL로 알고리즘 문제 풀기 (마름모 출력)
WITH절과 LPAD, UNION ALL 사용하여 마름모 출력 (LOOP문, 임시 저장 테이블 사용 X)
```sql
UNDEFINE p_num 
accept p_num prompt '숫자 입력' 

SELECT
    lpad(' ', &p_num - level, ' ')
    || lpad('☆', level, '☆') AS allosy
FROM
    dual
CONNECT BY
    level <= &p_num
UNION ALL
SELECT
    lpad(' ', level - 1, ' ')
    || lpad('★', &p_num + 1 - level, '★') AS allosy
FROM
    dual
CONNECT BY
    level <= &p_num;
    
-- SQL PLUS 명령어 하지 않을 경우, 치환변수/호스트변수/외부변수 입력횟수만큼 ENTER VALUE 프롬프르창이 뜸
-- promt로 '숫자 입력 :'을 화면에 출력하고 accept는 값을 받아 p_num 변수에 담아 출력
```

#### 116. SQL로 알고리즘 문제 풀기 (사각형 출력)
WITH절과 계층형 질의문 사용하여 사각형 출력
```sql
undefine p_num1
undefine p_num2
ACCEPT p_num1 prompt '세로는요?'
ACCEPT p_num2 prompt '가로는요?'

WITH LOOP_TABLE AS (SELECT LEVEL FROM DUAL CONNECT BY level <= &p_num1)

SELECT LPAD ('♥', &p_num2,'♥')
from LOOP_TABLE;

-- ACCEPT문 : ACCEPT 호스트 변수 prompt '메세지' ;
```

#### Day 16. REVIEW
Finally reach to Algorithm definetely with easy and basic one

#### 117. SQL로 알고리즘 문제 풀기
계층형 질의문과 집계 함수를 활용해 1부터 10까지의 합 출력
```sql
undefine p_num
ACCEPT p_num prmpt '숫자는요?'

SELECT SUM(LEVEL) as 합계
FROM DUAL
CONNECT BY LEVEL <= &p_num;
```

#### 118. SQL로 알고리즘 문제 풀기
계층형 질의문과 LN, EXP함수를 활용해 1부터 10까지의 곱 출력
```sql
undefine p_num
ACCEPT p_num prompt '숫자는요?'

SELECT ROUND(EXP(SUM(LN(LEVEL)))) as 곱
FROM DUAL
CONNECT BY LEVEL <= &p_num;


-- ln함수 : 밑수가 자연상수(e)인 로그 함수
-- exp함수 : 자연상수의 제곱으로 만들어주기 위한 함수
-- round함수를 하지 않으면 저 소수 밑자리에서 11값이 등장함
```

#### 119. SQL로 알고리즘 문제 풀기
계층형 질의문으로 1부터 10까지 짝수만 출력
```sql
undefine p_num
ACCEPT p_num prompt '숫자는요?'

SELECT LISTAGG(LEVEL, ',') as 짝수
FROM DUAL
WHERE mod(LEVEL, 2) = 0
CONNECT BY LEVEL <= &p_num;
```

#### 120. SQL로 알고리즘 문제 풀기
WITH절과 계층형 질의문을 활용해 1부터 10까지 소수만 출력
```sql
undefine p_num
ACCEPT p_num prompt '숫자는요?'

WITH LOOP_TABLE AS (SELECT LEVEL as NUM
                    FROM DUAL
                    CONNECT BY LEVEL <= &p_num)

SELECT L1.NUM as 소수
FROM LOOP_TABLE L1, LOOP_TABLE L2
WHERE mod(L1.NUM, L2.NUM) = 0
GROUP BY L1.NUM
HAVING COUNT(L1.NUM) = 2;

-- 약수 : MOD(A, B) = 0, B는 A의 약수이다.
-- 자기 자신의 수로 mod함수 사용하기 위해 셀프 조인 활용
```

#### 121. SQL로 알고리즘 문제 풀기 (최대 공약수)
```sql
undefine p_num1
undefine p_num2
ACCEPT p_num1 prompt '숫자1 은요?'
ACCEPT p_num2 prompt '숫자2 는요?'

WITH LOOP_TABLE AS (SELECT LEVEL as NUM
                     FROM DUAL
                     CONNECT BY LEVEL <= &p_num2)
         
SELECT max(NUM) as 최대공약수          
FROM LOOP_TABLE   
WHERE mod(&p_num1, NUM) = 0
  and mod(&p_num2, NUM) = 0;    
  
-- 계층형 질의문의 CONNECT BY절은 WITH문 or SELECT문에서 등장할 수 있음 
-- GROUP BY NUM 함수 활용 시, 최대공약수 8이 아닌 모든 공약수가 출력됨
```

#### 122. SQL로 알고리즘 문제 풀기 (최소 공배수)
```sql
undefine p_num1
undefine p_num2
ACCEPT p_num1 prompt '숫자1 은요?'
ACCEPT p_num2 prompt '숫자2 는요?'

WITH LOOP_TABLE AS (SELECT LEVEL as NUM
                     FROM DUAL
                     CONNECT BY LEVEL <= &p_num2)
         
SELECT max(NUM) as 최대공약수, 
       (max(NUM) * (&p_num2/max(NUM)) * (&p_num1/max(NUM))) as 최소공배수          
FROM LOOP_TABLE   
WHERE mod(&p_num1, NUM) = 0
  and mod(&p_num2, NUM) = 0;    
  
-- 최소 공배수 = 최대 공약수 * (숫자1/최대 공약수) * (숫자2/최대 공약수)
```

#### 123. SQL로 알고리즘 문제 풀기 (피타고라스의 정리)
CASE문과 POWER함수를 사용해 직각삼각형 여부를 출력
```sql
ACCEPT p_num1 prompt '밑변은요?'
ACCEPT p_num2 prompt '높이는요?'
ACCEPT p_num3 prompt '빗변은요?'

SELECT CASE WHEN
            (power(&p_num1,2) + power(&p_num2,2) = power(&p_num3,2) )
            THEN '직각삼각형이 맞습니다.'
            ELSE '직각삼각형이 아닙니다.' END AS "피타고라스의 정리"
FROM DUAL;

-- undefine문 없이 ACCEPT문만으로 작성 가능
-- POWER함수 : 지수함수 power(밑, 지수)
-- CASE문에서 문자 데이터 출력 시, single quatation 작성해야 출력됨
```

#### 124. SQL로 알고리즘 문제 풀기 (몬테카를로 알고리즘)
피타고라스의 정리, DBMS_RANDOM 패키지와 계층형 질의문으로 원주율 출력
```sql
SELECT SUM( CASE WHEN ( power(num1,2) + power (num2,2) <=1
                 THEN 1
                 ELSE 0 END) ) /100000 *4 as 원주율
FROM (SELECT DBMS_RANDOM.VALUE(0,1) as num1
             DBMS_RANDOM.VALUE(0,1) as num2
      FROM DUAL
      CONNECT BY LEVEL < 100000);

-- 난수 : 특정한 배열순서나 규칙을 가지지 않는 연속적인 임의의 수
-- 원주율 : 원의 지름에 대한 둘레의 비율, 원의 지름에 대한 넓이의 비율
-- 몬테카를로 알고리즘은 난수를 이용하여 알고자 하는 값을 확률적으로 계산해 내는 알고리즘
-- DMBS_RANDOM 패키지는 난수를 생성하는 패키지, VALUE로 숫자 구간을 설정하고 CONNECT BY LEVEL문으로 갯수 설정
-- FROM절에서 계층형 질의문 활용
```

#### 125. SQL로 알고리즘 문제 풀기 (오일러 상수 자연상수 구하기)
POWER 함수, 계층형 질의문, 몬테카를로 알고리즘을 이용하여 자연상수 e값(2.718...) 출력
```sql
WITH LOOP_TABLE as (SELECT LEVEL as NUM
                    FROM DAUL
                    CONNECT BY LEVEL <= 1000000)

SELECT e값
FROM (
    SELECT NUM, POWER(1+1/NUM),NUM) as e값
    FROM LOOP_TABLE)
WHERE NUM =1000000;    

-- NUM(난수)가 1000000 조건을 적용하기 위해 FROM절에 서브쿼리문 작성 
-- 오일러 상수 : POWER(1+1/NUM),NUM)
-- SQL문은 꼭 난수가 필요한가?
```

#### DAY 17. REVIEW
Deep and Concise Questions!


#### 126. 엑셀 데이터를 DB에 로드하는 방법
CSV파일을 오라클 데이터 베이스에 입력
```sql
CREATE TABLE POLLUTION
(측정일시   DATE,
 측정소명   VARCHAR(2),
 이산화질소농도   NUMBER(10,3),   
 오존농도        NUMBER(10,3),  
 이산화탄소농도   NUMBER(10,1),
 아황산가스      NUMBER(10,3),
 미세먼지        NUMBER(10),
 초미세먼지      NUMBER(10));
 
ALTER TABLE POLLUTION MODIFY 측정소명 VARCHAR(20);
 
SELECT  * 
FROM    POLLUTION
WHERE   측정소명 in ( '강동구', '강남구' );
 
-- '측정소명' 컬럼 데이터 타입 변경 : VARCHAR(2) > VARCHAR(20)
```

#### 127. 텍스트에서 가장 빈도수가 높은 단어 출력
스티브 잡스 연설문에서 가장 많이 나오는 단어 조회 (REGEXP_SUBSTR)
```sql
CREATE TABLE SPEECH
( SPEECH_TEXT   VARCHAR2(1000));

SELECT  count(*)
FROM    SPEECH;

SELECT word, count(*)
FROM (
    SELECT  REGEXP_SUBSTR( lower(SPEECH_TEXT), '[^ ]+', 1, a) word 
    FROM    SPEECH, 
            (SELECT level a
            FROM    DUAL
            CONNECT BY level <=52) )
WHERE    word is not null
GROUP BY word
ORDER BY count(*) desc;
        
-- 텍스트 길이 10000은 너무 길어 오류(ORA-00910) 발생
```

#### 128. 텍스트에서 긍정 단어, 부정 단어 건수 출력 (다중 로우 서브 쿼리문)
```sql
CREATE TABLE POSITIVE ( P_TEXT VARCHAR2(2000));
CREATE TABLE NEGATIVE ( N_TEXT VARCHAR2(2000));

CREATE VIEW SPEECH_VIEW
AS
    SELECT  REGEXP_SUBSTR( lower(SPEECH_TEXT), '[^ ]+', 1, a) word 
    FROM    SPEECH, 
            (SELECT level a
            FROM    DUAL
            CONNECT BY level <=52);
            
SELECT count(word) as 긍정단어
FROM SPEECH_VIEW
WHERE lower(word) IN (SELECT lower (p_text)
                      FROM positive) ;  

-- 1) 영어 긍정 단어와 부정 단어를 저장하기 위한 테이블을 생성
-- 2) 심플 작성을 위해 127 VIEW 생성
-- 3) 긍정단어 테이블을 서브 쿼리문으로 작성하여 긍정단어 수 조회
```

#### 129. 절도가 많이 발생하는 요일은 언제인가? (unpivot, rank)
```sql
CREATE TABLE CRIME_DAY
(CRIME_TYPE VARCHAR2(50),
 SUN_CNT    NUMBER(10),
 MON_CNT    NUMBER(10),
 TUE_CNT    NUMBER(10),
 WED_CNT    NUMBER(10),
 THU_CNT    NUMBER(10),
 FRI_CNT    NUMBER(10),
 SAT_CNT    NUMBER(10),
 UNKNOWN_CNT    NUMBER(10)) ;
 
 CREATE TABLE UNPIVOT
 AS
    SELECT *
    FROM CRIME_DAY
    UNPIVOT ( CNT FOR DAY_CNT IN (SUN_CNT, MON_CNT, TUE_CNT, WED_CNT, THU_CNT, FRI_CNT, SAT_CNT)) ;
 
 SELECT *
 FROM (
     SELECT     DAY_CNT, CNT, RANK () OVER (ORDER BY CNT DESC) as RNK
     FROM       UNPIVOT
     WHERE      TRIM(CRIME_TYPE) = '살인')
 WHERE RNK =1;
 
 -- unpivot문으로 요일 컬럼을 로우로 검색한 데이터로 crime_day_unpivot 테이블 생성
 -- 특정 범죄(절도)로 조회한 뒤, CNT 순위의 컬럼명 지정(RNK)
 ```
 
 #### 130. 우리나라에서 대학 등록금이 가장 높은 학교는 어디인가?
 데이터셋 : 공공 데이터 포털에서 '대학등록금' 검색
 ```sql
 CREATE TABLE UNIVERSITY_FEE
 (DIVISION      VARCHAR2(20),
  TYPE          VARCHAR2(20),
  UNIVERSITY    VARCHAR2(60),
  LOC           VARCHAR2(40),
  ADMISSION_CNT NUMBER(20),
  ADMISSION_FEE NUMBER(20),
  TUITION_FEE   NUMBER(20));
  
  -- 대학명, 지역명은 데이터 유형 60,40까지 지정해야 함.
  -- 빈번히 까먹는 컬럼명, 컬럼 데이터 유형 지정 후 ',' 작성해야 함

SELECT  *  
FROM (
      SELECT UNIVERSITY, TUITION_FEE, RANK() OVER (ORDER BY TUITION_FEE DESC NULLS LAST) 순위
      FROM  UNIVERSITY_FEE)
WHERE   순위 = 1 ; 

-- 오라클에서 순위 정렬 시, null값이 자동적으로 가장 높은 값으로 인식됨.(2차 반복!)
```

#### 131. 서울시 물가 중 가장 비싼 품목과 가격은 무엇인가?
데이터셋 : 공공 데이터 포털에서 '서울시 농수산물 가격' 검색
```

CREATE TABLE SEOUL_PRICE
( P_SEQ    number(20),
  M_SEQ    number(20),
  M_NAME   varchar2(30),
  A_NAME   varchar2(30),
  A_PRICE  number(30));
  
 SELECT A_NAME, A_PRICE, M_NAME
 FROM   SEOUL_PRICE
 WHERE  A_PRICE = ( SELECT MAX(A_PRICE)
                    FROM    SEOUL_PRICE);
                    
-- WHERE절에서 집계 함수(MAX, MIN)를 활용한 서브쿼리문 작성하는 아이디어
-- 만약 일일이 insert문을 작성하여 데이터 입력 시, 임의적으로 컬럼 선택/제외하지 않을 것
```

#### 132. 살인이 가장 많이 발생하는 장소는 어디인가?
데이터셋 : 공공 데이터 포털에서 '범죄발생장소' 검색
```sql
CREATE TABLE CRIME_LOC
( TYPE    VARCHAR2(100),
  LOC     VARCHAR2(100),
  CNT     NUMBER(10));  
  
SELECT  *
FROM    (SELECT LOC, CNT, RANK () OVER (ORDER BY CNT DESC) 순위 
         FROM CRIME_LOC
         WHERE TYPE = '살인')
WHERE   순위 = 1;

-- 범죄발생장소 데이터의 경우, 대부분 구체적인 장소명들이 열 나열이라 데이터 임포트가 어려움
```

#### DAY 18. REVIEW
To kaggle out data set and make the point


#### 133. 가정불화로 생기는 가장 큰 범죄 유형은 무엇인가?
데이터셋 : 공공 데이터 포털 사이트에서 범죄유형과 범죄원 검색
```sql
CREATE TABLE CRIME_REASON
(범죄유형 VARCHAR2(30),
 생계형  number(10),
 유흥 number(10),
 도박 number(10),
 허영심 number(10),
 복수  number(10),
 해고  number(10),
 징벌 number(10),
 가정불화  number(10),
 호기심 number(10),
 유혹  number(10),
 사고   number(10),
 불만   number(10),
 부주의   number(10),
 기타   number(10)  );

CREATE TABLE CRIME_REASON2
AS
    SELECT  *
    FROM    CRIME_REASON1
    UNPIVOT ( CNT FOR TERM IN (생계형, 유흥, 도박, 허영심, 복수, 해고, 징벌, 가정불호, 호기심, 유혹, 사고, 불만, 부주의, 기타)); 

SELECT  범죄 유형
FROM    CRIME_REASON2
WHERE   CNT = (SELECT   MAX(CNT)
               FROM     CRIME_REASON2
               WHERE    TERM = '가정불화')
        AND TERM = '가정불화';       

-- unpivot문(CREATE TABLE AS)으로 범죄 동기 컬럼(열)을 로우(행)으로 조회한 데이터 테이블 생성
-- unpivot문은 열을 행의 집합으로, pivot문은 행을 열의 집합으로 조회
```

#### 134. 방화 사건의 가장 큰 원인은 무엇인가?
```sql
SELECT  범죄 유형 as 방화 원인
FROM    CRIME_REASON2
WHERE   CNT = (SELECT   MAX(CNT)
               FROM     CRIME_REASON2
               WHERE    TERM = '방화')
        AND TERM = '방화';  
```

#### 135. 한국에서 교통사고가 가장 많이 발생하는 지역은?
```sql
CREATE TABLE ACC_LOC
(ACC_LOC    varchar2(200),
 ACC_CNT    number(20));
 
SELECT  *
FROM    (SELECT ACC_LOC, ACC_CNT, DENSE_RANK() OVER(ORDER BY ACC_CNT DESC NULLS LAST) as 순위
         FROM ACC_LOC)
WHERE   순위 <= 5 ;
```

#### 136. 치킨집 폐업이 가장 많았던 연도가 언제인가?
```sql
CREATE TABLE CHI_CLOSING
(연도     NUMBER(10),
 치킨집    NUMBER(10)); 
 
SELECT  *
FROM    CHI_CLOSING
WHERE   치킨집 = (SELECT MAX(치킨집)
                 FROM   CHI_CLOSING);
                 
SELECT  *
FROM    (SELECT 연도, 치킨집, RANK() OVER (ORDER BY 치킨집 DESC) 순위
         FROM CHI_CLOSING)
WHERE   순위 = 1;         

-- 1) WHERE 절의 서브 쿼리문에서 최대값 조회하는 방법
-- 2) FROM 절의 서브 쿼리문에서 rank 함수 활용하는 방법
```

#### 137. 세계에서 근무 시간이 가장 긴 나라는 어디인가?
데이터셋 : 통계청 KOSIS 국가 통계포털 "근로시간" 검색
```sql
CREATE TABLE WORKING_TIME
(국가별    VARCHAR2(20),
 "2014"     NUMBER(30),  
 "2015"     NUMBER(30),
 "2016"     NUMBER(30),
 "2017"     NUMBER(30),  
 "2018"     NUMBER(30));
 
ALTER TABLE WORKING_TIME
MODIFY 국가별 VARCHAR2(30);

CREATE VIEW WORKING_TIME2
AS
    SELECT  *
    FROM    WORKING_TIME
    UNPIVOT ( CNT FOR YEAR IN ("2014", "2015", "2016", "2017", "2018"));
     
SELECT  국가별, CNT, RANK () OVER (ORDER BY CNT DESC) 순위
FROM    WORKING_TIME2
WHERE   YEAR = 2018 ; 

-- 컬럼이었던 2014~2018이 로우(행)으로 가면서 새로운 컬럼명 생성 : YEAR
```

#### 138. 남자와 여자가 각각 많이 걸리는 암은 무엇인가?
```sql
CREATE TABLE CANCER
(TYPE    varchar2(50),
 PATIENT number(20),
 SEX     varchar2(30));
 
SELECT  distinct(type),sex, patient
FROM    CANCER
WHERE   patient = (SELECT max(patient)
                   FROM   CANCER
                   WHERE  sex = '남자' and type != '모든암' )   
UNION ALL
SELECT  distinct(type),sex,  patient
FROM    CANCER
WHERE   patient = (SELECT max(patient)
                   FROM   CANCER
                   WHERE  sex = '여자' );   
    
-- distinct 컬럼이라기 보단 SELECT distinct(기준 컬럼) 으로 작성해야 함   
```

#### DAY 19.REVIEW
DEALT with unkind dataset using UNPIVOT


#### 139. PL/SQL 변수 이해하기 (dbms_output.put_line)
```sql
set serveroutput on
accept p_num1 prompt '첫 번째 숫자를 입력하세요 ~'
accept p_num2 prompt '두 번째 숫자를 입력하세요 ~'

declare 
    v_sum   number(10);
begin
    v_sum   := &p_num1 + &p_num2 ;
    dbms_output.put_line('총합은:' || v_sum);
end;
/

-- 명령 프롬프트에서 sqlplus 계정명/비밀번호 입력 후 SQL*PLUS 프롬프트 실행(SQL 명령문 기능 & Oracle 환경 설정 기능 제공)
-- SQL*PLUS 프롬프트에서 edit p139 작성 후 엔터 > 메모장에 예제 저장 후 닫기 > 프롬프트 창에서 @p.139 스크립트 실행
-- PL/SQL은 Procedure Language SQL 약자. 비절차적인 언어인 SQL에 프로그래밍 요소를 가미해서 절차적으로 처리하는 데이터 베이스 프로그래밍 언어
-- 절차적 언어란 개발자가 처리 절차(순서, 방법)을 처음부터 끝까지 정해주는 언어 COBAL JAVA C.
-- 비절차적 언어란 개발자가 처리절차를 지정하지 않고 원하는 결과(무엇)만 정의하여 요청하는 언어
-- set serveroutpuut on 설정 후, dbms_output.putline( ) : 변수에 있는 값을 화면에 출력하는 put_line함수
-- declare 선언절 : 변수, 상수, 커서, 예외 등 선언 / ;으로 종료
-- begin 실행절 : 할당 연산자(:=) / ;으로 종료
-- end; 절 : PL/SQL 블록 종료 
-- / : PL/SQL문 종료
-- 성공적으로 실행 시 "PL/SQL 프로시저가 성공적으로 완료되었습니다"라고 워크시트에 노출됨
```

#### 140. PL/SQL 변수 이해하기 (SELECT INTO 절)
```sql
set serveroutput on
accept p_empno prompt '사원 번호를 입력하세요~'

declare
    v_sal number(10);
begin
    select sal into v_sal
    from emp
    where empno = &p_empno;
    dbms_output.put_line('해당 사원의 월급은' || v_sal);

end;
/

-- ORA-01403 오류 : 데이터를 찾을 수 없다고 뜨는데..?
```

#### 141. PL/SQL IF 이해하기 (블록 내에서의 제어문, IF ~ ELSE문)
```sql
set serveroutput on
set verify off
accept p_num prompt '숫자를 입력하세요!'
begin
    if mod(&p_num,2)=0 then
     dbms_output.put_line ('짝수입니다');
    else 
     dbms_output.put_line ('짝수입니다');
    end if;
end;
/

-- set verify on/off : 명령어나 PL/SQL에서 &치환 변수를 사용할 때, 치환 전후의 자세한 값의 표시 여부 지정, 기본값은 ON
```

#### 142. PL/SQL IF 이해하기 (IF ~ELSE ~ ELSE문)
이름을 입력받아 사원의 월급이 3000이상이면 고소득자, 2000 이상이고 3000보다 작으면 중간소득자, 2000보다 작으면 저소득자 메세지 출력
```sql
set serveroutput on
set verify off
accept p_name prompt '사원 이름을 입력하세요!'

declare
    v_ename emp.ename%type := upper('&p_name');
    v_sal   emp.sal%type;
    
begin
    select sal into v_sal
    from emp
    where ename = v_ename;
    
    if v_sal >= 3000 then
     dbms_output.put_line('고소득자');
    elsif v_sal >= 2000 then
     dbms_output.put_line('중간소득자');
    else 
     dbms_output.put_line('저소득자');
    end if; 
    
end;
/
 
-- SQL 프롬프트에서 사원이름을 입력받아 p_name 외부변수에 저장
-- %type : 기존 테이블의 컬럼 데이터 유형을 PL/SQL 프로그램의 변수의 데이터 유형으로 설정
-- if ~ elsif ~ else ~ end if
```

#### 143. PL/SQL basic loop 이해하기(Loop ~ exit when 조건 ~ end loop;)  
```sql
declare
    v_count number(10) := 0;

begin
    LOOP 
     v_count := v_count +1;
     dbms_output.put_line ('2 X ' || v_count || ' = ' || 2*v_count);
    EXIT WHEN v_count = 9;
    END LOOP;

end;
/

-- set serveroutput on문과 accept v_count prompt문이 등장하기 않는 이유는?
```

#### 144. PL/SQL While Loop 이해하기
```sql
declare
    v_count number(10) := 0;

begin
    WHILE   v_count < 9 loop
    v_count := v_count +1;
    dbms_output.put_line ('2 X ' || v_count || ' = ' || 2*v_count);
    END LOOP;
    
end;
/

-- while 루프문을 반복시킬 조건 loop이 TRUE일 때에만 loop문 수행.
-- BASIC LOOP : loop ~ exit when 조건 ~ end loop -> WHILE LOOP : while 조건 loop ~ end loop
```

#### 145. PL/SQL for Loop 이해하기
```sql
begin
    for i in 1 .. 9 loop
    dbms_output.put_line ('2 X ' || i || ' = ' || 2*i);
    END LOOP;
    
end;
/

-- BASIC LOOP : loop ~ exit when 조건 ~ end loop -> FOR LOOP : for i in 시작숫자 .. 종료숫자 loop
-- FOR LOOP문이 가장 단순하며 무한루프 빠지지 않을 코드 (v_count 외부 변수 대신 인덱스 카운터 i 활용, declare문 X)
```

#### 146. PL/SQL 이중 Loop 이해하기 
```sql
prompt '구구단 전체를 출력합니다.'
begin
    for i in 2 .. 9 loop
     for j in 1 .. 9 loop
    dbms_output.put_line (i || ' X ' || j || ' = ' || i*j);     
     END LOOP;
    END LOOP;
    
end;
/

-- prompt 다음 나오는 문장은 single quatation 써도 되고 안써도 됨
-- for loop문 작성 시, 하한값 .. 상한값 사이 점을 꼭 2개 찍어야 함
-- 바깥 loop문과 안쪽 loop문이 중첩된 이중 loop문
```

#### 147. PL/SQL Cursor문 이해하기 (Basic Loop)
```sql
declare v_ename     emp.ename%type;
        v_sal       emp.sal%type;
        v_deptno    emp.deptno%type;

    cursor emp_cursor is
            select  ename, sal, deptno
            from    emp
            where   deptno = 10;
begin
        open emp_cursor;
            loop 
                fetch emp_cursor into v_ename, v_sal, v_deptno;
                exit when emp_cursor%notfound;
                dbms_output.put_line ( v_ename || ' ' || v_sal || ' ' || v_deptno);
            end loop;
        close emp_cursor;

end;
/

-- ★ spl 워크시트 창에서 실행하는 것이 아니라, 명령 프롬프트 PL/SQL에서 메모장에 쿼리 작성 후 SQL 프롬프트에서 실행하는 것.
-- decalre문으로 데이터 타입 선언 > cursor문(cursor 메모리영역명 is ...) > begin문 open 메모리영역명 basic loop문 > end loop, close 메모리영역명 > end  
-- Cursor문 : PL/SQL 프로그램에서 처리할 데이터를 저장할 메모리 영역. (cursor 선언 > open > fetch > close) 
-- 데이터 베이스 프로그래밍(PL/SQL)은 원래 테이블에서 데이터를 한 건씩 가져오는데, cursor문은 여러 행의 결과를 한 번에 출력
-- 묵시적 커서,명시적 커서 / 4개의 속성(%ISOPEN, %FOUND, %NOTFOUND, %ROWCOUNT)
-- fetch문 : 커서문에서 원하는 결과를 읽어온 것 
```

#### 148. PL/SQL Cursor문 이해하기 (For Loop)
```sql
accept p_deptno prompt '부서 번호를 입력하세요~'
declare
    cursor emp_cursor is
        select  ename, sal, deptno
        from    emp
        where   deptno = &p_deptno;
        
begin
    for emp_record in emp_cursor loop
     dbms_output.put_line ( emp_record.ename || ' ' || emp_record.sal || ' ' || emp_record.deptno);
    end loop;
    
end;
/
```

#### 149. PL/SQL Cursor for loop문 이해하기
declare 절 없이 for loop 선언하여 서브 쿼리문 작성
```sql
accept p_deptno prompt '부서 번호를 입력하세요~'
        
begin
    for emp_record in (
        select  ename, sal, deptno
        from    emp
        where   deptno = &p_deptno) loop
        
     dbms_output.put_line ( emp_record.ename || ' ' || emp_record.sal || ' ' || emp_record.deptno);
    end loop;
    
end;
/
```

#### DAY 20. REVIEW
PL/SQL : Understanding SQL in a whole new direction 


#### 150. 프로시저 구현하기 (create procedure)
```sql
create or replace procedure pro_ename_sal (p_ename in emp.ename%type)
is
	v_sal emp.sal%type;
begin
	select sal into v_sal
		from emp
		where ename = p_ename;

	dbms_output.put_line (v_sal || '입니다');

end;
/

-- create or replace문으로 데이터베이스에 프로시저 생성 또는 PL/SQL 코드 변경 
-- 프로시저를 생성한 뒤, exec 함수로 PL/SQL코드를 데이터 베이스에서 프로시저 호출하여 실행
```

#### PL / SQL 개념 및 작성 요령에 관하여
-- PL / SQL 은 Procedure Language와 Structured Query Language의 줄임말로 데이터베이스 응용프로그램을 작성
-- PL / SQL은 SQL Developer 혹은 SQL명령창(SQLPLUS)에서 바로 작성하고 컴파일한 후 결과를 실행
-- PL / SQL로 개발한 프로그램은 SQL Developer에 프로시저로 저장 가능 

-- PL / SQL 블록 내에서 한 문장이 종료할 때마다 세미콜론(;)을 사용한다.
-- END 뒤에 ;을 사용하여 하나의 블록이 끝났다는 것을 명시한다.
-- PL / SQL 블록의 작성은 편집기를 통해 파일로 작성할 수도 있고, 프롬프트에서 바로 작성할 수도 있다.
-- SQL PLUS 환경에서는 DECLARE나 BEGIN이라는 키워드로 PL / SQL 블록이 시작하는 것을 알 수 있다.
-- 단일 행 주석은 --이고 여러 행 주석은 /* */이다.
-- PL / SQL 블록은 행에 /가 있으면 종결된다.
   
#### 151. 함수 구현하기 (create function)
```sql
create or replace function get_loc (p_deptno in dept.deptno%type)
return dept.loc%type
is v_loc dept.loc%type;

begin
    select  loc into v_loc
    from    dept
    where   deptno = p_deptno;
  return v_loc;
  
end;
/

select  ename, get_loc(deptno) as loc
from    emp
where   job = 'SALESMAN';

-- 프로시저 구현 : 1번째 블록 procedure 프로시저명 (입력용 매개변수 in 데이터타입) - 2번째 블록 begin - 3번째 end
-- 함수 구현 : 1번쨰 블록 function 함수명 (입력용 매개변수 in 데이터타입) return 데이터타입 - 2번째 블록 begin - 3번째 end
```

#### 152. 수학식 구현하기 (절대값)
PL/SQL 프로그래밍 코드로 절대값 출력하는 수학식 구현, if else문 사용
```sql
set serveroutput on
accept p_num prompt '숫자를 입력하세요~'

declare
    v_num   number(10) := &p_num;
    
begin
    if v_num >= 0 then
     dbms_output.put_line(v_num);
    else
     dbms_output.put_line(-1 * v_num);
    end if;

end;
/

-- begin절에서 is else문을 사용했기 때문에 end if로 종료해야 함
-- set serveroutput on 은 dbms_output.put_line을 수행하기 위한 SQL*PLUS 명령어이다.
```

#### 153. 수학식 구현하기 (직각 삼각형)
피타고라스와 직각삼각형 정리를 PL/SQL문으로 구현, if문과 power함수를 사용
```sql
set serveroutput on
accept p_num1   prompt '밑변을 입력하세요~'
accept p_num2   prompt '높이를 입력하세요~'
accept p_num3   prompt '빗변을 입력하세요~'

begin
    if power(&p_num1,2) + power(&p_num2,2) = power(&p_num3,3)
     then dbms_output.put_line('직각삼각형입니다.');
    else dbms_output.put_line('직각삼각형이 아닙니다.');
    end if;
    
end;
/

-- power (x, a) = x의 a승와 같은 지수함수
-- begin절에서 dbms_output.put_line을 사용하기 위해 set serveroutput on절이 필요함
-- declare절은 결과를 출력할 내부 변수가 필요할 경우 선언, 또는 특정 값을 할당할 경우.
```

#### 154. 수학식 구현하기 (지수함수)
loop문을 이용하여 밑수를 지수만큼 반복하여 곱한 값 출력
```sql
set serveroutput on
set verify off
accept p_num1 prompt '밑수를 입력하세요~'
accept p_num2 prompt '지수를 입력하세요~'

declare
    v_result    number(10) :=1 ;
    v_num2      number(10) := &p_num1;
    v_count     number(10) := 0;

begin
    loop
        v_count := v_count + 1;
        v_result := v_result*v_num2;
        exit when   v_count = &p_num2;
    end loop;
        dbms_output.put_line(v_result);
end;
/

-- 외부변수가 declare절, begin절 둘다 사용 가능함
```

#### 155. 수학시 구현하기 (로그 함수)
밑수를 입력받아 진수가 되도록 밑수를 반복하여 곱한 값 출력
```sql
set serveroutput on
set verify off
accept p_num1 prompt '밑수를 입력하세요~'
accept p_num2 prompt '진수를 입력하세요~'

declare
    v_num1 number(10)    := &p_num1;
    v_num2 number(10)    := &p_num2;
    v_count number(10)   := 0 ;
    v_result number(10)  := 1;

begin
    loop
            v_count  := v_count + 1;
            v_result := v_result*v_num1;
            exit when   v_result = v_num2;
    end loop;
            dbms_output.put_line(v_count);
end;
/

-- v_count 로그값 출력하는 anonymous PL/SQL 코드
-- set verify off : old값, new값 출력되지 않게 하는 SQL*PLUS 명령어
```

#### 156. 수학식 구현하기 (이중 루프문으로 구현하는 순열)
```sql
drop table emp145;

create table emp145
( num  number(10),
 fruit   varchar2(10) );

insert into emp145 values (1, '사과');
insert into emp145 values (2, '바나나');
insert into emp145 values (3, '오렌지');
commit;

select * from emp145;

set serveroutput on
set verify off
declare
 v_name1 emp145.fruit%type; 
 v_name2 emp145.fruit%type;
 
begin 
    for i in 1 .. 3 loop
     for j in 1 .. 3 loop
        select fruit into v_name1 from emp145 where num =i;
        select fruit into v_name2 from emp145 where num =j;
        if i != j then
         dbms_output.put_line(v_name1 || ', ' || v_name2);
        end if;
      end loop;
     end loop; 
end;
/

-- emp145 drop 후 create 후 insert 데이터값 진행
-- 순열이란 서로 다른 n개 중에서 r개를 택하여 일렬로 배열하는 것 (permutation)
-- 위 예제는 3개 중에서 2개 택하기, 서로 같은 값이 아닐 때, 가능한 경우의 수 예시를 나열하는 것
-- 외부변수없이 바로 내부변수 선언
```

#### 157. 수학식 구현하기 (조합)
```sql
set serveroutput on
set verify off
declare
 v_name1 emp145.fruit%type; 
 v_name2 emp145.fruit%type;
 
begin 
    for i in 1 .. 3 loop
     for j in 1 .. 3 loop
        select fruit into v_name1 from emp145 where num =i;
        select fruit into v_name2 from emp145 where num =j;
         dbms_output.put_line(v_name1 || ', ' || v_name2);
      end loop;
     end loop; 
end;
/

-- 조합이란 서로 다른 n개의 원소 중에서 r개를 선택하여 만든 모임 (combination)
```

#### 158. 기초 통계 구현하기 (평균값)
5개의 숫자를 입력받아 5개 숫자의 평균값을 출력
```sql
set serveroutput on
set verify off
accept p_arr prompt '숫자를 입력하세요~'

declare
    type arr_type is varray(5) of number(10); 
    v_num_arr   arr_type := arr_type(&p_arr);
    v_sum number(10) := 0;
    v_cnt number(10) := 0;
    
begin
    for i in 1.. v_num_arr.count loop
        v_cnt := v_cnt +1;
        v_sum := v_sum +v_num_arr(i);
    end loop;
     dbms_output.put_line(v_sum/v_cnt);

end;
/

-- loop문, 배열변수를 활용하여 평균값 통계식 구현
-- 배열변수 p_arr, v_num_arr, 할당값 arr_type(&p_arr), 5개의 숫자형 데이터 varray(5) of number(10)
-- 5개의 숫자 저장할 메모리 영역 변수 : 배열변수
```

#### 159. 기초 통계 구현하기 (중앙값)
홀수개의 숫자를 입력받으면 가운데값 출력, 짝수개의 숫자 입력받으면 가운데 2개의 평균값 출력
```sql
set serveroutput on
set verify off
accept p_arr prompt '숫자를 입력하세요~'

declare
    type arr_type is varray(10) of number(10);
    v_num_arr arr_type := arr_type(&p_arr);
    v_n number(10);
    v_medi number(10,2);
    
begin
    v_n := v_num_arr.count;
    if mod(v_n,2) = 1 then
        v_medi := v_num_arr((v_n+1)/2 );
    else
     v_medi := (  v_num_arr((v_n)/2 ) + v_num_arr((v_n)/2+1)  ) /2;
    end if;
    dbms_output.put_line(v_medi);
end;
/

-- n개의 숫자값을 담는 배열 변수형 타입을 선언한 후, n개보다 적은 숫자값을 입력해도 됨.
-- loop문 없이 if then, else 문을 활용해 PL/SQL 프로그래밍 코드 구현 
-- 내부 배열변수 : v_num_arr(카운팅된 숫자)
-- v_n : declare절에서 데이터 타입만 선언하고, begin절에서 입력숫자 counting 지정
-- v_medi : 중앙값
```

#### DAY 21. REVIEW
Procedual Language in SQL is tricky but efficiency 

#### 160. 기초 통계 구현하기 (최빈값)
입력받은 숫자들을 배열 변수에 담고 '숫자들의 값'을 카운트한 값들 중 최대값 : 최빈값
```sql
accept p_num1 prompt '데이터를 입력하세요~'
declare
    type array_t is varray(10) of number(10);
    v_array array_t := array_t(&p_num1);
    v_cnt number(10);
    v_tmp number(10);
    v_max number(10) := 0;
    v_tmp2 number(10);
    
begin
    for i in 1.. v_array.count loop
        v_cnt := 1;
        for j in i+1 .. v_array.count loop
            if v_array(i) = v_array(j) then
                v_tmp := v_array(i);
                v_cnt := v_cnt +1;
            end if;
        end loop;
        
        if v_max <= v_cnt then
            v_max := v_cnt;
            v_tmp2 := v_tmp;
        end if;
        end loop;
dbms_output.put_line ('최빈값은 '|| v_tmp2 ||'이고' || v_max || '개입니다.');
end;
/
            
-- type 배열변수타입명 is varray(변수갯수) of 데이터 타입           
-- 배열변수명 배열변수타입명 := 배열변수타입명(&외부 배열변수)
-- 배열변수명(순서) : 해당 순서로 입력한 변수 
```

#### 161. 기초 통계 구현하기 (분산과 표준편차 v_var)
먼저 평균값을 구한 후, 각각의 입력값과 평균값 차의 제곱을 모두 더한 뒤, 숫자들의 갯수를 나누면 분산값 (루트 분산값이 표준편차)
```sql
set serveroutput on
set verify off
accept p_arr prompt '숫자를 입력하세요~'

declare
    type arr_type is varray(10) of number(10);
    v_num_arr arr_type := arr_type(&p_arr);
    v_sum number(10,2) := 0;
    v_cnt number(10,2) := 0;
    v_avg number(10,2) := 0;
    v_var number(10,2) := 0;
    
    
begin
    for i in 1.. v_num_arr.count loop
        v_sum := v_sum + v_num_arr(i);
        v_cnt := v_cnt + 1;
    end loop;
    
    v_avg := v_sum/v_cnt;
    
    for i in 1..v_num_arr.count loop
        v_var := v_var + power(v_num_arr(i) - v_avg, 2);
    end loop;    
    
    v_var := v_var/ v_cnt;
    
dbms_output.put_line('분산값은: ' || v_var);
dbms_output.put_line('표준편자는: ' || round(sqrt(v_var)));

end;
/

-- 분산 : 데이터의 흩어진 정도를 나타내는 지표로 편차 제곱의 합
-- 2번의 for loop문 : 입력값의 합을 구하는 loop문, 입력값과 평균값의 차이를 계속 더하는 loop문 
-- 루트값을 구하는 sqrt함수
```

#### 162. 기초 통계 구현하기 (공분산 v_var)
```sql
accept p_arr1 prompt '키를 입력하세요~'
accept p_arr2 prompt '체중을 입력하세요~'

declare
    type arr_type is varray(10) of number(10,2);
    v_num_arr1 arr_type := arr_type(&p_arr1);
    v_sum1 number(10,2) := 0;
    v_avg1 number(10,2) := 0;
    
    v_num_arr2 arr_type := arr_type(&p_arr2);
    v_sum2 number(10,2) := 0;
    v_avg2 number(10,2) := 0;
    
    v_cnt number(10,2) := 0;
    v_var number(10,2) := 0;

begin
    v_cnt := v_num_arr1.count;
    
    for i in 1 .. v_num_arr1.count loop
        v_sum1 := v_sum1 + v_num_arr1(i);
    end loop;
    
    v_avg1 := v_sum1 /v_cnt;
    
    for i in 1 .. v_num_arr2.count loop
        v_sum2 := v_sum2 + v_num_arr2(i);
    end loop;
    
    v_avg2 := v_sum2 /v_cnt;
    
    for i in 1 .. v_num_arr2.count loop
        v_var := v_var + (v_num_arr1(i) - v_avg1) * (v_num_arr2(i) - v_avg2) / v_cnt;
    end loop;    
    
    dbms_output.put_line('공분산 값은 ' || v_var);
end;
/
-- 공분산 : 두 개의 변량 사이의 상관관계를 수치화, 공분산이 0보다 크면 양의 상관, 0보다 작으면 음의 상관관계
-- PL/SQL 절차적 언어로 거의 R, Python 와 다름없는 통계값 출력, 기본 지식인 비절차적 쿼리문 대비 좀 더 깊은 원리 이해가 필요할 듯 (w/ SQL 전문가 가이드)
```

#### 163. 기초 통계 구현하기 (상관계수 v_corr)
```sql
set serveroutput on
set verify off
accept p_arr1 prompt '키를 입력하세요~'
accept p_arr2 prompt '체중을 입력하세요~'

declare
    type arr_type is varray(10) of number(10,2);
    v_num_arr1 arr_type := arr_type(&p_arr1);
    v_sum1 number(10,2) := 0;
    v_avg1 number(10,2) := 0;
    
    v_num_arr2 arr_type := arr_type(&p_arr2);
    v_sum2 number(10,2) := 0;
    v_avg2 number(10,2) := 0;
    
    v_cnt number(10,2) := 0;
    cov_var number(10,2) := 0;

    v_num_arr1_var  number(10,2) := 0;
    v_num_arr2_var  number(10,2) :=0;
    v_corr          number(10,2) :=0;
    
begin
    v_cnt := v_num_arr1.count;
    
    for i in 1 .. v_num_arr1.count loop
        v_sum1 := v_sum1 + v_num_arr1(i);
    end loop;
    
    v_avg1 := v_sum1 /v_cnt;
    
    for i in 1 .. v_num_arr2.count loop
        v_sum2 := v_sum2 + v_num_arr2(i);
    end loop;
    
    v_avg2 := v_sum2/ v_cnt;
    
    for i in 1 .. v_num_arr2.count loop
        cov_var := cov_var + (v_num_arr1(i) - v_avg1) * (v_num_arr2(i) - v_avg2) / v_cnt;
        v_num_arr1_var := v_num_arr1_var + power(v_num_arr1(i) - v_avg1,2);
        v_num_arr2_var := v_num_arr2_var + power(v_num_arr2(i) - v_avg2,2);
    end loop;    
    
        v_corr := cov_var /sqrt(v_num_arr1_var *v_num_arr2_var);
         dbms_output.put_line('상관관계는 :' || v_corr );
end;
/

-- 상관관계 분석은 한 변수의 변화에 따른 다른 변수의 변화 정도와 방향 '예측', +1/-1 강한 상관관계, 0은 아주 약한 상관관계
-- 분산(표준편차) 개념 → 공분산 개념 → 상관계수 개념
```

#### 164. 기초 통계 구현하기 (확률)
dbms_random 패키지로 동전을 던졌을 때 확률 50% 값 출력

```sql
set serveroutput on
set verify off

declare 
    v_loop number(10) := 10000;
    v_coin number ;
    v_0 number(10) := 0;
    v_1 number(10) := 0;
    
begin
    for i in 1 .. v_loop loop
    
        select round(dbms_random.value(1,2)) into v_coin
         from dual;
        
        if v_coin = 1 then
            v_0 := v_0 +1;
            
        else v_1 := v_1 +1;
        
        end if;
    end loop;

    dbms_output.put_line('동전 앞면이 나올 확률 : ' || round(v_0/v_loop,2));
    dbms_output.put_line('동전 뒷면이 나올 확률 : ' || round(v_1/v_loop,2));    
    
end;
/

-- 교재가 나와있지 않더라도, set serveroutput on 작성해야 함. 그래야 dbms_output 결과가 워크시트창에 노출됨
```

#### 165. 기초 통계 구현하기 (확률2)
dbms_random 패키지를 2번 사용하여 동전 2개를 던져 둘다 앞면, 둘다 뒷면, 각각 한면씩 나오는 확률을 구현
```sql
set serveroutput on
set verify off

declare 
    v_loop number(10) := 10000;
    v_coin1 number(10) ;
    v_coin2 number(10) ;
    v_0 number(10) := 0;
    v_1 number(10) := 0;
    v_2 number(10) := 0;    

begin
    for i in 1 .. v_loop loop
    
        select round(dbms_random.value(1,2)), round(dbms_random.value(1,2)) into v_coin1, v_coin2
         from dual;
        
        if v_coin1 = 1 and v_coin2 = 1 then
            v_0 := v_0 +1;
            
        elsif v_coin1 = 2 and v_coin2 = 2 then
            v_1 := v_1 +1;
        else
            v_2 := v_2 +1;
        end if;
    end loop;

    dbms_output.put_line('동전 둘다 앞면이 나올 확률 : ' || round(v_0/v_loop,2));
    dbms_output.put_line('동전 둘다 뒷면이 나올 확률 : ' || round(v_1/v_loop,2));    
    dbms_output.put_line('동전 한 면이 나올 확률 : ' || round(v_2/v_loop,2));    
end;
/

-- 왜 동전 한 면이 나올 확률이 0.51이지...?
```

#### DAY 22. REVIEW
1st Studyng and Reading, 2nd should be deeper


#### 166. 기초 통계 구현하기 (이항 분포)
동전 던지기 확률을 사용자 정의 함수로 생성, 계층형 질의문으로 구현
```sql
create or replace function mybin (p_h in number)
return number
is
    v_h     number(10) := p_h;
    v_sim   number(10) := 100000;
    v_cnt   number(10) := 0;
    v_cnt2  number(10) := 0;
    v_res   number(10,2);
    
begin
    for n in 1 ..v_sim loop
    v_cnt := 0;
        for i in 1..10 loop
            if dbms_random.value <0.5 then
                v_cnt := v_cnt+1;
            end if;
        end loop;
        if v_cnt = v_h then
            v_cnt2 := v_cnt2 +1;
        end if;
    end loop;
    
    v_res := v_cnt2 /v_sim;
    return v_res;
    
end;
/

-- 이항 확률 분포 : 한 번 이상 반복 실시한 베르누이 시행 결과의 합을 변수의 값으로 하는 확률변수의 분포 
-- 동전 던지기 10번을 총 N번(100,000번) 반복하는 베르누이 시행
-- 동전던지기 경우의 수 발생 : dbms_random.value < 0.5
-- v_res 변수에 담긴 확률 값을 "리턴"
```

#### 167. 기초 통계 구현하기 (정규분포)
난수를 생성하여 dbms_random 패지키로 정규 확률 분호 구현
```sql
create or replace procedure probn
 (p_mu  in number,
  p_sig in number,
  p_bin in number)
is
 type arr_type is varray(9) of number(30);
 
 v_sim  number(10) := 100000;
 v_rv   number(20,7);
 v_mu   number(10) : p_mu;
 v_sig  number(10) : p_sig;
 v_nm   arr_type := arr_type('',0,0,0,0,0,0,0,'');
 v_cnt  arr_type := arr_type(0,0,0,0,0,0,0,0);
 v_rg   arr_type := arr_type(-power(2,31), -3, -2, -1, 0, 1,2,3, power(2,32));
 
begin
    for i in v_nm.first+1 .. v_nm.last-1 loop
        v_nm(i) := v_mu -3*p_bin + (i-2)p_bin;
    end loop;
    
    for i in 1 .. v_sim loop
        v_rv := dbms_random.normal * v_sig + v_mu;
        
    for i in 2 .. v_rg.count loop
        if v_rv >= v_mu + v_rg(i-1)*p_bin  and v_rv < v_mu + v_rg(i-1)*p_bin   then
            v_cnt(i-1) := v_cnt(i-1) +1;
        end if;    
    end loop;  
 end loop;   
    
    for i in 1 .. v_cnt.count loop
        dbms_output.put_line(rpad (v_nm(i)|| '~'||v_nm(i+1),10,' ') || lpad('★' , trunc((v_cnt(i)/v_sim)*100), '★'));
        
  end loop;   
  end;
  /
 
 /
-- 정규 분포 : 키, 몸무게, 제품 수명 등 표본을 크게 추출한 자료들이 좌우대칭 종 모양의 연속 확률 분포.
-- 변수값 := dbms_random.normal*표준편차 + 평균;
-- SQL 중고급의 길은 아직 멀고 험난하구나... 가보자고~
```

#### 168. PL/SQL로 알고리즘 문제 풀기 (삼각형 출력) 
숫자를 입력받아 삼각형을 출력하는 PL/SQL문을 학습 (Lpad 활용)
```sql
set serveroutput on
accept p_num prompt '숫자를 입력하세요~'

declare
    v_cnt number(10) := 0;
    
begin
    while v_cnt < &p_num loop
     v_cnt := v_cnt + 1;
     dbms_output.put_line(Lpad('★',v_cnt,'★'));
    end loop;
end;
/

-- 예제 113은 with절과 계층형 질의문은 사용한 SQL 쿼리문이며, 위 예제는 while loop문을 사용한 PL/SQL 프로시저 쿼리문이다.
-- v_cnt가 &p_num보다 작을 동안에만 while loop문이 수행됨 

#### 168. PL/SQL로 알고리즘 문제 풀기 (사각형 출력) 
가로, 세로 입력값을 받아 사각형을 출력하는 PL/SQL문 작성 

set serveroutput on
accept p_a prompt '가로를 입력하세요~'
accept p_b prompt '세로를 입력하세요~'

begin
    for i in 1 .. &p_b loop
    dbms_output.put_line(lpad('★',&p_b,'★'));
    end loop;
end;
/

-- 내부 변수 없이 외부 변수만으로 for loop문 작성이 가능함
-- 예제 168의 경우, 직각삼각형이라 while loop문, v_cnt에 점점 커지는 수 할당이 필요했음
```

#### 170. PL/SQL로 알고리즘 문제 풀기 (피타고라스의 정리)
if문과 power함수 활용하여 피타고라스의 정리를 PL/SQL로 구현
```sql
set serveroutput on
accept p_a prompt '밑변을 입력하세요~'
accept p_b prompt '높이를 입력하세요~'
accept p_c prompt '빗변을 입력하세요~'

declare
    v_a number(10) := &p_a;
    v_b number(10) := &p_b;
    v_c number(10) := &p_c;
    
begin
    if
    ( power(v_a,2) + power(v_b,2) )= power(v_c,2) then
    dbms_output.put_line('직각삼각형이 맞아요');
    else dbms_output.put_line('직각삼각형이 아니에요');
    end if;
end;
/

-- 교재에 쓰여진대로가 아닌, 응용력이 발휘되고 있음. 나 성장한건가??!!
```

#### DAY 23. REVIEW
Follow my gut, but still stick to the basic
