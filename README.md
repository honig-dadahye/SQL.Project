# SQL.Project

## STEP 00. SQLD 자격증 취득
**강의 : 제로베이스 SQL 완주반**

기간 : 2021/7/5(MON) ~ 8/20(FRI)

시험일정 : 2021/9/5(SUN)

시험결과 : Y

## STEP 01. 이론과 실전, 간극을 좁히다. 
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
column alias, double quatation mark for case, space, and special characters. (do not ues single quotation mark)
column alias in a formula (not function), avaliavle in ORDER BY clause 

