# SQL.Project

## < INTRO. SQLD 자격증 취득 >
- 강의 : 제로베이스 SQL 완주반
- 기간 : 2021/7/5(MON) ~ 8/20(FRI)
- 시험일정 : 2021/9/5(SUN)
- 시험결과 : Y

## < DEV. 이론과 실전, 간극을 좁히다. > 
- 교재 : 초보자를 위한 SQL 200제, SQL 시작을 위한 최고의 입문서
- 기간 : 2021/10/25(MON) ~ 11/21(SUN)
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
