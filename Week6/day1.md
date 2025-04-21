# 그룹 함수와 윈도우 함수

## 1. 윈도우 함수

**윈도우 함수 (Window Function)**: 순위, 집계 등 행과 행 사이의 관계를 정의하는 함수 (`OVER` 구문 필수)

```
SELECT WINDOW_FUNCTION (ARGUMENTS)
OVER ([PARTITION BY 컬럼] [ORDER BY 절] [WINDOWING 절])
FROM 테이블명;
```

- `ARGUMENTS`: 윈도우 함수에 따라서 필요한 인수
- `PARTITION BY`: 전체 집합에 대해 소그룹으로 나누는 기준
- `ORDER BY`: 소그룹에 대한 정렬 기준
- `WINDOWING`: 행에 대한 범위 기준

**Point I**
**순위 함수**

- `RANK`: 동일한 값에는 동일한 순위를 부여합니다.
- `DENSE_RANK`: 같은 값에는 같은 순위를 부여하나 한 건으로 취급합니다.
- `ROW_NUMBER`: 동일한 값이라도 고유한 순위를 부여합니다.

```
SELECT ID, NAME, SALARY,
    RANK() OVER (ORDER BY SALARY DESC) RANK,
    DENSE_RANK() OVER (ORDER BY SALARAY DESC) DENSE_RANK,
    ROW_NUMBER() OVER (ORDER BY SALARY DESC) ROW_NUMBER
FROM EMPLOYEE;
```

**Point II**
**일반 집계 함수**
일반 집계 함수(`SUM`, `AVG`, `MAX`, `MIN`, …)는 GROUP BY 구문 없이 사용할 수 있습니다.

```
SELECT ID, NAME, SALARY,
    AVG(SALARY) OVER (PARTITION BY DEPARTMENT_ID) DEPARTMENT_AVG
FROM EMPLOYEE;
```

**Point III**
**그룹 내 행 순서 함수**

1. `FIRST_VALUE`: 가장 먼저 나온 값을 구합니다.
2. `LAST_VALUE`: 가장 나중에 나온 값을 구합니다.

```
SELECT ID, DEPARTMENT_ID, NAME, SALARY,
    
    FIRST_VALUE(SALARY)
        OVER (PARTITION BY DEPARTMENT_ID ORDER BY SALARY
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
        AS DEPARTMENT_MIN_SALARY,
    
    LAST_VALUE(SALARY)
        OVER (PARTITION BY DEPARTMENT_ID ORDER BY SALARY
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
        AS DEPARTMENT_MAX_SALARY)
        
FROM EMPLOYEE
ORDER BY ID;
```

각 부서에서 급여를 가장 많이 받은 사람의 급여와 가장 적게 받는 사람의 급여를 함께 출력
![img](https://cdn-api.elice.io/api-attachment/attachment/d033abca120246e690f53ef31fd4e59e/image.png)

1. `LAG`: 이전 X 번째 행을 가져옵니다.
2. `LEAD`: 이후 X 번째 행을 가져옵니다.

```
SELECT ID, NAME, SALARY,
    LAG(NAME, 1) OVER (ORDER BY ID) PREV_EMPLOYEE_NAME,
    LEAD(NAME, 1) OVER (ORDER BY ID) AFTER_EMPLOYEE_NAME
FROM EMPLOYEE;
```

본인 사원 번호의 앞과 뒤에 해당하는 직원의 이름을 함께 출력
![img](https://cdn-api.elice.io/api-attachment/attachment/17e005f47ad6455384ecabe91e997d86/image.png)

**Point IV**
**그룹 내 비율 함수**

- `RATIO_TO_REPORT`: 파티션 내 전체 SUM에 대한 비율을 구합니다.

  ```
    SELECT ID, NAME, SALARY,
        SUM(SALARY) OVER() TOTAL_SALARY,
        RATIO_TO_REPORT(SALARY) OVER() RATIO_TO_REPORT
    FROM EMPLOYEE;
  ```

  직원 전체 급여의 합 중 각 행이 차지하는 비율을 출력

- `PERCENT_RANK`: 파티션 내 순위를 백분율로 구합니다.

- `CUME_DIST`: 파티션 내 현재 행보다 작거나 같은 건들의 수 누적 백분율로 구합니다.

  ```
    SELECT ID, NAME, SALARY,
        PERCENT_RANK() OVER(ORDER BY SALARY DESC) 
            AS PERCENT_RANK,
        ROUND(CUME_DIST() OVER(ORDER BY SALARY DESC), 4)
            AS CUME_DIST
    FROM EMPLOYEE;
  ```

- `NTILE`: 파티션 내 행들을 N등분한 결과를 구합니다.

  ```
    SELECT ID, NAME, SALARY,
        NTILE(3) ORDER(ORDER BY SLARAY DESC) NTILE
    FROM EMPLOYEE;
  ```

------

## 2. 그룹 함수

**그룹 함수 (Group function)**: 데이터를 통계하기 위해 원하는 데이터를 그룹화하는 함수 (`GROUP BY` 사용)

- `ROLL UP`: 그룹화하는 컬럼에 대한 부분적인 통계 제공합니다.

  ```
    SELECT D.NAME AS DEPARTMENT_NAME,
           J.NAME AS JOB_NAME, AVG(E.SALARY) AS AVG_SALARY,
    FROM EMPLOYEE E
    JOIN DEPARTMENT D
    ON E.DEPARTMENT_ID = D.ID
    JOIN JOB J
    ON E.JOB_ID = J.ID;
    GROUP BY ROLLUP(D.NAME, J.NAME);
  ```

  ![img](https://cdn-api.elice.io/api-attachment/attachment/c6a6d277060b448ea06b3086b6f9d669/image.png)

- `CUBE`: 그룹화 하는 컬럼에 대해 결합 가능한 모든 경우의 수에 대해 다차원 집계 생성합니다.

  ```
    SELECT D.NAME AS DEPARTMENT_NAME,
           J.NAME AS JOB_NAME, AVG(E.SALARY) AS AVG_SALARY,
    FROM EMPLOYEE E
    JOIN DEPARTMENT D ON E.DEPARTMENT_ID = D.ID
    JOIN JOB J ON E.JOB_ID = J.ID
    GROUP BY CUBE(D.NAME, J.NAME)
  ```

  ![img](https://cdn-api.elice.io/api-attachment/attachment/81ef4180d1c942b391f347f0a0fa89a7/image.png)

- `GROUPING SETS`: 명시된 컬럼에 대해 개별 통계 생성합니다.

  ```
    SELECT D.NAME AS DEPARTMENT_NAME,
           J.NAME AS JOB_NAME, AVG(E.SALARY) AS AVG_SALARY,
    FROM EMPLOYEE E
    JOIN DEPARTMENT D ON E.DEPARTMENT_ID = D.ID
    JOIN JOB J ON E.JOB_ID = J.ID
    GROUP BY GROUPING SETS(D.NAME, J.NAME);
  ```

  ![img](https://cdn-api.elice.io/api-attachment/attachment/6346eb62a70a436689e38a61a21be9af/image.png)

  - 각 컬럼에 대해 GROUP BY로 생성한 통계를 모두 UNION ALL한 결과와 동일
