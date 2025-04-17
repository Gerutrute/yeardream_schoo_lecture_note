2. FROM절 JOIN 형태
Point I
INNER JOIN: 내부 JOIN이라고 하며, JOIN 조건에서 동일한 값이 있는 행만 반환

SELECT * FROM USER a (INNER) JOIN CLASS b
--INNER JOIN구로 테이블 정의
ON a.CLASS_ID = b.ID;
--ON구를 사용해 조인 조건 지정

--WHERE NAME = '모자장수';
INNER JOIN은 JOIN의 기본값으로 코드 작성시 ‘INNER’ 생략 가능
WHERE문을 이용하여 조건을 걸 수 있음 (코드 주석 부분 참조)
Point II
USING: 같은 이름을 가진 컬럼들 중 원하는 칼럼에 대해서만 선택적으로 등가 조인 가능

SELECT * FROM 테이블1 JOIN 테이블2
USING (기준칼럼);
--USING 조건절 사용시에는 컬럼이나 테이블에 별칭을 붙일 수 없음
SQL Server에서는 지원 X
Point III
NATURAL JOIN: 두 테이블 간의 동일한 이름을 갖는 모든 칼럼들에 대해 등가 조인을 수행

SELECT * FROM 테이블1 NATURAL JOIN 테이블2;
--추가로 ON/USING 조건절, WHERE 절에서 NATURAL JOIN 조건 정의 불가
--INNER JOIN과 달리 별칭 지정 불가
Point IV
CROSS JOIN: JOIN 조건이 없는 경우 생길 수 있는 모든 데이터의 조합을 조회

SELECT * FROM PERSON
(CROSS) JOIN PUBLIC_TRANSPORT;
CROSS절 생략 가능

Point V
OUTER JOIN: 두 개의 테이블 간에 교집합을 조회하고 한쪽 테이블에만 있는 데이터도 포함시켜서 조회

SELECT * FROM USER, CLASS
WHERE USER.CLASS_ID (+) = CLASS.CLASS_ID;


빈 곳은 NULL 값으로 출력
WHERE 조건절에서 한쪽에만 있는 데이터를 포함시킬 테이블 쪽으로 (+)를 위치
Point VI

LEFT (OUTER) JOIN: 왼쪽에 있는 테이블을 기준으로 조인

SELECT * FROM USER LEFT (OUTER) JOIN CLASS
ON USER.CLASS_ID = CLASS.CLASS_ID;


코드에서 OUTER 생략 가능
RIGHT (OUTER) JOIN: 오른쪽에 있는 테이블을 기준으로 조인

SELECT * FROM RIGHT (OUTER) JOIN CLASS
ON USER.CLASS_ID = CLASS. CLASS_ID;


코드에서 OUTER 생략 가능
FULL OUTER JOIN: 왼쪽 또는 오른쪽 테이블에 있는 모든 데이터를 조인


Note
MySQL은 FULL OUTER JOIN을 지원하지 않기 때문에 동일한 결과를 얻기 위해 UNION을 사용해야 합니다.

SELECT * FROM CLASS LEFT OUTER JOIN USER
ON USER.CLASS_ID = CLASS.CLASS_ID
UNION
SELECT * FROM CLASS RIGHT OUTER JOIN USER
ON USER.CLASS_ID = CLASS.CLASS_ID;


3. 셀프 조인
셀프 조인이란 동일 테이블 사이의 조인을 말합니다. 동일 테이블 간에 조인을 수행하면 테이블과 칼럼 이름이 모두 동일하기 때문에 식별을 위해 별칭이 필요합니다.

SELECT ALPHA.사원번호, ALPHA.관리자, BETA.관리자 차상위
FROM 직원 ALPHA, 직원 BETA --별칭 지정
WHERE ALPHA.관리자 = BETA.사원번호;
