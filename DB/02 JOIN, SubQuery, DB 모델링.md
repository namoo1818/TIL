### 2023.10.11

# JOIN
- 둘 이상의 테이블에서 데이터를 조회하기 위해서 사용
- 일반적으로 조인조건은 PK(Primary Key) 및 FK(Foreign Key)로 구성된다
- PK 및 FK 관계가 없더라도 논리적인 연관만으로도 JOIN 가능하다
- JOIN의 종류
  - INNER JOIN: 조인 조건에 해당하는 칼럼 값이 양쪽테이블에 모두 존재하는 경우에만 조회
    동등 조인(Equi-join)이라고도 한다. N개의 테이블 조인 시 N-1개의 조인 조건이 필요
  - OUTER JOIN: 조인 조건에 해당하는 칼럼 값이 한 쪽 테이블에만 존재 하더라도 조회
    기준 테이블에 따라 LEFT OUTER JOIN, RIGHT OUTER JOIN으로 구분
- 순서가 중요하다

# 카타시안 곱 Cartesian Product
- 두 개 이상의 테이블에서 데이터를 조회할 때
  - 조인 조건을 지정하지 않음
  - 조인 조건이 부적합함
- 첫 번째 테이블의 모든 행이 두 번째 테이블의 모든 행에 조인되어 처리됨

```mysql
# 14개
SELECT empno, ename, job
FROM emp;

# 4개
SELECT deptno, dname
FROM dept;

# 14 x 4 = 56개
SELECT empno, ename, job, emp.deptno, dept.deptno dname
FROM emp, dept;
```

```mysql
-- 조인을 이용하여 작성
SELECT ename, job, emp.deptno, dname
FROM emp, dept
WHERE emp.deptno = dept.deptno
AND empno = 7788;
```

![sql join](https://github.com/namoo1818/TIL/assets/50236187/e9596fed-3e19-49c3-8495-d0918a1d074e)

```mysql
SELECT * FROM emp;
```
![emp](https://github.com/namoo1818/TIL/assets/50236187/0d1113a7-f9df-4930-9808-b8b4c81becea)

```mysql
SELECT * FROM dept;
```
![dept](https://github.com/namoo1818/TIL/assets/50236187/f2c10f7e-0b5d-4da5-af95-3525a173a8a9)


# INNER JOIN
- 두 테이블에서 일치하는 값을 가진 레코드를 조회
```mysql
-- INNER JOIN
SELECT e.ename, e.job, e.deptno, d.dname
FROM emp e
INNER JOIN dept d
ON e.deptno = d.deptno
WHERE e.empno = 7788;
```
![inner join](https://github.com/namoo1818/TIL/assets/50236187/08ef816f-e0ea-4030-be64-4b84b172d4bf)

# OUTER JOIN
- 두 테이블에서 하나의 테이블에 조인조건 데이터가 존재하지 않더라도(조인조건을 만족하지 않음)
  데이터를 조회하기 위해서 사용
- 기준 테이블에 따라 LEFT OUTER JOIN(LEFT JOIN), RIGHT OUTER JOIN(RIGHT JOIN)으로 구분

# LEFT OUTER JOIN
- 왼쪽 테이블을 기준으로 JOIN하여 조건에 일치하지 않는 데이터까지 조회
- 사원의 이름, 부서번호, 부서 이름 조회
- emp를 기준 테이블로 LEFT OUTER JOIN하였을 때, JOIN 조건에 부합하지 않는 레코드가 조회됨을 알 수 있다
```mysql
SELECT e.ename, e.deptno, d.dname
FROM emp e LEFT OUTER JOIN dept d
ON e.deptno = d.deptno;
```
![left outer join](https://github.com/namoo1818/TIL/assets/50236187/3b9e6d49-33c7-4ddc-8c2c-1bac416808f4)

# RIGHT OUTER JOIN
- 오른쪽 테이블을 기준으로 JOIN하여 조건에 일치하지 않는 데이터까지 조회
- 회사내 모든 부서에 대해서 부서이름과, 부서에서 근무하는 사원의 사번, 이름 조회
- OPERTION 부서에 근무하는 사원은 없지만 조회되었음
```mysql
SELECT e.ename, e.deptno, d.dname
FROM emp e RIGHT OUTER JOIN dept d
ON e.deptno = d.deptno;
```
![right outer join](https://github.com/namoo1818/TIL/assets/50236187/e3f0c1ae-545e-47f0-8597-6c5c07a5c176)

# 셀프 조인 SELF JOIN
- 같은 테이블 2개 조인
- 모든 사원의 이름, 매니저 번호, 매니저 이름 조회
- 사원 정보는 e1, 매니저 정보는 e2에서 조회
- 조인 조건은 e1.mgr = e2.empno
```mysql
SELECT e1.empno, e1.ename, e1.mgr, e2.ename
FROM emp e1, emp e2
WHERE e1.mgr = e2.empno
ORDER BY e2.ename;
```
![self join](https://github.com/namoo1818/TIL/assets/50236187/df0c3416-a14a-4a92-ab46-754e1894d187)

# 비 동등 조인 Non-Equi JOIN
- 조인조건이 table의 PK, FK 등으로 정확히 일치하는 것이 아닐 때 사용
- 모든 사원의 사번, 이름, 급여, 급여등급을 조회
```mysql
SELECT e.empno, e.ename, e.sal AS "급여", sg.grade AS "급여등급"
FROM emp e, salgrade sg
WHERE e.sal BETWEEN sg.LOSAL AND sg.HISAL
ORDER BY sg.grade DESC, e.sal DESC;
```
![non equi join](https://github.com/namoo1818/TIL/assets/50236187/b575a472-e4d0-4a52-afef-a3829966df7a)

# 서브 쿼리 Subquery
- 하나의 SQL문 안에 포함되어 있는 SQL문을 의미
- 서브 쿼리를 포함하는 SQL을 외부 쿼리(outer query) 또는 메인 쿼리라고 부르며,
  서브 쿼리는 내부 쿼리(inner query)라고 부른다

# 서브 쿼리의 종류
- 중첩 서브 쿼리 - WHERE 절에 작성하는 서브 쿼리
- 인라인 뷰 - FROM 절에 작성하는 서브 쿼리
- 스칼라 서브 쿼리 - SELECT 문에 작성하는 서브 쿼리   
자세한 건 ppt 참고   

# 데이터베이스 모델링
- 실생활의 모든 것을 DB 세상에 옮기는 작업
![데이터베이스 모델링](https://github.com/namoo1818/TIL/assets/50236187/35bd1d2d-0434-4ce6-8d66-359e60fd832b)

그 다음은 ppt 참고
