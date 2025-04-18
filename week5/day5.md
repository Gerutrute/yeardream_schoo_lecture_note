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

## 데이터 분석 함수
윈도우 함수 : 순위 함수 + 집계 함수로 구성되며, 행과 행 사이의 관계를 정의하는 함수 OVER 구문을 필수로 함(윈도우 함수 = OVER 구문)

↳ 집계 함수 : AVG, SUN, MAX, MIN 등...
그룹 함수 : 

**윈도우 함수**
- 테이블 안에서의 작은 틀로 생각하면 됨.
![image](https://github.com/user-attachments/assets/3ab2f2e7-d860-415f-846a-f5638861e070)
구문 예시
SELECT WINDOW_FUNCTION(ARGUMENTS) ex : SELECT ROWS()
OVER ([PARTITION BY 칼럼] [ORDER BY 절] [WINDOWING 절]) FROM 테이블 명;

### ✅ 윈도우 함수 구성 요소

| 구조         | 설명                                  |
|--------------|----------------------------------------|
| ARGUMENTS    | 윈도우 함수에 따라서 필요한 인수       |
| PARTITION BY | 전체 집합에 대해 소그룹으로 나누는 기준 |
| ORDER BY     | 소그룹에 대한 정렬 기준                |
| WINDOWING    | 행에 대한 범위 기준                    |
윈도우 함수 구성요소 -> POW

### ✅ WINDOWING 절 내 범위 지정 키워드

| 구조                | 설명                                   |
|---------------------|----------------------------------------|
| ROWS                | 물리적 단위로 행의 집합을 지정         |
| UNBOUNDED PRECEDING | 윈도우의 시작 위치가 첫 번째 행         |
| UNBOUNDED FOLLOWING | 윈도우의 마지막 위치가 마지막 행       |
| CURRENT ROW         | 윈도우의 시작 위치가 현재 행           |

![image](https://github.com/user-attachments/assets/f898f586-1c6d-48cd-856e-72ff1217c0a4)
윈도우 함수 -> 순위 함수

![image](https://github.com/user-attachments/assets/d104a9e6-e53c-454c-b1f6-0d6f5eed1ce7)
윈도우 함수 -> 집계 함수

# RANK() 함수 사용 예제

ChatGPT의 말:
markdown
복사
편집
# RANK() 함수 사용 예제

1. **PARTITION 없이**

   ```
   SELECT
     name,
     department,
     salary,
     RANK() OVER (ORDER BY salary DESC) AS rank
   FROM employees;
   ```
전체 테이블 기준으로 연봉 순위를 매깁니다.

2. **PARTITION 사용**

```
SELECT
  name,
  department,
  salary,
  RANK() OVER (
    PARTITION BY department
    ORDER BY salary DESC
  ) AS dept_rank
FROM employees;
```
부서(department)별로 따로 순위를 매깁니다.
