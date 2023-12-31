# Oracle VS SQL Server
## Database concept
오라클과 SQL Server 의 가장 큰 차이점은 SQL Server 의 경우 인스턴스 하나를 여러 개의 DB들이 공유할 수 있다는 것이다.

## Client 접속 방식
오라클의 경우 Dedicated & Shared Server 의 2가지 클라이언트 접속 방식을,
SQL Server 의 경우 오라클의 Shared Server 방식을 이용한다.

### Oracle
- PL/SQL (Procedural Language/SQL) 언어 사용 -> 검색이나 업데이트용 언어
- 리눅스/유닉스 환경에서 널리 사용됨
- 대용량 정보관리 성능이 좋음
- DDL 문장 수행 후 Auto Commit
- DML 수행 후 TCL 처리해줘야 한다.
- 데이터베이스가 모든 스키마와 사용자간에 공유 됨 => 한 서버 당 한 개의 데이터베이스
- Savepoint 세이브포인트명 ... Rollback To 세이브포인트명
- Order by 에서 Null 을 가장 큰 값으로 간주
- Outer Join 구문을 사용할 때 (+) 기호를 사용하여 처리한다. -> +가 있는 쪽 테이블이 Null 값을 포함하라는 의미
  - 예를 들어 Where A.col = B.col(+) 라면, A Left Outer Join B 인 것이다.
  - Where A.col(+) = B.col(+) 는 Full Outer Join
- 행 기반 DB 이므로 데이터를 액세스할 때 행 전체 칼럼을 메모리에 로드 -> Select 절에 기술되지 않는 칼럼으로 정렬 가능함
- 프로시저, 함수 및 변수가 패키지로 캡슐화 됨
- VARCHAR 인 컬럼에 "" 을 입력하면 Null 로 입력됨


### SQL Server (MSSQL)
- T-SQL (Transact-SQL) 언어 사용
- 윈도우즈 환경에서 특화
- DDL 문장 수행 후 사용자가 Commit 이 필요
- Auto Commit 모드이므로 DML 수행 후 TCL 을 처리할 필요가 없다.
- 사용자 간 데이터베이스가 공유되지 않음 => 한 서버당 다수의 데이터베이스 생성 가능 (멀티 데이터베이스)
- Save Transaction 세이브포인트명 ... Rollback Transaction 세이브포인트명
- 여러 개의 칼럼을 동시에 수정하는 구문은 지원하지 않는다
- 괄호를 사용하지 않는다
- Order by 에서 Null 을 가장 작은 값으로 간주
- 패키지가 존재하지 않음
- VARCHAR 인 컬럼에 ""로 입력하면 ""(공백)으로 입력 됨

#### SQL Server의 계층형 질의
- CTE (Common Table Expression)을 재귀호출하여 계층 구조를 전개 (최상위 -> 하위순)
- 앵커 멤버를 실행하여 기본 결과 집합을 만들고 이후 개체 멤버를 지속적으로 실행한다.


#### 오라클에서 제공하는 유저
1. Scott : 테스트용 샘플 유저
2. Sys : 백업 복수 등의 DB의 모든 관리 기능 수행 가능. DBA 권한을 부여 받은 유저, 최상위 관리자 계정
3. System : 백업/복수 등 일부 기능을 제외한 모든 시스템 권한을 부여받은 DBA 계정, 오라클 설치 시 패스워드 설정하여 Sys 바로 밑


#### PL/SQL
1. Block 구조 -> 각 기능별로 모듈화가 가능
2. 변수, 상수 등을 선언하여 SQL 문장 간 값을 교환
3. If, Loop 등 절차형 언어를 사용하는 절차적 프로그램
4. DBMS 정의 에러나 사용자 정의 에러를 정의 가능
5. 응용 프로그램의 성능 향상
6. 여러 SQL 문장을 Block 으로 묶고 한번에 Block 을 서버로 보내므로 통신량을 줄일 수 있음
7. Procedure, User Defined function, Trigger 객체를 작성 가능 -> 하나의 트랜젝션이 아닌 트랜젝션을 분할하여 가능
8. Procedure 내부의 절차적 코드는 PL/SQL 엔진이 처리하고 일반적인 SQL문장은 SQL실행기가 처리한다.
9. 동적 SQL, DDL 문장을 실행할 때 execute immediate 를 사용한다.

#### PL/SQL 에서 데이터베이스 Cursor를 사용할 때
- 명시적 Cursor란 사용자가 직접 정의해서 사용하는 커서 <-> 묵시적 커서는 데이터베이스가 내부적으로 사용하는 커서
- 모든 커서는 사용하기 전 선언해줘야한다.
```
선언
Cursor 커서명[(매개변수1, ...)]
Is
Select 문장;
```

```
커서 오픈
Open 커서명[(매개변수1, ...)];

커서 클로즈
Close 커서명;
```
사용이 완료된 커서는 반드시 Close 해줘야 함

```
실제 테이블에서 데이터를 읽어올 때 (Fetch)
  Loop
    Fetch 커서명 Into 변수1, ...;
    Exit When 커서명%Notfound;
  End Loop;
```

#### 저장형 프로시저는 SQL 을 로직과 함께 데이터베이스 내 저장해 놓은 명령문의 집합
#### 사용자 정의함수(저장형 함수)는 다른 SQL을 통해 호출되고 그 결과를 리턴하는 SQL의 보조적인 역할을 함

#### Trigger
- 특정 테이블에 Inset, Update, Delete 같은 DML문이 수행 됐을 때 DB에서 자동으로 동작하도록 작성된 프로그램
- 데이터의 무결성과 일관성을 위해 사용자 정의 함수를 사용
- Commit/Rollback 같은 TCL문은 사용 불가함 -> 다만 프로시저는 TCL문 사용이 가능
- 데이터베이스에 로그인하는 작업도 정의 가능함

```
  프로시저          |          트리거
-------------------------------------------
Create Procedure  |    Create Trigger
execute 로 실행    |        자동 실행
    TCL OK        |        TCL X
```
