# SQL.Project

## < INTRO. SQLD 자격증 취득 >
**강의 : 제로베이스 SQL 완주반**

기간 : 2021/7/5(MON) ~ 8/20(FRI)

시험일정 : 2021/9/5(SUN)

시험결과 : Y

## < DEV. 이론과 실전, 간극을 좁히다. > 
**교재 : 초보자를 위한 SQL 200제, SQL 시작을 위한 최고의 입문서**

기간 : 2021/10/25(MON) ~ 11/21(SUN)

성장목표 : SQL 실무 시뮬레이션 & Kaggle 데이터 분석 도전

증명목표 : SQL 코딩 테스트 & SQLP 자격증 취득

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
a struggle in installing and setting up ORACEL & ORACLE SQL DEVELOPER

single vs double quotation

distinct vs unique

query plan : FROM the first, then WHERE, then SELECT, ORDER BY the last
