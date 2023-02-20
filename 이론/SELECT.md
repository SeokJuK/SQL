# SELECT
- Table에서 Data를 가져오기 위해 SELECT구문을 사용한다
> SELECT(DISTINCT)칼럼명(ALIAS)FROM 테이블명;
- SELECT:검색하고자 하는 데이터(칼럼)을 나열
- DISTINCT:중복행을 제거
- ALIAS:나타날 컬럼에 대한 다름 이름 부여
- FROM:선택한 컬럼이 있는 테이블을 명시

# 전체 Data Select
- SELECT를 가장 간단히 사용하게 되면 table의 모든 데이터를 가져온다
```
SELECT * FROM emplyees; //emplyees table의 모든 데이터를 가져와라
```

# 특정 칼럼을 보고싶은 경우
- comma(,)로 분리해서 관심있는 column을 적어주면 된다
```
select first_name, last_name from emplyees; // -> first_name과 last_name 출력
```

# 컬럼에 대한 ALIAS부여
- 컬럼에 대한 ALIAS(별칭)을 부여해서 나타내는 칼럼의 HEADING을 변경할 수 있다
- employees 테이블에서 직원의 이름, 입사일을 출력
```
select first_name as 이름, hire_date as 입사일 from emplyees; // -> first_name은 이름으로 컬럼이 별칭이 바뀌고 hire_date는 입사일로 바뀐다
```

# 컬럼의 합성(Concatenation)
- 문자열 결합함수 concat사용
- emplyees 테이블에서 직원의 전체 이름 입사일을 출력
```
select concat(first_name, ' ', last_name) as 이름, hire_date as 입사일 from emplyees; ->성, 이름이 합쳐져서 이름이라는 컬럼에 나온다
```
- 다른 방법으로는 Oracle DB기준으로
```
select first_name || ' ' || last_name AS 이름, hire_date as 입사일 from emplyees;
```

# 중복행의 제거(DISTINCT)
- 중복되는 행이 출력되는 경우, distinct 키워드로 중복행을 제거
```
select manager_id from emplyees;
select distinct manager_id from employees;
```

# 결과를 정렬하고 싶을 때
- SELECT(DISTINCT) 칼럼명(ALIAS) FROM 테이블명 ORDER BY 칼럼이나 표현식(ASC 또는 DESC);
- ORDER BY절을 사용한다
- 오름차순 정렬 ASC(생략 가능), 내림차순 정렬 DESC
```
select fist_name, last_name, hire_date from employees order by hire_date asc; // 오름차순
select fist_name, last_name, hire_date from employees order by hire_date desc; //내림차순
```

# WHERER과 함께 조회하기
> SELECT(DISTINCT) 칼럼명 (ALIAS)
> FROM 테이블명
> WHERE 조건식
> ORDER BY 칼럼이나 표현식(ASC 또는 DESC)
- 조건식: 컬럼이름이나 표현식의 상수, 연산자로 구성

# 특정 ROW에 대한 SELECT
- 테이블에서 특정 ROW만 가져올 수 있다
- LAST_NAME이 'KING'인 데이터를 조회한다
```
select * from employees where last_name ='king';
```
- 논리 연산자 and
```
select * from employees where last_name ='king' and first_name ='steven'; //first_name이 steven이면서 last_name이 king인사람
```
- 논리 연산자 or
```
select * from employees where last_name ='king' or first_name ='steven'; //first_name이 steven인사람 또는 last_name이 king인사람
```

# Null 다루기
- Null이 의미하는 것은 빈 값 또는 알 수 없는 값이다.
- NULL인지 아닌지 확인하기 위해 =,<,<>와 같은 산술연산자 비교를 사용할 수 없다
- 대신 IS NULL, IS NOT NULL연산자를 사용해야 한다
```
select*from employees where commision_pct is null; // null인것만 찾기
select*from employees where commision_pct is not null; //null이 아닌걸 찾기

# 패턴 매칭
- LIKE or NOT LIKE 비교 연산자를 사용해서 패턴매칭을 한다.
- 기본적으로 영문자인경우 대소문자 구분X
- 와일드카드를 
```
