## Oracle VS SQL Server

### Oracle
- DDL 문장 수행 후 Auto Commit
- DML 수행 후 TCL 처리해줘야 한다.
- Savepoint 세이브포인트명 ... Rollback To 세이브포인트명
- Order by 에서 Null 을 가장 큰 값으로 간주
- Outer Join 구문을 사용할 때 (+) 기호를 사용하여 처리한다. -> +가 있는 쪽 테이블이 Null 값을 포함하라는 의미
  - 예를 들어 Where A.col = B.col(+) 라면, A Left Outer Join B 인 것이다.
  - Where A.col(+) = B.col(+) 는 Full Outer Join



#### 오라클에서 제공하는 유저
1. Scott : 테스트용 샘플 유저
2. Sys : 백업 복수 등의 DB의 모든 관리 기능 수행 가능. DBA 권한을 부여 받은 유저, 최상위 관리자 계정
3. System : 백업/복수 등 일부 기능을 제외한 모든 시스템 권한을 부여받은 DBA 계정, 오라클 설치 시 패스워드 설정하여 Sys 바로 밑



### SQL Server
- DDL 문장 수행 후 사용자가 Commit 이 필요
- Auto Commit 모드이므로 DML 수행 후 TCL 을 처리할 필요가 없다.
- Save Transaction 세이브포인트명 ... Rollback Transaction 세이브포인트명
- 여러 개의 칼럼을 동시에 수정하는 구문은 지원하지 않는다
- 괄호를 사용하지 않는다
- Order by 에서 Null 을 가장 작은 값으로 간주
