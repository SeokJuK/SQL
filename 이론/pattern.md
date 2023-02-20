# 패턴매칭 예제
```
//first_name이 b로 시작하는 직원 정보 조회
select * from employees where first_name like 'n%';
//first_name이 t로 끝나는 직원 정보 조회
select * from employees where first_name like '%t";
//first_name이 w가 포함된 직원 조회
select * from employees where first_name like '%w%';
```

# 특정 글자 수만 찾기
```
select*from employees where first_name like '_____';
// 5글자이면서 첫 글자가 H인 사람
select*from employees where first_name like 'H____';
```

# IN
- In은 or와 똑같다고 생각하면 된다
- in을 사용 후(찾고싶은 값,찾고싶은 값);
```
//부서id가 90.100인 사원의 데이터 출력
select * from employees where department_id in (90,100);
// or를 사용했을 때
select * from employees where department_id = 90 or department_id = 100;
```

# 문자형 함수 - UCASE,UPPER
```
// last_name을 대문자로 모두 변경
select ucase(last_name) from employees;
select upper(last_name) from employees;
```

# 문자형 함수 - LCASE,LOWER
```
// last_name을 소문자로 모두 변경
select lcase(last_name) from employees;
select lower(last_name) from employees;
```

# 문자형 함수 - substring
```
select substring('happy_day',3,2); // 3번째 index부터 두글자 잘라라
```

# index 생성
- 많은 데이터양을 처리할 때 빠르게 처리가 가능하다
```
CREATE INDEX employees_hire_date_idx ON employees (hire_date);
EXPLAIN SELECT concat (first_name, ' ', last_name) AS 이름 , hire_date AS 입사딜 FROM employees where hire_date like '1989%';
// explain select 컬럼명 from 테이블 where ~;
```

# index 목록 보기, 인덱스 삭제하기
```
//목록 보기
show index from employees;
// 삭제하기
alter table employees drop index employees_hire_date_idx;
```

# 문자형 함수 - LPAD,RPAD
```
//hi라는 문자를 5자만큼 채우고 빈칸은 왼쪽으로 ?로 표시
select LPAD("hi",5,"?")
```

# 문자형 함수 - TRIM,LTRIM,RTRIM
- 공백을 제거해주는 역할
```
SELECT LTRIM(' hello '), RTRIM(' hello ');
// 문자를 사라지게 하는 방법 TRIM(BOTH '사라지게 하고싶은 문자' FROM '문자열');
SELECT TRIM(' hi '),TRIM(BOTH 'x' FROM 'xxxhixxx');
```

# 숫자형 함수 - ABS(x) - 절댓값
```
select ABS(2),ABS(-2);
```

# 숫자형 함수 - MOD(n,m) -> % 의미 : n을 m으로 나눈 나머지 값을 출력
```
select mod(342,10);
// 2가 출력
```

# 숫자형 함수 - CELING(X) -> x보다 작지 않은 가장 작은 정수를 반환
```
SELECT CEILING(1.23);
// 2 출력
```

# 숫자형 함수 - ROUND(X) -> X에 가장 근접한 정수를 반환
```
SELECT ROUND(1.23);
// 1출력
```

# 숫자형 함수 - ROUND(X,D) -> X값 중에서 소수점 D자리에 가장 근접한 수로 반환
```
SELECT ROUND(1.298,1)
// 1.3반환
```

# 숫자형 함수 - POW(x,y) POWER(x,y) -> x의 y제곱 승을 반환한다
```
SELECT POW(2,2)
//2의 2승 반환 -> 4
```

# 숫자형 함수 - SIGN(X) -> X가 음수이면 -1 X=0이면 0 X=양수이면 1을 출력한다
```
SELECT SIGN(-32), SIGN(0), SIGN(234);
// -1 0 1 출력
```

# 숫자형 함수 - GREATEST(X,Y,....) -> 가장 큰 값을 반환
```
SELECT GREATEST(2,0,3,6,9);
// 9를 반환
```

# 숫자형 함수 - LEAST(X,Y,....) -> 가장 작은 값을 반환

# 날짜형 함수 - CURDATE(), CURRENT_DATE -> 오늘 날짜를 YYYY-MM-DD나 YYYYMMDD 형식으로 반환
```
SELECT CURDATE(), CURRENT_DATE;
```

# 날짜형 함수 - CURTIME(), CURRENT_TIME -> 현재 시각을 HH:MM:SS나 HHMMSS형식으로 반환한다
```
SELECT CURTIME(), CURRENT_TIME;
```

# 날짜형 함수 - NOW() SYSDATE() CURRENT_TIMESTAMP -> 오늘 현 시각을 YYYY-MM-DD HH:MM:SS나 다른 형식으로 반환
```
SELECT NOW(), SYSDATE(), CURRENT_TIMESTAMP;
```

# 날짜형 함수 - DATE_FORMATE(date,format) -> 입력된 date를 format형식으로 반환한다.
```
select date_format((curdate(), '%w "m %y');
```

# 날짜형 함수 - PERIOD)DIFF(p1,p2): YYMM이나 YYYYMM으로 표기되는 p1과 p2의 차이 개월을 반환한다.
- 오늘까지 근무한 근무개월 수와 직원 이름을 출력하시오
```
SELECT concat(first_name, ' ', last_name) as name, PERIOD_DIFF(DATE_FORMAT(CURDATE(), '%Y'%m), DATE_FORMAT(hire_date, '%Y'%m)) FROM employees;
```

# 형 변환
CAST 함수는 type을 변경하는데 유용하다
```
CAST(expression as type) or CONVERT(expression, type);
```

# ROW 카운팅(counting)
- 테이블에 어떤 특정 조건의 데이터가 어떤 빈도로 나타나는가에 대한 database의 응답이다
- 예를 들어, 부서별로 직원이 몇명인지 궁금하고 싶을 때 사용
- 직원의 총 수는 테이블의 전체 row수 이다.
- 전체 직원 수 구하기
```
select count(*) from employees;
```
