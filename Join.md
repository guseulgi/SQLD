# Join
- 두 개 이상의 테이블 들을 연결 또는 결합하여 데이터를 출력하는 것
- 일반적으로 PK나 FK 값의 연관에 의해 Join이 성립되지만, 특별한 경우엔 PK, FK 관계가 없어도 논리적인 값들의 연관만으로 JOin이 성립 가능하다.
- 주의할 것은, From 절에서 여러 테이블이 나열되더라도 SQL에서 데이터를 처리할 땐 두 개의 집합 간에만 조인이 일어난다는 점이다.
- 테이블에 대한 alias를 적용하여 SQL 문장을 작성했을 때 Where절과 select 절에는 테이블명이 아닌 테이블에 대한 alias를 사용해야 한다. 다만, 하나의 SQL문장 내 유일하게 사용하는 컬럼명이라면 alias를 생략해도 된다.
- Join이 필요한 이유
  - 정규화란 불필요한 데이터의 정합성을 확보하고 이상현상을 피하기 위해 테이블을 분할하여 생성하는 것
  - 특정 요구조건을 만족하는 데이터들을 분할된 테이블로부터 조회하기 위해 테이블 간에 논리적인 연관관계가 필요하고 그런 관계성을 통해 다양한 데이터들을 출력할 수 있다.
  - 이런 논리적인 관계를 구체적으로 표현하는 것이 Join 조건인 것이다.



## Equi Join (등가 조인)
- 두 개의 테이블 간에 칼럼 값들이 서로 정확하게 일치하는 경우에 사용하는 방법
- 즉 Where 절에 기술하게 되는데 = 연산자를 사용해서 표현한다.
- PK <-> FK 의 관계를 기반으로 함
- 교집합
```
ex) Equi Join
SELECT T1.COL, T2.COL
FROM T1, T2
WHERE T1.COL1 = T2.COL2;

-> Ansi/ISO SQL 표준 방식으로 표현하면,
SELECT T1.COL, T2.COL
FROM T1
INNER JOIN T2 ON T1.COL1 = T2.COL2;
```

- Where 절에서 Join 조건 외 검색 조건에 대한 제한 조건을 덧붙여 사용 가능
- 즉, Equi Join 의 최소한의 연관 관계를 위해서 (테이블 수 - 1)개의 Join 조건을 Where절에 명시하고, 부수적인 제한 조건을 논리 연산자를 통해 추가로 입력하는 것이 가능
- 해시 조인은 Equi Join만 사용 가능
  1. 선행 테이블에서 주어진 조건을 만족하는 행을 찾음
  2. 선행 테이블의 조인 키를 기준으로 해시 함수 사용하여 해쉬 테이블 생성
  3. 해시 테이블을 메인 메모리에 생성
  4. 후행 테이블에서 조건을 만족하는 행 검색
  5. 후행 테이블의 조인키를 기준으로 해쉬 함수를 적용하여 실제 조인될 데이터를 찾음
  6. 조인에 성공하면 추출 버퍼에 넣음
  - 테이블 2개를 조인하여 결과를 가져와야 하고, 인덱스가 없다.
  - 주소를 사용하므로 CPU연산을 많이 하게 됨
  - 해시 함수를 사용하여 주소를 계산하며, 조인 컬럼의 동일한 해시값을 갖는 데이터를 조인하는 방식


## Non Equi Join (비등가 조인)
- 두 개의 테이블 간에 칼럼 값들이 서로 정확하게 일치하지 않는 경우 사용
- = 연산자를 제외한 Between, >, <, >=, <= 연산자 등을 사용하여 Join을 수행
```
SELECT COUNT(*) CNT
FROM EMP_TBL A, RULE_TBL B
WHERE A.ENAME LIKE B.RULE
```

## Natural Join
1. 반드시 두 테이블 간 동일한 이름, 타입을 가진 컬럼이 필요 -> 타입이 다르면 에러 발생
2. 조인에 이용되는 컬럼은 명시하지 않아도 자동으로 조인에 사용
3. 조인하는 테이블 간 동일 칼럼이 select절에 기술되어도 테이블명은 생략해야함
4. using 조건절은 사용 불가
```
Select *
From dept natural join location
where city = 'LA'
```

## Hash Join
1. 선행 테이블로 작은 테이블이 선정되어야 함
2. 해시 함수를 사용하여 주소를 계산하므로 CPU사용량이 증가함
   - 해시 함수는 유일한 값/암호화
3. Non Equal 조인 X / Equal 조인 O


## Inner Join (내부 조인)
- 두 테이블을 조인할 때 두 테이블에 모두 지정한 열의 데이터가 있어야 함
- 교집합
- Equi Join 과 기능이 동일하나 On을 사용하요 조인 조건을 나타낸다는 차이점이 존재
```
SELECT <열 목록>
FROM <첫 번째 테이블>
    INNER JOIN <두 번째 테이블>
    ON <조인 조건>
[WHERE 검색 조건]
```
- Natural Join 은 내부 조인에 속함
  - 두 테이블에서 동일한 칼럼명을 갖는 칼럼은 모두 조인
  - 두 테이블이 동시에 가지고 있는 칼럼의 값이 전부 같은 것만 리턴
  - 칼럼의 이름이 같지만 데이터 타입이 다르면 에러
  ```
  SELECT 조회할 컬럼
  FROM 테이블1
  NATURAL JOIN 테이블2
  [WHERE 조건문]
  ```

## Outer Join (외부 조인)
- 두 테이블을 조인할 때 1개의 테이블에만 데이터가 있어도 결과가 나옴
```
SELECT <열 목록>
FROM <첫 번째 테이블(LEFT 테이블)>
    <LEFT | RIGHT | FULL> OUTER JOIN <두 번째 테이블(RIGHT 테이블)>
     ON <조인 조건>
[WHERE 검색 조건]
```

### Left Outer Join
- 왼쪽 테이블의 모든 값이 출력되는 조인
- 오른쪽 테이블에서 없는 값의 경우 Null 로 채워짐

### Right Outer Join 
- 오른쪽 테이블의 모든 값이 출력되는 조인
- 왼쪽 테이블에서 없는 값의 경우 Null로 채워짐

### Full Outer Join
- 왼쪽 또는 오른쪽 테이블의 모든 값이 출력되는 조인, = Left Outer Join + Right Outer Join 
- 합집합


## Cross Join (상호 조인)
- 한 쪽 테이블의 모든 행과 다른 쪽 테이블의 모든 행을 조인
- 테이블 간 Join 조건이 없는 경우 생길 수 있는 모든 데이터 조합을 의미하며 결과는 양쪽 집합의 각 행인, M행 * N행 건의 데이터 조합이 발생한다. 이를 카테시안 곱(Cartesian product) 이라고 한다.
```
SELECT *
FROM <첫 번째 테이블>
    CROSS JOIN <두 번째 테이블>
```


## Self Join (자체 조인)
- 자신이 자신과 조인, 1개의 테이블을 사용
```
SELECT <열 목록>
FROM <테이블> 별칭A
    INNER JOIN <테이블> 별칭B
[WHERE 검색 조건]
```



# 집합 관계에 따른 분류
## 교집합
1. Equi Join
2. Inner Join
3. Intersect 연산 : 2 개의 테이블에서 공통된 값을 조회
```
SELECT DEPTNO FROM STUDENT
INTERSECT
SELECT DEPTNO FROM DEPT;
```


## 합집합
1. Full Outer Join
2. Union 연산 : 2개의 테이블을 하나로 합치는 연산, 단 2개 테이블의 칼럼 개수, 데이터 형식이 일치해야 함
  - 테이블을 1개로 합치면서 중복 데이터를 제거하고 정렬함
  - 단순하게 중복 데이터를 제거하지 않고 정렬되지 않는 합집합 연산으로 Union All 도 있음
```
Select *
From A Full Outer Join B
On (A.key = B.key);
```


## 차집합
1. Minus 연산 : 2개의 테이블에서 차집합을 조회
  - 먼저 쓴 Select 문에는 있는 값이면서 뒤에 언급된 select 문에는 없는 집합을 조회
```
SELECT DEPTNO FROM DEPT
MINUS
SELECT DEPTNO FROM STUDENT;
```
```
# 차집합을 조인으로 나타낼 경우,
Select *
From A Left Join B
On (A.key = B.key)
Where B.key Is Null;
```
2. Except 연산(MS-SQL)


# Join 절의 On절과 Where절의 차이
- 본론부터 말하자면 Join 할 대상(범위)가 On/Where에 따라 달라진다.
  - On : Join 하기 전, 필터링을 해준다. = On 조건으로 필터링된 레코드들 간 Join이 발생한다.
  - Where : Join 을 한 다음 필터링 된다.
```
Select * From t Left Join t2
On (t.a = t2.a)
where t2.c = 7;
# t2.c 인 데이터만 리턴 된다

Select From t Left Join t2
On (t.a = t2.a And t2.c = 7);
# t2.c인 데이터와 아닌 데이터도 리턴 된다
```

# Join 절의 using 조건절
- 두 개의 테이블이 Inner Join 으로 조인될 때 조인 하고자 하는 두 테이블의 칼럼명이 같을 경우, 조인 조건인 On절을 길게 적지 않고 간단하게 적을 수 있도록 한 조건절
```
Select * From A Inner Join B
On (A.ID = B.ID);
      =
Select * From A Inner Join B
Using(ID)
```
