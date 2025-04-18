# 서브쿼리 심화

서브쿼리 심화 수업도 끝이 났어요! 🤗
심화 과정인 만큼 이번 장에는 어려운 내용이 많았어요.
이럴 땐 뭐다? 복습! 이번 장의 내용을 꼼꼼히 훑어보고 마지막 장으로 넘어가요~

------

## 1. 동작하는 방식에 따른 서브쿼리 분류

**Point I**
**연관 서브쿼리**: 메인쿼리의 컬럼이 서브쿼리에 포함되며, 메인쿼리의 컬럼은 서브쿼리에 특정 조건으로 사용

```
SELECT ID, DEPARTMENT_ID, NAME, SALARY
FROM EMPLOYEE A
WHERE SALARY > (
    SELECT AVG(SALARY)
    FROM EMPLOYEE B
    WHERE B.DEPARTMENT_ID = A.DEPARTMENT_ID);
```

- 본인이 속한 부서의 평균 급여보다 높은 급여를 받는 직원들 출력

**Point II**
**비연관 서브쿼리**: 메인쿼리 컬럼이 서브쿼리에 포함되지 않으며, 주로 메인쿼리에 특정한 값을 제공할 때 사용

```
SELECT AVG(SALARY)
FROM EMPLOYEE
WHERE DEPARTMENT_ID = (
    SELECT DEPARTMENT_ID
    FROM EMPLOYEE
    WHERE NAME = 'ELICE');
```

- ELICE가 속한 부서의 평균 급여 출력

------

## 2. 반환되는 데이터 형태에 따른 서브쿼리 분류

**Point I**
**단일 행 서브쿼리**: 서브쿼리의 결과가 한 개의 행을 반환하며, 단일 행 비교 연산자(`=`, `<`, `>`, `<=`, `>=`)와 같이 사용

```
SELECT ID, NAME, SALARY
FROM EMPLOYEE
WHERE DEPARTMENT_ID = (
    SELECT DEPARTMENT_ID
    FROM EMPLOYEE
    WHERE NAME = 'ELICE');
```

- ELICE가 속한 부서의 직원들을 출력
- 서브쿼리가 DEPARTMENT_ID = 1을 반환

**Point II**
**다중 행 서브쿼리**: 서브쿼리의 결과가 두 개 이상의 행을 반환하며, 다중 행 비교 연산자(`IN`, `ALL`, `ANY`, `EXISTS`)와 같이 사용

`IN`: 서브쿼리 결과에 존재하는 값들 중 하나와 일치하는 경우

```
SELECT NAME FROM EMPLOYEE
WHERE DEPARTMENT_ID IN (
    SELECT ID
    FROM DEPARTMENT
    WHERE NAME = '품질' OR NAME = '영업');
```

- 품질 또는 영업 팀에 속하는 직원들을 출력

`EXISTS`: 서브쿼리 결과 값이 존재하는지 확인

```
SELECT NAME FROM EMPLOYEE A
WHERE EXISTS (
    SELECT ID
    FROM EMPLOYEE B
    WHERE B.SALARY >= 10000
        AND A.DEPARTMENT_ID = B.DEPARTMENT_ID);
```

- 급여가 10000을 넘는 직원이 존재하는 부서에 소속된 모든 직원들을 출력

`ALL`: 서브쿼리 결과에 존재하는 모든 값들에 대해 조건을 만족하는 경우

```
SELECT NAME FROM EMPLOYEE
WHERE SALARY >= ALL (
    SELECT SALARY
    FROM EMPLOYEE
    WHERE DEPARTMENT_ID = 1);
```

- 개발팀(DEPARTMENT_ID = 1) 소속 모든 직원들 급여보다 급여가 큰 직원들을 출력

`ANY`: 서브쿼리 결과에 존재하는 값들 중 조건을 만족하는 것이 하나 이상 존재하는 경우

```
SELECT NAME FROM EMPLOYEE
WHERE SALARY >= ANY (
    SELECT SALARY
    FROM EMPLOYEE
    WHERE DEPARTMENT_ID = 1);
```

- 개발팀 소속 임의의 직원 급여보다 급여가 큰 직원들을 출력

**Point III**
**다중 컬럼 서브쿼리**: 서브쿼리의 결과가 여러 개의 컬럼을 반환하며, 메인쿼리의 조건과 동시에 비교

```
SELECT NAME, SALARY
FROM EMPLOYEE
WHERE (DEPARTMENT_ID) IN (
    SELECT DEPARTMENT_ID, MAX(SALARY)
    FROM EMPLOYEE
    GROUP BY DEPARTMENT_ID);
```

- 각 부서에서 가장 높은 급여를 받는 직원의 이름과 급여 출력

------

## 3. 스칼라 서브쿼리

**Point I**
**스칼라 서브쿼리**는 하나의 속성을 가지면서 하나의 행만 반환하는 쿼리입니다. 이는 `SELECT`, `WHERE`, `HAVING` 절 등에서 사용 가능합니다.

```
SELECT NAME, (
    SELECT COUNT(*)
    FROM EMPLOYEE E
    WHERE E.DEPARTMENT_ID = D.ID)
FROM DEPARTMENT D;
```

- 부서명과 부서의 구성원 수를 출력

**Point II**
`DUAL` 예시

```
SELECT
    (SELECT COUNT(*) FROM EMPLOYEE WHERE DEPARTMENT_ID = 1) /
    (SELECT COUNT(*) FROM EMPLOYEE)
    AS DEVELOPER_RATIO
FROM DUAL;
```

- FROM을 사용한 특정 테이블 참조 없이 쿼리 작성 가능
- 전체 임직원 중 팀장 직급이 차지하는 비율 출력

------

## 4. 뷰

**뷰**는 다른 테이블에서 파생된 테이블입니다. 물리적으로 데이터가 저장되는 것이 아니라, 논리적으로만 존재하며 뷰를 사용한 질의 시에는 DBMS에서 뷰 정의에 따라 질의를 재작성하여 수행합니다.

**Point I**
**VIEW의 장점**

- **독립성**: 테이블 구조가 변경되어도 뷰를 사용하고 있는 응용 프로그램은 변경하지 않아도 됩니다.
- **편리성**: 자주 사용되는 복잡한 쿼리를 미리 뷰로 정의해 놓으면, 추후 쿼리는 간단한 형태로 표현할 수 있습니다.
- **보안성**: 사용자의 권한에 따라 열람 가능한 데이터를 다르게 할 수도 있습니다.

**Point II**
**VIEW의 특징**

- 생성된 뷰는 또 다른 뷰를 생성하는데 사용될 수 있습니다.
- 뷰의 정의는 변경할 수 없으며, 삭제 후에는 재생성이 필요합니다.
- 뷰를 통한 갱신을 위해서는 원천 테이블의 기본키가 포함되어야 합니다.
- 원천이 되는 테이블이나 뷰가 삭제되면 이를 기반으로 하는 뷰도 함께 삭제 됩니다.

**Point III**
VIEW 정의 쿼리 예시

```
CREATE VIEW EMPLOYEE_FULL AS --같은 이름의 뷰가 존재하면 기존 뷰를 무시하고 대체
( --뷰를 생성할 쿼리 구문
    SELECT
        E.ID AS EMPLOYEE_ID,
        E.NAME AS EMPLOYEE_NAME,
        E.SALARY,
        E.DEPARTMENT_ID,
        D.NAME AS DEPARTMENT_NAME
    FROM EMPLOYEE E
    LEFT OUTER JOIN DEPARTMENT D
    ON E.DEPARTMENT_ID = D.ID
);
```
