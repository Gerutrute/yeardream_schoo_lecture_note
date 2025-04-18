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

| 구문                                                   | 의미                           |
|--------------------------------------------------------|--------------------------------|
| ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW       | 맨 앞에서부터 현재 행까지 포함 |
| ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING       | 현재 행부터 끝까지 포함        |
| ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING               | 현재 행 앞뒤 하나씩 포함       |


### ✅ 그룹 내 행 순서 함수

| 함수          | 설명                         |
| ------------- | ---------------------------- |
| FIRST_VALUE   | 가장 먼저 나온 값을 구한다   |
| LAST_VALUE    | 가장 나중에 나온 값을 구한다 |
| LAG           | 이전 X번째 행을 가져온다     |
| LEAD          | 이후 X번째 행을 가져온다     |

![image](https://github.com/user-attachments/assets/f898f586-1c6d-48cd-856e-72ff1217c0a4)
윈도우 함수 -> 순위 함수

![image](https://github.com/user-attachments/assets/d104a9e6-e53c-454c-b1f6-0d6f5eed1ce7)
윈도우 함수 -> 집계 함수

구현 예시
```
SELECT
    ID, DEPARTMENT_ID, NAME, SALARY,
    FIRST_VALUE(SALARY)
        OVER(PARTITION BY DEPARTMENT_ID ORDER BY SALARY
             ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
        AS DEPARTMENT_MIN_SALARY,
    LAST_VALUE(SALARY)
        OVER(PARTITION BY DEPARTMENT_ID ORDER BY SALARY
             ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
        AS DEPARTMENT_MAX_SALARY
FROM EMPLOYEE
ORDER BY ID;
```

## RANK() 함수 사용 예제

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

윈도우 함수_ 그룹 내 함수 사용 예제
## 🔺 기본 테이블 예시 (`ORDER BY salary ASC`)

| NAME | SALARY |
|------|--------|
| Kim  | 3000   |
| Lee  | 5000   |
| Park | 7000   |
| Jung | 9000   |

---


## 🟦 1. `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`

> "맨 앞부터 현재 행까지 포함"
<details>
<summary>접기/펼치기</summary>
<div markdown="1">
### 각 행 기준 포함 범위:

| 현재 행 | 포함되는 행 (범위)     | 합계 (SUM 예시) |
|--------|------------------------|----------------|
| Kim    | Kim                   | 3000           |
| Lee    | Kim, Lee              | 8000           |
| Park   | Kim, Lee, Park        | 15000          |
| Jung   | Kim, Lee, Park, Jung  | 24000          |

✅ 옆에서부터 누적되는 누적합
</div>
</details>

## 🟦 2. `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING`

> "현재 행부터 마지막까지 포함"
<details>
<summary>접기/펼치기</summary>
<div markdown="1">
### 각 행 기준 포함 범위:

| 현재 행 | 포함되는 행 (범위)     | 합계 (SUM 예시) |
|--------|------------------------|----------------|
| Kim    | Kim, Lee, Park, Jung  | 24000          |
| Lee    | Lee, Park, Jung        | 21000          |
| Park   | Park, Jung             | 16000          |
| Jung   | Jung                   | 9000           |

✅ 뒤에서부터 줄어드는 누적합
</div>
</details>
## 🟦 3. `ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING`

> "현재 행의 앞 한 줄 + 현재 + 뒤 한 줄 포함"
<details>
<summary>접기/펼치기</summary>
<div markdown="1">
### 👇 각 행 기준 포함 범위:

| 현재 행 | 포함되는 행 (범위)     | 합계 (SUM 예시) |
|--------|------------------------|----------------|
| Kim    | Kim, Lee               | 8000           |
| Lee    | Kim, Lee, Park         | 15000          |
| Park   | Lee, Park, Jung        | 21000          |
| Jung   | Park, Jung             | 16000          |

✅ 이웃한 행까지 포함한 슬라이딩 윈도우 계산

</div>
</details>

**순위 함수**

RANK() OVER([PARTITION BY 컬럼][ORDER BY 컬럼 ][WINDOWING 절])
| 함수         | 설명                                                                 |
|--------------|----------------------------------------------------------------------|
| `RANK`       | 동일한 값에는 동일한 순위를 부여                                     |
| `DENSE_RANK` | `RANK`와 같이 같은 값에는 같은 순위를 부여하나 한 건으로 취급         |
| `ROW_NUMBER` | 동일한 값이라도 고유한 순위를 부여                                   |

![image](https://github.com/user-attachments/assets/d632a4cd-4307-4ed8-b81f-4718894ab543)

**일반 집계 함수**
- 일반 집계함수(SUM, AVG, MAX, MIN, ...)를 GROUP BY 없이 사용 가능(OVER(Partition) 기능 때문에)

![image](https://github.com/user-attachments/assets/3ad12664-2109-498e-93d5-a9d9ea7cd5a0)

## 🔍 `FIRST_VALUE`, `LAST_VALUE`

**각 부서에서 급여를 가장 많이 받은 사람의 급여와, 가장 적게 받은 사람의 급여를 함께 출력**

```sql
SELECT
    ID, DEPARTMENT_ID, NAME, SALARY,

    FIRST_VALUE(SALARY) OVER(PARTITION BY DEPARTMENT_ID ORDER BY SALARY
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS DEPARTMENT_MIN_SALARY,

    LAST_VALUE(SALARY) OVER(PARTITION BY DEPARTMENT_ID ORDER BY SALARY
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS DEPARTMENT_MAX_SALARY

FROM EMPLOYEE
ORDER BY ID;
```

![image](https://github.com/user-attachments/assets/e3e08402-35ff-4369-bd6e-88de84f5ff82)


** 그룹 내 비율 함수**

| 함수             | 설명                                                        |
|------------------|-------------------------------------------------------------|
| `RATIO_TO_REPORT` | 파티션 내 전체 SUM에 대한 비율을 구한다                    |
| `PERCENT_RANK`    | 파티션 내 순위를 백분율로 구한다                            |
| `CUME_DIST`       | 파티션 내 현재 행보다 작거나 같은 건들의 수 누적 백분율로 구한다 |
| `NTILE`           | 파티션 내 행들을 N등분한 결과를 구한다                     |

*`RATIO_TO_REPORT`*

![image](https://github.com/user-attachments/assets/b40d2b9a-f05b-4f8b-b889-1259c980a1af)

*`PERCENT_RANK`*
*`CUME_DIST`*

![image](https://github.com/user-attachments/assets/72e9f77f-afe1-4299-b974-7b84da559175)

*`NTILE`*

![image](https://github.com/user-attachments/assets/5b863f0f-a96f-46b5-bda4-bbab76359734)

##ROLL UP
- 그룹의 평균치를 나타내는 것
![image](https://github.com/user-attachments/assets/d4521d3c-e098-4c76-bab7-1a493d393976)

| 항목                   | WITH ROLLUP (MySQL 확장 문법) | ROLLUP(...) (SQL 표준 문법)        |
|------------------------|-------------------------------|------------------------------------|
| 문법 스타일            | MySQL 확장 문법               | SQL 표준 문법                     |
| 괄호 사용              | 없음 (쉼표로 집합 나열)       | 있음 (괄호로 집합 감쌈)           |
| MariaDB 지원 여부     | ○ (전 버전에서 가능)          | ○ (10.2 이상)                     |
| GROUPING SETS와 호환  | ✕                              | ○                                 |
| 명확성 및 유연성       | 중간                           | 높음                              |
| GROUPING 함수 지원 여부 | ✕                              | ✕ (MariaDB 자체가 지원 안 함)     |
| 결과 차이              | 있음 (동일한 ROLLUP 결과 생성) | 없음                              |

![image](https://github.com/user-attachments/assets/32ef9a1c-e8cb-49bd-8da3-e06414993ba3)

![image](https://github.com/user-attachments/assets/cc74bf5e-e51a-4ed2-9e8b-931e27e4fee9)

![image](https://github.com/user-attachments/assets/e104ea02-4a60-4400-bdb9-f93cb29746d0)

![image](https://github.com/user-attachments/assets/96cda673-5f1f-436d-86a1-607887d19199)


## CUBE
- ROLL UP 함수에서 제공하는 결과를 포함하여, CUBE 함수에서 그룹화 하는 컬럽에 대해 결합 가능한 모든 경우의 수에
다차원 집계를 생성함.

![image](https://github.com/user-attachments/assets/e825c2c4-d454-4929-a088-78f4e40a845a)

![image](https://github.com/user-attachments/assets/03edd86b-1d54-438e-98f8-4bbc32292ed7)

## ROLL UP과 CUBE 구분 설명예제

![image](https://github.com/user-attachments/assets/44551fc7-451f-4982-82ea-8c667690e974)

| 항목            | ROLLUP                              | CUBE                                  |
|-----------------|--------------------------------------|----------------------------------------|
| 조합 수         | 누적 조합 (N + 1개)                  | 모든 조합 (2ⁿ개)                       |
| 예: 2개 열      | (A, B), (A), ()                      | (A, B), (A), (B), ()                   |
| 사용 목적       | 계층 보고서 (예: 년 → 월 → 일)       | OLAP, 피벗 테이블 등 다차원 분석      |
| 순서 중요       | O                                    | X                                      |
| MariaDB 지원    | O (WITH ROLLUP 또는 ROLLUP())         | ✕ (직접 지원 X → GROUPING SETS로 대체 가능) |

## Online Analytical Processing의 대표 기능

| 기능명       | 설명                                                    | SQL 대응 기능                    |
|--------------|---------------------------------------------------------|----------------------------------|
| Slice        | 하나의 축(열)에 대해 값 하나만 선택해서 잘라보기         | `WHERE` 또는 필터                |
| Dice         | 두 개 이상의 축의 값 범위를 지정해 잘라보기              | `WHERE AND` 조건                |
| Roll-up      | 상위 수준으로 요약하기 (예: 일 → 월 → 년)              | `GROUP BY + ROLLUP`             |
| Drill-down   | 하위 수준으로 세부 정보 보기 (예: 월 → 일)             | `GROUP BY` 더 세부로            |
| Pivot        | 행과 열을 바꾸며 보는 형태 (예: Excel 피벗테이블)       | `CUBE`, `GROUPING SETS` 등      |

| 년도 | 지역 | 제품  | 매출 |
|------|------|-------|------|
| 2024 | 서울 | A상품 | 1000 |
| 2024 | 부산 | B상품 |  800 |

---

이 데이터를 OLAP 분석으로 이렇게 볼 수 있어요:

- ✅ **연도별 매출 합계** (`ROLLUP`)
- ✅ **연도 + 지역별 매출** (`GROUP BY`)
- ✅ **지역 + 제품별 매출 요약** (`GROUPING SETS`)
- ✅ **전체 평균 매출** (`CUBE 결과 중 (NULL, NULL)`)

## GROUPING SETS
- 명시된 컬럼에 대해 개별 통계를 생성
- 각 컬럼에 대해 GROUP BY로 생성한 통계를 모두 UNION ALL한 결과와 동일함
![image](https://github.com/user-attachments/assets/55eb9258-12e1-4bf8-9b6c-b1508e41dfdb)

![image](https://github.com/user-attachments/assets/91080a41-5b9f-41d4-85d6-4db07650fcee)

