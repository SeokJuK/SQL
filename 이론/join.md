# join
- 하나 이상의 테이블로부터 연관된 데이터를 검색해 오는 방법(테이블이 다른 경우)

# Cartesian Join(잘못된 경우)
- Join에 대한 조건이 생략되거나 잘못 기술되어 한 테이블에 있는 모든 행들이 다른 테이블에 있는 모든 행들과 Join되어 얻어지는 경우
- 테이블이 n개일 때 n-1개의 join 조건이 필요하다
- 쉽게 말하면 교집합인 부분을 where절에 넣어 출력을 한다 생각하면 쉽다 
```
select e.first_name, d.department_name from employees e, departments d where e.department_id = d.department_id;
```

# EQUIJOIN
- 컬럼에 있는 값이 정확하게 일치하는 경우에 =연산자를 사용하여 join
-- ex) 사원의 아이디와 부서의 아이디가 일치하는 것을 찾아 name과 departmentname을 조회
```
select 테이블명.컬럼명, 테이블명.컬럼명... from 테이블1. 테이블2 where 테이블1.컬럼1 = 테이블1.컬럼2;
```
- 컬럼에 있는 값드이 정확히 일치하는 경우에 = 연산자를 사용해 조인
- 일반적으로 pk-fk관계에 의하여 join이 성립
- where절 혹은 on절을 이용
- 액세스 효율을 향상시키고 좀 더 명확히 하기 위해 칼럼이름 앞에 테이블 이름을 밝힌다
- 같은 이름의 칼럼이 조인대상 테이블에 존재하면 반드시 컬럼이름 앞에 테이블 이름을 밝혀주어야 한다

# 조건(theta) Join
- 임의의 조건을 Join 조건으로 사용 가능
- Non-Equi-Join이라고도 함
```
select e.ename, e.sal, s.grade
from emp e, salgrade s
where e.sal between s.local and s.hisal
```

# Natural Join
- 두 테이블에 공통 칼럼이 있는 경우 별다른 JOIN 조건없이 공통 칼럼처럼 묵시적으로 조인이 되는 유형
- ANSI/ISO SQL1999를 따르는 ANSI JOIN문법
```
select*from departments natural join locations; //잘 사용하지 않는다
```

# Inner Join - Join ~ Using
- Natural Join의 문제점 : 조인하고자 하는 두 테이블에 같은 이름의 칼럼이 많을 때 위와 같을 시 특정한 칼럼으로만 조인하고 싶다면 Using절을 사용한다
```
select * from employees natural join departments;

select * from employees join departments using(department_id);
```

# Inner Join - Join - On
- 공통된 이름의 칼럼이 없는 경우 가장 보편적으로 사용할 수 있는 유형
- WHERE절에 일반 조건만 쓸 수 있게하고 조인 조건은 ON에 두어 보다 의미를 명확히 하고 알아보기 쉽다
- ON부분을 WHERE절에서 작성 가능하다
```
SELECT * FROM EMPLOYEES E JOIN DEPARTMENTS D ON(E.DEPARTMENT_ID = D.DEPARTMENT_ID);
```
