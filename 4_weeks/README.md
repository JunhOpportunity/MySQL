# 4주차

Integrity constraints = rules

## SQL

Query Language, 프로그래밍 언어가 아니다.

쿼리란? DB와 상호작용 하기 위해 작성하는 것

대문자와 소문자를 구별하지 않는다. (select == SELECT)

주석 : `--` 또는 `#` 또는 `/* */`

예약어가 존재한다.

세미콜론 사용한다

## DDL (Data Definition Language)

### CREATE

CREATE DATABASE testDB;

SHOW DATABASES;

```sql
CREATE TABLE relation_name(
//            도메인
  attribute1 datatype, // 1열 (칼럼)
  floor int, // 2열
  username varchar(45), // 3열
); 
```

위 코드에서 문제가 존재하는데, 바로 PK가 존재하지 않다는 것이다.

그래서 MySQL 에서는 이것들을 제공해준다.

NOT NULL
PRIMARY KEY
FOREIGN KEY

### DROP

DROP DATABASE testDB; 

USE testDB; (중요)

테이블 자체가 완전히 삭제 (데이터까지)
⇒ 하지만 TRUNCATE 의 경우에는 데이터만 삭제하고 테이블은 남긴다.

### ✋ALTER

### TRUNCATE

## MySQL

Q. SQL에는 NOT NULL 이거 못쓰나? MySQL만 가능한가?

```sql
CREATE TABLE department(
	deptno int NOT NULL,
	deptnamevarchar(45) NOT NULL,
	floor int,
	CONSTRAINT PK_Department PRIMARY KEY (deptno),
	CONSTRAINT FK_Employee_Manager FOREIGN KEY (manager) REFERENCES employee(empno),
);
```

## DML (Data Manipulation Language)

### INSERT

?? 저 괄호 부분은 생략해도 된다는 건가?

INSERT INTO department (deptno, deptname, floor)

VALUES (2, '기획', 10),

### UPDATE

```sql
UPDATE relation_name
SET attribute1 = value1, attribute2 = value2, ...
WHERE condition; // WHERE 은 없어도 되는데 있는게 좋다
```

### DELETE

하나의 행을 삭제할 때 사용

```sql
DELETE FROM relation_name WHERE condition;
```

### SELECT (굉장히 중요. 시험 절반은 SELECT Query)

SELECT와 FROM 은 무조건 있어야 한다.

order of statements (순서가 매우 중요하다) 

SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY → LIMIT

GROUP BY와 HAVING 은 둘이 묶어서 사용한다.

SELECT * 은 전부 선택한다는 의미이다. (모든 attribute)

SELECT * vs SELECT deptno, deptname, floor 둘 중 일일이 적어주는 것이 조금 더 빠르다. 왜냐하면, * 은 나중에 컴파일 과정에서 *을 attribute로 다시 변환해주어야 하기 때문이다. 

SELECT DISTINCT title (removes duplicates 반복된 값을 삭제한다.)

AND 연산자가 오면 양쪽 다 true 인 경우에만 해당한다.
⇒ WHERE title = '과장' AND dno = 1;

<> 는 != 와 같다

✋BETWEEN AND 는 range operator 라고 부른다

OR 연산자가 오면 한쪽이라도 true 인 경우에 해당한다.
⇒ WHERE title = '대리' OR title = '사원';

WHERE NOT

(시험)LIKE 연산자는 text를 검색할 때 사용한다.

WHERE empname LIKE ‘이%’

이% : 이로 시작하는 문자열

%이 : 이로 끝나는 문자열

%or% :

_r% : 

IN 연산자는 OR 연산자와 비슷하다.
⇒ WHERE dno IN (1, 3); 1 또는 3
⇒ WHERE dno = 1 OR dno = 3

SELECT empname, salary, salary * 1.1 AS newsalary
⇒ 여기서 AS 를 사용해서 별칭을 설정한다. 기존 이름은 안 바뀌고 새로운 열이 만들어진다. (AS 도 중요)

?? Can only appear in SELECT and HAVING clauses 

튜플이 몇 개 있는지 확인하려면 COUNT(*) 사용
⇒ SELECT COUNT(*) AS allTuples FROM employee;

GROUP BY 는 (COUNT, SUM, AVG, MAX, MIN) 와 같이 쓴다

HAVING 은 GROUP BY와 세트이다. (GROUP BY의 조건을 추가하기 위해 HAVING을 사용한다)

ORDER BY 오름차순 내림차순

LIMIT 는 데이터가 너무 많을 때 제한을 둬서 몇개만보여주는지 결정하는 것