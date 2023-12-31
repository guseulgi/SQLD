# SQL 기본 및 활용

## 데이터 언어
데이터베이스를 정의하고 접근하기 위한 데이터베이스 관리 시스템과의 통신수단

### 데이터 언어와 SQL 명령어
1. 비절차적 데이터 조작어(DML)은 사용자가 무슨 데이터를 원하는지만을 명세 - What
2. 절차적 데이터 조작어는 어떻게 데이터를 접근해야하는지 명세 - How
   - PL/SQL(오라클), T-SQL(SQL Server)


## 데이터 언어의 사용 목적에 따른 분류
### DDL (Data Definition Language) 데이터 정의어
Creat, Alter, Drop, Rename ... <br/>
테이블과 같은 데이터 구조를 정의하는데 사용되는 명령어들로 그러한 구조를 생성하거나 변경하거나 삭제하거 이름을 바꾸는 데이터 구조와 관련된 명령어

#### Create
##### 테이블 생성 시 주의사항
- 테이블명은 객체를 의미할 수 있는 단수형
- 다른 테이블의 이름과 중복되지 않아야 한다
- 한 테이블 내 칼럼명이 중복되지 않아야 한다
- 데이터 표준화 관점에 의거하여 칼럼에 대해서 다른 테이블까지 고려하여 데이터베이스 내에서 일관성 있게 사용
- 칼럼 뒤 데이터 유형은 꼭 필요하다
- 테이블명과 칼럼명은 문자로 시작해야한다 (숫자X)
- 벤더에 사전에 정의한 예약어는 쓸 수 없다
- A-Z, a-z, 0-9, _, $, # 문자만 사용 가능

#### 제약조건
무결성을 지키기 위해 사용
```
Create table 테이블명
   ( 칼럼명1 타입 제약조건,
      ...,
     Constraint 제약조건명 Primary key (칼럼명)
   );
```

#### 제약조건의 종류
1. 고유키 (Unique Key) : 중복되지 않는 키, Null 이 가능하나 행을 구별할 수 있어야 한다.
2. 기본키 (Primary Key) : 중복되지 않으면서 Null이 아닌 키 -> 하나의 테이블에 하나의 기본키
3. 외래키 (Foreign Key) : 기본키를 가져와서 쓰는 키, 테이블 간 관계를 정의하기 위해 기본키를 다른 테이블의 외래키로 복사
  -  참조 무결성 제약 조건 선택이 가능하다. -> 삭제하려고 하는 테이블이나 데이터가 외부 다른 테이블에서 참조되고 있다면 삭제가 불가능하게 제약
    - 참조 무결성 Delete/Modify Action
     1. Cascade : 마스터 삭제 시 자식도 삭제
     2. Restrict : 자식 테이블에 PK가 없는 경우만 마스터 삭제
     3. Set Null : 마스터 삭제 시 자식 필드 Null
     4. Set Default : 마스터 삭제 시 자식 해당 필드 Default 값으로 설정
     5. No Action : 참조 무결성을 위반하는 삭제/수정 액션을 취하지 않음
    - 참조 무결성 Insert Action
     1. Automatic : 마스터 테이블에 PK가 없는 경우 마스터 PK를 생성 후 자식 입력
     2. Set Null : 마스터 테이블에 PK가 없는 경우 자식 외부키를 Null 값으로 처리
     3. Set Default : 마스터 테이블에 PK가 없는 경우 자식 외부키를 지정된 기본값으로 입력
     4. Dependent : 마스터 테이블에 PK가 존재할 때만 자식 입력 허용
     5. No Action : 참조 무결성을 위반하는 입력 액션을 취하지 않음
  -  한 테이블에 여러 개 존재할 수 있다.
  -  외래키 값은 Null 을 가질 수 있다.
4. Not Null : 값이 Null 이 아닌 키
5. Check : 입력값이 조건에 맞는지 확인
   - 데이터베이스에서 데이터의 무결성을 유지하기 위해 테이블의 특정 컬럼에 설정하는 제약

#### Alter table 테이블명 (Alter/Add/Drop) ...
- Alter table 테이블명 Alter/Modify Column (컬럼명 데이터유형) ...
- Alter table 테이블명 Drop Column 삭제할컬럼명 ... : 불필요한 컬럼 삭제
- Alter table 테이블명 Add Column ...
- Alter table 테이블명 Rename Column ...

#### Rename 테이블명 To 바꿀테이블명

#### Truncate Table 테이블명
테이블의 데이터를 전부 삭제하고 사용하고 있던 공간을 반납 = 초기 상태
- 해당 테이블의 데이터가 모두 삭제되지만 테이블 자체가 지워지는 것이 아님, 즉 컬럼값은 남아있지만 튜플은 없는 상태이다.
- 해당 테이블에 생성되어 있던 인덱스도 함께 truncate
- Delete 보다 Truncate 가 좋아보이나 원하는 데이터만 골라 삭제가 불가능 하다.

#### Drop Table 테이블명
테이블 자체를 삭제하는 명령어
- 테이블 자체가 모두 지워지며, 해당 테이블에 생성되어 있던 인덱스도 삭제됨
- 테이블 자체가 사라지는 것이므로 데이터도 삭제되고, 사용하던 공간도 모두 반납한다.
- 테이블의 구조와 제약 조건 등도 사라진다.

```
    Drop      |     Truncate     |     Delete
------------------------------------------------
   DDL        |    DML or DDL    |      DML
------------------------------------------------
  Rollback X  |     Rollback X   |   Commit 이전 Rollback O       
------------------------------------------------
  Auto Commit |  Auto Commit     |  사용자 Commit
------------------------------------------------
테이블이 사용했던 |  테이블이 사용했던    |  데이터를 모두
Storage를 모두 |  Storage 중 최초   |  Delete 해도
Release       |  테이블 생성 시     | 사용했던 Storage는
              | 할당된 Storage만   | Release 되지 않음
              |  남기고 Release   |
------------------------------------------------
테이블 정의 자체를|  테이블을 최초 생성된  |  데이터만 삭제
   완전히 삭제   |  초기 상태로 만듦    |
------------------------------------------------
```

#### 삭제 데이터에 대한 로그를 남기려면
테이블 삭제 시, 삭제 데이터에 대한 로그를 남기면서 사용 용도가 없다고 판단한 테이블의 데이터 삭제를 하기 위해서는 Delete from 테이블명 을 사용해준다. 위에 언급한 Truncate 와 Drop 은 로그를 남기지 않는다.


### DML(Data Manipulation Language) 데이터 조작어
- Select : 데이터베이스에 들어 있는 데이터를 조회하거나 검색하기 위한 명령어 - Retrieve 라고도 함
- Insert, Update, Delete ...<br/>
데이터베이스의 테이블에 들어있는 데이터에 변형을 가하는 종류의 명령어들을 의미

#### Select
- Distinct : 중복 요소 제거
- As : Alias, 별칭 지정

#### Select 문장의 실행 순서
From -> Where -> Group by -> Having -> Select -> Order by
* Where 절에서는 AS(Alias)를 사용할 수 없다!

#### Update 테이블명 set 칼럼명=값

#### Insert into 테이블명 (컬럼명) values 값

#### Where 조건절
- 자신이 원하는 자료만 검색하기 위해 자료들에 대해 제한
- 연산자의 종류
  - 비교 연산자 : <, >, ^=, !=
  - SQL 연산자
    - Between A and B <-> Not Between A and B
    - In <-> Not in
    - Like '문자열'
    - Is Null <-> Is not null : Null 을 비교할 때 '=' 같은 비교 연산자는 사용 불가함!
  - 논리 연산자
    - And, Or, Not
  - 연산자 우선 순위
    1. 괄호
    2. 비교 연산자, SQL 연산자
    3. Not 연산자
    4. And
    5. Or


#### Group by 절
1. 소그룹 별 기준 정한 후, Select절에 집계함수 사용
2. 집계함수는 Null값을 가진 행을 제외하고 수행
3. Having 절은 Group by 절의 기준 항목이나 소그룹의 집계 함수를 이용한 조건 표시
4. Having 절에서 제한 조건을 두어 조건을 만족하는 내용만 출력
5. Having 절은 Group by 앞/뒤에 위치 가능
6. 집계함수는 Where절에 올 수 없음. => Group by 보다 Where 이 먼저 수행 되므로

#### Having 절
1. Where 절에서는 집계 함수를 사용할 수 없다.
2. 집계된 결과 집합을 기준으로 특정 조건을 주고 싶은 경우 사용
3. 그룹을 나타내는 결과 집합의 행에 조건이 적용

#### Order by 절
```
   Select 컬럼명 From 테이블명 [Where 조건식]
   [Group by 칼럼/표현식]
   [Having 그룹 조건식]
   [Order by 칼럼/표현식 [Asc/Desc]]
```
1. 기본적인 행 순서는 ASC(오름차순)
2. 숫자형 데이터 타입은 오름차순의 경우 가장 작은 값부터, 날짜형 데이터 타입은 날짜값이 가장 빠른 값이 먼저 출력된다.
3. 컬럼명 대신 Alias나 칼럼 순서를 나타내는 정수를 서로 혼용하여 사용 가능
4. 목적에 맞는 특정 칼럼을 기준으로 정렬
5. Group by 절을 사용하면 Order by 절에 집계함수를 사용할 수 있음

```
   Order by 1, 2
```
* Order by 절에 숫자가 들어온 경우, 숫자는 칼럼의 순서를 의미한다.
* 숫자가 조회되었을 때 칼럼순서에 따라 인덱스를 붙여준 것 (1부터 시작)

#### 문자 유형 크기 비교 방법 (양쪽이 모두 Char 타입인 경우)
1. 길이가 서로 다르면 작은 쪽에 공백을 추가하여 길이를 같게 한다.
2. 서로 다른 문자가 나올 때까지 비교
3. 달라진 첫번째 값에 따라 크기를 결정 (AscII)
4. 공백의 수만 다르다면 같은 값으로 결정 -> 'ABC', 'ABC ' 같은 것으로 판단

#### 문자 유형 크기 비교 방법 (비교 연산자 중 한쪽이 Varchar인 경우)
1. 서로 다른 문자가 나올 때까지 비교
2. 길이가 서로 다르면 짧은 것이 끝날 때까지만 비교
3. 길이가 긴 것이 크다고 판단
4. 길이가 같고 다른 것이 없다면 같다고 판단
5. Varchar 는 공백도 문자로 판단 -> 'ABC', 'ABC ' 다른 것으로 판단

#### 문자 유형 크기 비교 방법 (상수값과 비교)
1. 상수쪽을 변수 타입과 동일하게 바꾸고 비교
2. 변수가 Char면 Char 유형 타입의 경우를 적용
3. 변수가 Varchar면 Varchar 유형을 적용


### DCL (Data Control Language) 데이터 제어어
Grant, Revoke ... <br/>
- 데이터베이스에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 명령어
- 데이터 보호와 보안을 위해 유저/권한 관리

#### Grant
- 권한을 부여하는 DCL 명령어
- Grant 권한명 To 권한을 뷰여할 유저명;
  - Create Session : 유저가 로그인 할 수 있게 해줌
  - Create Table : 테이블을 생성할 수 있게 해줌

#### Revoke 
- 부여한 권한을 회수하는 DCL 명령어

#### Role
1. Grant 를 일일이 지정하기 번거롭기 때문에
2. Role을 생성하여 각종 권한을 부여한 후, Role 을 다른 Role이나 유저에게 부여
3. Role에 포함된 권한들이 필요한 유저에게 Role만 부여하여 빠르고 정확하게 필요한 권한을 부여할 수 있다.
4. Role을 생성하여 Role 에 권한을 부여할 때도 Grant문을 쓴다.

#### Connect, Resource Role이 보유한 권한들
1. Connect : Create Session
2. Resource : Create Cluster
3. Create Type
4. Create Table
5. Create Procedure
6. Create Trigger

### TCL (Transaction Control Language) 트랜잭션 제어어
Commit, Rollback ... <br/>
논리적인 작업의 단위를 묶어서 DML에 의해 조작된 결과를 트랜잭션(작업단위)별로 제어하는 명령어

#### Commit
- DML 구문이 성공할 때,
- 데이터에 대한 변경사항을 데이터베이스에 영구적으로 저장

#### Rollback
- DML 구문에 오류가 있을 때
- 데이터에 대한 변경사항을 모두 폐기하고 변경 전 상태로 되돌리는 명령
- 테이블 내 입력한 데이터나 수정한 데이터, 삭제한 데이터에 대하여 Commit 이전에는 변경사항을 취소할 수 있는데, 이를 Rollback 하는 것
- 데이터 변경 사항이 취소되어 데이터 이전 상태로 복구되며, 관련된 향에 대한 Locking 이 풀리고 다른 사용자들이 데이터 변경을 할 수 있게 된다.
- 커밋 되지 않은 상태의 모든 트랜잭션을 롤백하는 것이다.
- 최초의 Begin Transation 시점까지 Rollback 이 수행됨
```
Begin Transaction : 트랜잭션 실행
Commit Transaction / Rollback Transaction : 트랜잭션 종료
```

#### 트랜잭션 완료의 의미
1. 변경사항이 데이터베이스에 반영
2. 이전 데이터가 영영 사라져버린다.
3. 모든 사용자는 결과를 볼 수 있다.
4. 관련 행은 잠금이 풀리고 다른 사용자가 변경 가능하다.

#### Commit/Rollback 이전의 데이터 상태
1. 메모리 Buffer만 쌓여있으므로 데이터 변경 이전 상태로 복구 가능
2. 현재 사용자는 Select 문장으로 결과 확인 가능
3. 다른 사용자는 현재 사용자가 수행한 명령의 결과를 볼 수 없다.
4. 변경된 행은 잠금이 설정되어서 다른 사용자가 변경할 수 없다.

#### 커밋/롤백을 실행하지 않아도 자동으로 트랜잭션이 종료되는 경우
1. Create, Alter, Drop, Rename, Truncate table 등의 DDL 언어를 수행 시 전후 시점에 자동 커밋
2. DML 문장 이후 커밋 없이 DDL 문장이 실행되면 자동 커밋
3. 데이터베이스를 정상적으로 접속 종료하면 자동 커밋
4. 애플리케이션의 이상 종료로 데이터베이스와의 접속이 단절되었을 때 트랜지션이 자동 롤백

#### Savepoint
롤백할 때 트랜잭션에 포함된 전체 작업을 롤백하는 것이 아닌, 현 시점의 Savepoint 까지 트랜잭션의 일부만 롤백해준다.


## 참조 동작 (Referential Action)
### Delete/Modify Action
1. Cascade : 참조하는 자식도 같이 삭제
2. Restrict : 자식 테이블에 PK값이 없는 경우만 삭제 허용, PK가 있으면 취소됨
3. Set Null : 마스터 삭제 시 자식 해당 필드 Null 처리
4. Set Default : 마스터 삭제 시 자식 해당 필드 Default 값으로 설정

### Insert Action
1. Automatic : 마스터 테이블에 PK가 없는 경우 마스터 PK를 생성하고 자식 입력
2. Set Null : 마스터 테이블에 PK가 없는 경우 자식 외부키를 Null 로 처리
3. Set Default : 마스터 테이블에 PK가 없는 경우 자식 외부키를 Default 로 설정
4. Dependent : 마스터 테이블에 PK가 존재할 때 자식 입력 허용



## Null
### Null 특성
- Null 은 아직 정의되지 않은 값으로 0이나 공백과는 다른다.
- 공백은 문자, 0은 숫자이다.
- 테이블을 생성할 때 Not Null 또는 PK로 정의되지 않은 모든 데이터 유형은 널값을 포함할 수 있다.
- 널 값을 포함하는 연산의 경우 결과값도 널 값이다.
`Null + 2 = Null, Null * 2 = Null, Null / 2 = Null ...`
- 결과값을 Null 이 아닌 다른 값을 얻고자 할 땐 Nvl, IsNull 함수를 사용한다.
- 널 값의 대상이 숫자인 경우 주로 0으로, 문자인 경우는 공백보단 x 같이 의미없는 문자로 바꾸는 경우가 많다.


## Top N 쿼리
### Top N 쿼리란, 특정 순서로 데이터를 부분적으로 쿼리하는 것

#### Rownum 슈도 컬럼
SQL 처리 결과 시 각 행에 임시로 부여되는 일련번호 - Oracle 문법
- 데이터의 일부가 먼저 추출된 후 데이터에 대한 정렬 작업이 이루어진다.
- 인라인 뷰를 이용하여 집합을 정렬한 후 rownum 적용시켜 올바른 SQL문 사용해야 함

#### Top 절
결과 집합으로 출력되는 행의 수를 제한 - SQL server
  ex. Top (표현식) [Percent] [With ties]
  - 표현식 : 반환할 행 수 지정
  - Percent : 쿼리 결과 집합에서 처음 표현식%의 행만 반환됨 - 표현식 건이 아니라, 표현식의 %만큼 반환
  - With ties : Order by 절이 지정된 경우에만 사용 가능하며 마지막 행과 같은 값이 있으면 추가행이 출력되도록 지정

#### Row Limiting 절
Ansi 표준으로 어디서든 다 사용 가능
```
[Offset N {Row | Rows}]
[Fetch {First | Next} [{rowcount | percent}] {Row | Rows} {Only | With ties}]
```
- Offset N : 건너뛸 행의 개수 지정
- Fetch : 반환할 행의 개수 또는 백분율 지정
- Only : 지정된 행의 개수 또는 백분율 지정
- With ties : 마지막 행에 대한 동순위 포함해서 반환
