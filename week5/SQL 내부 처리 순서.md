
markdown
복사
# SQL 내부 처리 순서

SQL 쿼리는 우리가 위에서 아래로 작성하지만, 실제 실행 순서는 다릅니다.  
SQL 엔진은 정해진 순서대로 내부적으로 처리합니다.

---

## 1. SQL 실행 순서 (기본형 기준)

```sql
SELECT 컬럼
FROM 테이블
JOIN ...
WHERE 조건
GROUP BY 컬럼
HAVING 조건
ORDER BY 정렬
LIMIT 개수
2. SQL 실행 순서 (실제 내부 처리 순서)

순서	절 (Clause)	설명
①	FROM	기준 테이블 설정
②	JOIN	조인 테이블 붙이기
③	ON	조인 조건 필터링
④	WHERE	행(Row) 단위 조건 필터링
⑤	GROUP BY	그룹핑 (묶기)
⑥	HAVING	그룹에 대한 조건 필터링
⑦	SELECT	최종 컬럼 선택 (계산 포함)
⑧	ORDER BY	정렬 수행
⑨	LIMIT	출력 개수 제한
3. 서브쿼리 (서브쿼리는 먼저!)
예시 쿼리:

sql
복사
SELECT name
FROM user
WHERE user_id IN (
    SELECT user_id
    FROM rental
    WHERE item = '노트북'
);
포인트:

서브쿼리 (SELECT user_id ...)가 먼저 실행됩니다.

메인 쿼리는 서브쿼리 결과를 받아서 실행됩니다.

즉, SQL은 안쪽에서 바깥으로, FROM → SELECT 순으로 실행됩니다.

4. HAVING과 WHERE의 차이 및 순서
예시 쿼리:

sql
복사
SELECT department, COUNT(*)
FROM employee
WHERE age >= 30
GROUP BY department
HAVING COUNT(*) >= 5;
WHERE: 그룹핑 전에 조건 걸기 (개별 행 필터)

GROUP BY: 부서별로 묶기

HAVING: 그룹핑 후에 조건 걸기 (묶인 그룹 필터)

예를 들어, 30세 이상 직원만 모은 다음, 부서별로 묶고, 인원이 5명 이상인 부서만 추출

5. 정리: 외우기 쉬운 순서 암기법
plaintext
복사
FROM → JOIN → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT
FROM/WHERE: 데이터를 "어디서, 어떤 조건으로" 가져올지

GROUP BY/HAVING: 데이터를 "어떻게 묶고, 그 그룹을 어떤 기준으로 남길지"

SELECT: 최종으로 어떤 컬럼을 보여줄지

ORDER BY/LIMIT: 정렬하고 개수 제한

6. 실제 실행 흐름 예시
FROM user

JOIN rental ON ...

WHERE 조건

GROUP BY 컬럼

HAVING 조건

SELECT 컬럼명

ORDER BY 정렬기준

LIMIT N
