# JOIN 심화

## 1. JOIN

`JOIN`: 두 개 이상의 테이블들을 **연결** 또는 **결합**하여 데이터를 출력하는 명령어

**Point I**
**EQUI JOIN**: 두 개의 테이블 간에 서로 정확하게 일치하는 경우를 활용하는 조인 (`=`)

- 대부분 기본키-외래키 관계를 기반으로 발생

**Point II**
**Non EQUI JOIN**: 두 개의 테이블 간에 서로 일치하지 않는 경우를 활용하는 조인 (`>`, `>=`, `<=`, `<`, `BETWEEN`)

------

## 2. FROM절 JOIN 형태

**Point I**
`INNER JOIN`: 내부 JOIN이라고 하며, JOIN 조건에서 동일한 값이 있는 행만 반환

```
SELECT * FROM USER a (INNER) JOIN CLASS b
--INNER JOIN구로 테이블 정의
ON a.CLASS_ID = b.ID;
--ON구를 사용해 조인 조건 지정

--WHERE NAME = '모자장수';
```

- INNER JOIN은 JOIN의 기본값으로 코드 작성시 ‘INNER’ 생략 가능
- `WHERE`문을 이용하여 조건을 걸 수 있음 (코드 주석 부분 참조)

**Point II**
`USING`: 같은 이름을 가진 컬럼들 중 원하는 칼럼에 대해서만 선택적으로 등가 조인 가능

```
SELECT * FROM 테이블1 JOIN 테이블2
USING (기준칼럼);
--USING 조건절 사용시에는 컬럼이나 테이블에 별칭을 붙일 수 없음
```

- SQL Server에서는 지원 X

**Point III**
`NATURAL JOIN`: 두 테이블 간의 **동일한 이름**을 갖는 모든 칼럼들에 대해 **등가 조인**을 수행

```
SELECT * FROM 테이블1 NATURAL JOIN 테이블2;
--추가로 ON/USING 조건절, WHERE 절에서 NATURAL JOIN 조건 정의 불가
--INNER JOIN과 달리 별칭 지정 불가
```

**Point IV**
`CROSS JOIN`: JOIN 조건이 없는 경우 생길 수 있는 **모든 데이터의 조합**을 조회

```
SELECT * FROM PERSON
(CROSS) JOIN PUBLIC_TRANSPORT;
```

- CROSS절 생략 가능
  ![img](https://cdn-api.elice.io/api-attachment/attachment/4080c46882844612a6989b4c36f030e3/image.png)

**Point V**
`OUTER JOIN`: 두 개의 테이블 간에 교집합을 조회하고 한쪽 테이블에만 있는 데이터도 포함시켜서 조회

```
SELECT * FROM USER, CLASS
WHERE USER.CLASS_ID (+) = CLASS.CLASS_ID;
```

![img](https://cdn-api.elice.io/api-attachment/attachment/dc64dd243c4e4daeb7b7b1a842eaa2dd/image.png)

- 빈 곳은 NULL 값으로 출력
- WHERE 조건절에서 한쪽에만 있는 데이터를 포함시킬 테이블 쪽으로 `(+)`를 위치

**Point VI**

1. `LEFT (OUTER) JOIN`: 왼쪽에 있는 테이블을 기준으로 조인

   ```
   SELECT * FROM USER LEFT (OUTER) JOIN CLASS
   ON USER.CLASS_ID = CLASS.CLASS_ID;
   ```

   ![img](https://cdn-api.elice.io/api-attachment/attachment/677d6993e55844b9afc8eb3dcbf194c3/image.png)

   - 코드에서 OUTER 생략 가능

2. `RIGHT (OUTER) JOIN`: 오른쪽에 있는 테이블을 기준으로 조인

   ```
   SELECT * FROM RIGHT (OUTER) JOIN CLASS
   ON USER.CLASS_ID = CLASS. CLASS_ID;
   ```

   ![img](https://cdn-api.elice.io/api-attachment/attachment/47b4a3bac11f4919a59a640fbf4eb4f9/image.png)

   - 코드에서 OUTER 생략 가능

3. `FULL OUTER JOIN`: 왼쪽 또는 오른쪽 테이블에 있는 모든 데이터를 조인
   ![img](https://cdn-api.elice.io/api-attachment/attachment/d0437809921c4efba2ec3f76dd9a92e3/image.png)

*Note*
MySQL은 `FULL OUTER JOIN`을 지원하지 않기 때문에 동일한 결과를 얻기 위해 `UNION`을 사용해야 합니다.

```
SELECT * FROM CLASS LEFT OUTER JOIN USER
ON USER.CLASS_ID = CLASS.CLASS_ID
UNION
SELECT * FROM CLASS RIGHT OUTER JOIN USER
ON USER.CLASS_ID = CLASS.CLASS_ID;
```

------

## 3. 셀프 조인

**셀프 조인**이란 동일 테이블 사이의 조인을 말합니다. 동일 테이블 간에 조인을 수행하면 테이블과 칼럼 이름이 모두 동일하기 때문에 식별을 위해 별칭이 필요합니다.

```
SELECT ALPHA.사원번호, ALPHA.관리자, BETA.관리자 차상위
FROM 직원 ALPHA, 직원 BETA --별칭 지정
WHERE ALPHA.관리자 = BETA.사원번호;
```

![img](https://cdn-api.elice.io/api-attachment/attachment/fe309974fcac4bb88ddda2cf918a272f/image.png)


## 서브쿼리 종류와 특징
- 연관 서브쿼리 : 메인 쿼리의 컬럼을 사용하면 연관 서브쿼리
- 비연관 서브쿼리 :테이블의 데이터만 사용하고, 메인 쿼리 컬럼 사용안함

![image](https://github.com/user-attachments/assets/c9f16243-14de-49c3-b63e-6011c6f7692a)

![image](https://github.com/user-attachments/assets/34dcfcf9-7ffa-4d97-b258-d5de7a550489)


# 반환되는 데이터 형태에 따른 분류

## 서브쿼리 분류
- 단일 행 서브쿼리 : 서브쿼리의 결과가 한 개의 행을 반환
![image](https://github.com/user-attachments/assets/008d047d-651c-4421-ad80-203c7600c40b)


- 다중 행 서브쿼리 : 서브쿼리의 결과가 2개 이상의 행을 반환

| 특징    | 설명                                                                 |
|---------|----------------------------------------------------------------------|
| IN      | 서브쿼리 결과에 존재하는 **값들 중 하나**와 일치해야 한다             |
| EXISTS | 서브쿼리 결과 값이 존재하는지 여부를 확인한다                         |
| ALL     | 서브쿼리 결과에 존재하는 **모든 값들**에 대해 조건을 만족해야 한다   |
| ANY     | 서브쿼리 결과에 존재하는 **값들 중 조건을 만족하는 것**이 하나 이상 존재해야 한다 |

![image](https://github.com/user-attachments/assets/9fb1e54b-a9c6-4eb3-8dd9-946e8ff31fdd)

![image](https://github.com/user-attachments/assets/10a7553c-5989-49df-b17f-b85dfeb0809c)

- 다중 컬럼 서브쿼리 : 서브쿼리의 결과가 여러 개의 컬럼을 반환하며, 메인 쿼리의 조건과 동시에 비교

![image](https://github.com/user-attachments/assets/e4a0bceb-62ec-48d8-a725-ebe5d92382a7)


## 단일 행 다중행 서브쿼리 선택 기준

| 질문처럼 생각해보기                                   | 서브쿼리 결과 예상               | 서브쿼리 유형 |
| ---------------------------------------------------- | ------------------------------ | ------------- |
| "이 값과 비교할 수 있나?"                            | 단일 값 → `=`, `>`, …          | 단일행        |
| "이 값 중 하나라도 맞으면 되지 않을까?"              | 여러 값 → `IN`, `ANY`          | 다중행        |
| "모든 조건을 다 만족해야 하나?"                      | 여러 값 → `ALL`                | 다중행        |
| "그런 값이 존재하기만 하면 되지 않을까?"             | 존재 여부 → `EXISTS`           | 다중행        |

## 스칼라 서브쿼리

![image](https://github.com/user-attachments/assets/b6312899-332b-44dd-99ce-f59ff00b6446)

![image](https://github.com/user-attachments/assets/dad484a5-bb40-418d-aa3d-34ed87d3341a)

## SQL 뷰
- 하나 이상의 쿼리구조 즉, 특정쿼리로 구성 된 가상의 쿼리로 실제 결과데이터는 없음. 동일한 DBMS라면 아무곳에서나 호출하여 사용 가능
- 뷰는 다른 테이블에서 파생된 데이터, 논리적으로만 존재하며 뷰를 사용한 질의
  ![image](https://github.com/user-attachments/assets/c707daca-72ed-44e8-827e-e0b0915f6daa)

  ![image](https://github.com/user-attachments/assets/fa873e7c-1712-4908-baab-6824bc390050)

  ![image](https://github.com/user-attachments/assets/ee19e048-42a5-4dfd-8f61-c226e855e302)

  ![image](https://github.com/user-attachments/assets/e35f8d8b-b92f-4bd7-9bff-0a8b7eeb5087)

  ![image](https://github.com/user-attachments/assets/855653fd-24e1-4239-8d29-df329cf255c4)
