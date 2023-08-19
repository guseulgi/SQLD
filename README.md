# SQL D
---
SQL D 대비 정리

# 데이터 모델링
## 데이터 모델링의 이해
### 데이터 모델링이란?
정보 시스템을 구축하기 위한 데이터 관점의 업무 분석 기법 <br/>
현실 세계의 데이터에 대해 약속된 표기법에 의해 표현하는 과정 <br/>
데이터베이스를 구축하기 위한 분석/설계의 과정 <br/>
<br/>

#### 모델링의 특징
현실 세계를 일정한 형식에 맞추어 표현하는 추상화의 의미 <br/>
복잡한 현실을 제한된 언어나 표기법을 통하여 이해하기 쉽게 하는 단순화의 의미를 가지고 있다. <br/>
애매모호함을 배제하고 누구나 이해가 가능하도록 정확하게 현상을 기술하는 정확화의 의미를 가진다. <br/>
<br/>

#### 데이터 모델링의 유의점
- 중복
    - 데이터 모델은 같은 데이터를 사용하는 사람, 시간, 장소를 파악하는데 도움을 줌으로써 데이터베이스가 여러 장소에 같은 정보를 저장하는 잘못을 하지 않도록 한다.
- 비유연성
    - <strong>데이터 정의를 데이터의 사용 프로세스와 분리함</strong>으로써 데이터 모델링은 데이터 혹은 프로세스의 작은 변화가 애플리케이션과 데이터베이스에 중대한 변화를 일으킬 수 있는 가능성을 줄인다.
- 비일관성
    - 데이터 모델을 어떻게 설계했느냐에 따라 사소한 업무 변화에도 데이터 모델이 수시로 변경됨으로써 유지보수의 어려움을 가중 시킬 수 있다.
    - 데이터와 데이터 간의 상호 연관 관계에 대해 명확하게 정의한다면 데이터의 중복이 없더라도 비일관성이 발생하는 일들을 사전에 예방하는데 도움을 준다.
<br/>

#### 데이터 모델링에 개념

1. 개념적 데이터 모델링 <br/>
  전사적 데이터 모델링을 수행하거나, EA 수립 시 많이 하며, 추상화 수준이 높고 업무 중심적이고 포괄적인 수준의 모델링을 진행하는 것
2. 논리적 데이터 모델링 <br/>
  시스템으로 구축하고자 하는 업무에 대해 key, 속성, 관계 등을 정확하게 표현, 재사용성이 높다.
3. 물리적 데이터 모델링 <br/>
  실제로 데이터베이스에 이식할 수 있도록 성능, 저장 등의 물리적인 성격을 고려한 데이터 모델링
<br/>

### 스키마란
- 데이터베이스의 구조와 제약조건에 관해 전반적인 명세를 기술한 것
- 데이터 사전에 저장된다.
- 현실세계의 특정한 부분의 표현으로, 특정 데이터 모델을 이용하여 만들어진다.
- 시간에 따라 불변인 특성
- 데이터의 구조적 특성을 의미
- 인스턴스에 의해 규정된다.

#### ANSI-SPARC 에서 정의한 스키마 구조의 3단계
1. 외부 스키마
    현실세계에 존재하는 데이터들을 어떤 형식, 구조, 배치 화면을 통해 사용자에게 보여줄 것인가 <br/>
   같은 데이터베이스에 대해 서로 다른 관점을 정의할 수 있도록 허용
2. 개념 스키마 <br/>
  모든 사용자 관점을 통합한 조직 전체 관점의 통합적 표현이자 DB 정의 <br/>
  모든 응용시스템들이나 사용자들이 필요로하는 데이터를 통합한 조직 전체의 DB를 기술한 것으로 DB에 저장되는 데이터와 그들 간의 관계를 표현하는 스키마
3. 내부 스키마
    데이터베이스의 물리적 저장구조 <br/>
    데이터의 실제 저장방법을 기술, 물리적인 저장장치와 밀접한 계층으로 시스템 프로그래머나 시스템 설계자가 보는 관점을 스키마

#### -> 데이터 모델링은 통합 관점의 뷰를 가지고 있는 개념 스키마를 만드는 과정이다. <br/>



### ERD
- 1976 년 피터첸에 의해 Entity-Relationship Model 이라는 표기법이 만들어졌다.
- 일반적으로 ERD를 작성하는 방법은,
  1. 엔터티 도출
  2. 엔터티 배치
  3. 관계 설정
  4. 관계명 기술
  5. 관계의 참여도 및 필수 여부 기술
- 관계의 명칭은 관계 표현에 있어서 매우 중요한 부분에 해당된다.

### 엔터티
#### 엔터티의 특징
- 반드시 해당 업무에서 필요하고 관리하고자 하는 정보여야 한다.
- 유일한 식별자에 의해 식별이 가능해야 한다.
- 하나의 엔터티는 영속적으로 존재하는 <strong>두 개 이상의 인스턴스의 집합</strong>이여야 한다.
- 엔터티는 업무 프로세스에 의해 이용되어야 한다.
- 엔터티는 반드시 두 개 이상의 속성이 있어야 한다.
- 엔터티는 다른 엔터티와 최소 한 개 이상의 관계가 있어야 한다.
- 다만 공통코드, 통계성 엔터티의 경우엔 관계를 생략할 수 있다.
<br/>

#### 엔터티의 종류
- 기본(키) 엔터티
    - 업무에 원래 존재하는 정보
    - 다른 엔터티로부터 주식별자를 상속받지 않고 자신의 고유한 주식별자를 가진다.
    - 타 엔터티의 부모 역할을 하게 된다.
- 중심(메인) 엔터티
    - 기본 엔터티로부터 발생, 업무에서 중심적인 역할을 한다.
    - 데이터의 양이 많이 발생되고 다른 엔터티와의 관계를 통하여 많은 행위 엔터티를 생성
- 행위 엔터티
    - 두 개 이상의 부모 엔터티로부터 발생되고 자주 내용이 바뀌거나 데이터량이 증가
<br/>

#### 속성
업무에서 필요로 하는 인스턴스에서 관리하고자하는 의미상 더이상 분리되지 않는 최소의 데이터 단위
- 엔터티에 대한 자세하고 구체적인 정보를 나타낸다.
- 하나의 엔터티는 두 개 이상의 속성을 가진다.
- 하나의 인스턴스에선 각각의 속성은 하나의 속성값을 가져야 한다. (두 개 이상의 속성값은 X)
- 속성도 집합이다.
- 각 속성은 가질 수 있는 값의 범위가 있는데, 이를 <strong>도메인</strong>이라 한다. 앤터티 내에서 속성에 대한 데이터 타입과 크기, 제약 사항을 지정하는 것이다.
<br/>


#### 엔터티, 인스턴스, 속성, 속성값 사이의 관계
- 한개의 엔터티는 두 개 이상의 인스턴스의 집합이어야 한다.
- 한 개의 엔터티는 두 개 이상의 속성을 갖는다.
- 한 개의 속성은 한 개의 속성값을 가진다.


#### 속성의 특성에 따른 분류
- 기본 속성
  - 원래 가지고 있어야 하는 속성
- 설계 속성
  - 업무상 필요한 데이터 이외에 데이터 모델링을 위해 업무를 규칙화하기 위한 속성을 만들거나 변형하여 정의하는 속성
- 파생 속성
  - 기본 속성에서 계산된 속성
  - 데이터를 조회할 때 빠른 성능을 할 수 있도록 하기 위해
 #### 속성의 명칭 부여
 - 해당 업무에서 사용하는 이름 부여
 - 서술식 속셩명은 지양
 - 약어 사용 지양
 - 전체 데이터모델에서 유일성 확보


#### 관계
- 존재에 의한 관계와 행위에 의한 관계로 구분된다.
- ERD에서는 관계를 연결할 때 존재와 행위를 구분하지 않고 단일화된 표기법을 사용한다.
- 그러나 UML에는 클래스다이어그램의 관계 중 연관관계와 의존관계가 있으며, 실선과 점선의 표기법으로 다르게 표현해준다.

- 관계의 표기법은 관계명, 관계차수, 선택성의 3가지 개념으로 표현한다.
    - 관계명 : 관계의 이름
    - 관계차수 : 1:1, 1:M, N:M 같이 관계의 기수성을 나타냄
    - 선택성 : 필수 관계 또는 선택 관계
- 관계를 체크하는 사항
  1. 두 개의 엔터티 사이에 관심 있는 연관 규칙이 존재하는가?
  2. 두 개의 엔터티 사이에 정보의 조합이 발생되는가?
  3. 업무기술서, 장표에 관계연결을 가능하게 하는 동사가 있는가? *동사는 관계를 서술하는 업무기술서의 가장 중요한 사항임
  4. 업무기술서, 장표에 관계연결에 대한 규칙이 서술되어 있는가?
- 관계 표기
  - 기준 엔터티를 한 개 또는 각(Each)으로 읽는다
  - 대상 엔터티의 관계참여도, 즉 개수를 읽는다
  - 관계선택사양과 관계명을 읽는다
<br/>

#### 식별자의 종류
- 엔터티 내에서 대표성을 가지는가에 따라
  - 주식별자 : 엔터티 내에 각 어커런스를 구분할 수 있는 구분자이며, 타 엔터티와 참조관계를 연결할 수 있는 식별자
  - 보조식별자 : 엔터티 내에서 각 어커런스를 구분할 수 있는 구분자이나 대표성을 가지지 못해 참조관계 연결을 못함
  - 어커런스 : 정의된 레코드의 구조에 따라 데이터베이스에 구체적이고 실제적인 정보를 저장하고 있는 데이터
- 엔터티 내에서 스스로 생성되었는지 여부에 따라
  - 내부 식별자 : 엔터티 내부에서 스스로 만들어지는 식별자
  - 외부 식별자 : 타 엔터티와의 관계를 통해 타 엔터티로부터 받아오는 식별자
- 단일 속성으로 식별이 되는가에 따라 
  - 단일식별자 : 하나의 속성으로 구성된 식별자
  - 복합식별자 : 둘 이상의 속성으로 구성된 식별자
- 원래 업무적으로 의미가 있던 식별자 속성을 대체하여 일련번호와 같이 새롭게 만든 식별자를 구분하기 위해
  - 본질식별자 : 업무에 의해 만들어진 식별자
  - 인조식별자 : 업무적으로 만들어지지 않지만 원조식별자가 복잡한 구성을 가지고 있기에 인위적으로 만들어지는 식별자

#### 주식별자를 지정할 때 고려해야 하는 사항
1. 주식별자에 의해 엔터티 내의 모든 인스턴스들이 유일하게 구분되어야 한다.
2. 주식별자를 구성하는 속성의 수는 유일성을 만족하는 최소의 수가 되어야 한다.
3. 지정된 식별자의 값은 자주 변하지 않는 것이어야 한다.
4. 주식별자가 지정이 되면 반드시 값이 들어와야 한다.
5. 복합으로 주식별자를 구성할 경우 너무 많은 속성을 포함하지 않도록 한다.
6. 명칭 내역 등과 같이 이름으로 기술되는 것들은 가능하면 주식별자로 정하지 않는다.
#### 주식별자의 특징
1. 유일성
    - 주식별자에 의해 엔터티내 모든 인스턴스들을 유일하게 구분함
2. 최소성
    - 주식별자를 구성하는 속성의 수는 유일성을 만족하는 최소의 수가 되어야 함
3. 불변성
    - 주식별자가 한번 특정 엔터티에 지정되면 그 식별자의 값은 변하지 않아야 함
4. 존재성
    - 주식별자가 지정되면 반드시 데이터 값이 존재 (Null X)
  

#### 식별자관계
- 강한 연결관계 표현
- 자식 주식별자의 구성에 포함
- 실선으로 표기
- 반드시 부모 엔터티 종속
- 자식 주식별자구성에 부모 주식별자 포함 필요

#### 비식별자관계
- 약한 연결관계 표현
- 자식 일반 속성에 포함
- 점선 표현
- 약한 종속관계
- 자식 주식별자 구성을 독립적으로 구성
- 부모쪽의 관계참여가 선택관계
1. 관계의 강약을 분석하여 상호간에 연관성이 약할 경우, 비식별자 관계를 고려
2. 자식 테이블에서 독립적인 기본키의 구조를 가지기 원하면 비식별자 관계를 고려
3. 부모엔터티의 주식별자를 자식엔터티에서 받아 손자엔터티까지 계속 흘려보내기 위해 비식별자 관계를 고려
4. 모든 관계가 식별자 관계로 연결되면 Where 절에서 비교하는 항목이 증가되어 조인에 참여하는 테이블에 따라 SQL 문장이 길어지므로 복잡성이 증가하는 것을 방지하기 위해 비식별자 관계를 고려
5. 부모엔터티의 인스턴스가 자식 엔터티와 같이 소멸되는 경우는 식별자 관계를 고려



## 데이터 모델과 성능
#### 성능 데이터 모델링?
데이터베이스 성능 향상을 목적으로, 설계 단계의 데이터 모델링 때부터 성능과 관련된 사항이 데이터 모델링에 반영될 수 있도록 하는 것

#### 성능 데이터 모델링 수행 절차
1. 데이터 모델링을 할 때 정규화를 정확하게 수행
2. 데이터베이스 용량산정을 수행
3. 데이터베이스에 발생되는 트랜잭션의 유형을 파악
4. 용량과 트랜잭션의 유형에 따라 반정규화를 수행
5. 이력모델의 조정, PK/FK 조정, 슈퍼타입/서브타입 조정 등을 수행
 - 슈퍼타입과 서브타입의 관계는 배타적 관계와 포괄적 관계가 있는데, 배타적 관계는 고객이 개인이거나 법인고객인 경우를 의미하며 포괄적인 관계는 고객이 개인고객일 수도 있고 법인고객일 수도 있는 것  
6. 성능 관점에서 데이터 모델을 검증

* 정규화가 항상 조회 성능을 저하시킨다는 것은 잘못된 생각이며 기본적으로 중복된 데이터를 제거함으로써 조회성능을 향상시킬 수 있다.

#### 정규화
- 데이터의 일관성, 최소한의 데이터 중복, 최소한의 데이터 유연성을 위한 방법
- 데이터를 분해하는 과정
- 정규화된 모델은 테이블이 분해된다.
- 불필요한 데이터를 입력하지 않아도 되기 때문에 중복 데이터가 제거된다.

#### 정규화 절차
1. 제 1정규화
   - 속성의 원자성을 갖도록 테이블을 분해
   - 속성의 중복값을 제거
   - 기본키 설정
2. 제 2정규화
   - 기본키가 2개 이상의 속성으로 이루어진 경우, 부분 함수 종속성을 제거하여 완전 함수 종속을 만족하도록 테이블을 분해하는 것
   - 부분 함수 종속성이란 기본키가 2개 이상인 칼럼으로 이루어진 경우에만 발생 (기본키가 1개면 스킵)
   - 복합 인스턴스에 대해 각 인스턴의 종속적 중복을 삭제
3. 제 3정규화
   - 기본키를 제외한 칼럼 간에 종속성 제거
   - 이행 함수 종속성을 제거
   - 이행적 종속은 A->B, B->C가 성립할 땐 A->C가 성립되는 것
   - 일반 속성의 종속성을 제거
4. BCNF 정규화
   - 모든 결정자가 후보키가 되도록 테이블을 분해하는 것
   - BCNF 는 복수의 후보키가 있고 후보키들이 복합 속성이어야 하며, 서로 중첩되어야 한다.
5. 제 4정규화
   - 여러 칼럼들이 하나의 칼럼을 종속시키는 경우, 분해하여 다중값 종속성을 제거
   - 다치 종속성을 제거
6. 제 5정규화
   - 조인에 의해 종속성이 발생되는 경우 분해
  
#### 정규화의 문제점
정규화는 데이터 조회 시 조인을 유발하므로 cpu와 메모리를 많이 사용하게 된다.
-> 조인으로 인하여 성능이 저하되는 문제를 반정규화로 해결할 수 있다. 다만 반정규화는 데이터를 중복시키기에 다른 문제점을 발생시킨다.



#### 반정규화
- 데이터베이스의 성능 향상을 위해, 데이터 중복을 허용하고 조인을 줄이는 데이터베이스 성능 향상 방법
- 데이터 무결성이 깨질 수 있는 위험을 감수하고 조회 속도를 향상시키지만, 데이터 모델의 유연성을 낮아진다.

#### 반정규화를 수행하는 이유
- 정규화에 충실하여 종속성, 활용성은 향상 되었지만 수행속도가 느려진 경우
- 다량의 범위를 자주 처리하는 경우
- 특정 범위의 데이터만 자주 처리하는 경우
- 요약/집계 정보가 자주 요구되는 경우

#### 반정규화 절차
1. 대상 조사 및 검토 : 데이터 처리 범위, 통계성 등을 확인하여 반정규화 대상을 조사
 - 범위 처리 빈도수 조사
 - 대량의 범위 처리 조사
 - 통계성 프로세스 조사
 - 테이블 조인 개수  
2. 다른 방법 검토 : 반정규화를 수행하기 전 다른 방법이 있는지 검토
    - 뷰 테이블
    - 클러스터링 적용
    - 인덱스의 조정
    - 응용 애플리케이션
3. 반정규화 수행 : 테이블, 속성, 관계 등을 반정규화한다.

#### 반정규화 대상에 대한 다른 방법으로 처리
- 지나치게 많은 Join이 걸려 데이터를 조회하는 작업이 기술적으로 어려울 경우 View 를 사용하여 이를 해결
- 대량의 데이터처리나 부분처리에 의해 성능이 저하되는 경우 클러스터링을 적용하거나 인덱스를 조정함으로써 성능을 향상시킬 수 있음
- 대량의 데이터는 PK의 성격에 따라 부분적인 테이블로 분리 가능 (Partitioning 기법이 적용)
- 응용 애플리케이션에서 로직을 구사하는 방법을 변경하여 성능을 향상시킬 수 있음

##### 클러스터링 (Clustering)
디스크로부터 데이터를 읽어오는 시간을 줄이기 위해 조인이나 자주 사용되는 테이블의 데이터를 디스크의 같은 물리적인 위치에 정렬해서 저장시키는 방법 <br/>
클러스터링 인덱스라는 것은 인덱스 정보를 저장할 때, 물리적으로 정렬해서 저장하는 방법으로
조회 시 인접 블록을 연속적으로 읽기 때문에 성능이 향상된다.

#### 반정규화 기법
- 컬럼의 반정규화
  - 계산된 칼럼(파생칼럼) 추가
  - 중복 칼럼 추가
  - 이력 테이블 컬럼 추가
  - PK에 의한 칼럼 추가
  - 응용 시스템 오작동을 위한 칼럼 추가
- 테이블의 반정규화
  - 테이블 명함
    - 1:1 관계 테이블 병합
    - 1:M 관계 테이블 병합
    - 슈퍼/서브 타입 테이블 병합
  - 하나의 테이블을 두 개 이상의 테이블로 분할 (수직/수평분할)
  - 테이블 추가
    - 중복 테이블 추가
    - 통계 테이블 추가
    - 이력 테이블 추가
    - 부분 테이블 추가
- 테이블 수평 분할
  - 하나의 테이블에 있는 값을 기준으로 테이블을 분할



---
# SQL 기본 및 활용
## 트랜잭션
데이터베이스의 논리적 연산단위로서 밀접히 관련되어 분리될 수 없는 1개 이상의 데이터베이스 조작

#### 트랜잭션의 특징
1. 원자성 : 트랜잭션에 정의된 연산들은 모두 성공적으로 실행되던지 아니면 전혀 실행되지 않은 상태로 남아 있어야 한다.
2. 일관성 : 트랜잭션이 실행되기 전의 데이터베이스 내용이 잘못 되어 있지 않다면 트랜잭션이 실행된 이후에도 데이터베이스의 내용에 잘못이 있으면 안된다.
3. 고립성/독립성 : 트랜잭션이 실행되는 도중에 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어선 안된다.
4. 지속성 : 트랜잭션이 성공적으로 수행되면 그 트랜잭션이 갱신한 데이터베이스의 내용은 영구적으로 저장된다.
## SQL 문장 종류
#### DDL (Data Definition Language) 데이터 정의어
Creat, Alter, Drop, Rename ... <br/>
테이블과 같은 데이터 구조를 정의하는데 사용되는 명령어들로 그러한 구조를 생성하거나 변경하거나 삭제하거 이름을 바꾸는 데이터 구조와 관련된 명령어

##### 제약조건
무결성을 지키기 위해 사용
##### 제약조건의 종류
1. 고유키 (Unique Key) : 중복되지 않는 키
2. 기본키 (Primary Key) : 중복되지 않으면서 Null이 아닌 키
3. 외래키 (Foreign Key) : 기본키를 가져와서 쓰는 키
4. Not Null : 값이 Null 이 아닌 키
5. Check : 입력값이 조건에 맞는지 확인

##### Alter table 테이블명 (Alter/Add/Drop) ...
- Alter table 테이블명 Alter Column (컬럼명 데이터유형) ...
- Alter table 테이블명 Drop Column 삭제할컬럼명 ... : 불필요한 컬럼 삭제

##### Rename 테이블명 To 바꿀테이블명

##### Truncate
테이블의 데이터를 전부 삭제하고 사용하고 있던 공간을 반납
- 해당 테이블의 데이터가 모두 삭제되지만 테이블 자체가 지워지는 것이 아님, 즉 컬럼값은 남아있지만 튜플은 없는 상태이다.
- 해당 테이블에 생성되어 있던 인덱스도 함께 truncate
- Delete 보다 Truncate 가 좋아보이나 원하는 데이터만 골라 삭제가 불가능 하다.

##### Drop
테이블 자체를 삭제하는 명령어
- 테이블 자체가 모두 지워지며, 해당 테이블에 생성되어 있던 인덱스도 삭제됨
- 테이블 자체가 사라지는 것이므로 데이터도 삭제되고, 사용하던 공간도 모두 반납한다. 제약 조건 등도 삭제된다.

#### DML(Data Manipulation Language) 데이터 조작어
Select : 데이터베이스에 들어 있는 데이터를 조회하거나 검색하기 위한 명령어 - Retrieve 라고도 함 <br/>
Insert, Update, Delete ...<br/>
데이터베이스의 테이블에 들어있는 데이터에 변형을 가하는 종류의 명령어들을 의미

#### DCL (Data Control Language) 데이터 제어어
Grant, Revoke ... <br/>
데이터베이스에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 명령어

#### TCL (Transaction Control Language) 트랜잭션 제어어
Commit, Rollback ... <br/>
논리적인 작업의 단위를 묶어서 DML에 의해 조작된 결과를 트랜잭션(작업단위)별로 제어하는 명령어

##### Commit
데이터에 대한 변경사항을 데이터베이스에 영구적으로 저장

##### Rollback
데이터에 대한 변경사항을 모두 폐기하고 변경 전 상태로 되돌리는 명령
- 테이블 내 입력한 데이터나 수정한 데이터, 삭제한 데이터에 대하여 Commit 이전에는 변경사항을 취소할 수 있는데, 이를 Rollback 하는 것
- 데이터 변경 사항이 취소되어 데이터 이전 상태로 복구되며, 관련된 향에 대한 Locking 이 풀리고 다른 사용자들이 데이터 변경을 할 수 있게 된다.
- 커밋 되지 않은 상태의 모든 트랜잭션을 롤백하는 것이다.
- 최초의 Begin Transation 시점까지 Rollback 이 수행됨

`Begin Transaction : 트랜잭션 실행
Commit Transaction / Rollback Transaction : 트랜잭션 종료`

##### Savepoint
롤백할 때 트랜잭션에 포함된 전체 작업을 롤백하는 것이 아닌, 현 시점의 Savepoint 까지 트랜잭션의 일부만 롤백해준다.

## 관계형 데이터베이스
#### 테이블 생성 주의사항
- 테이블명은 객체를 의미할 수 있는 적절한 이름, 단수형
- 테이블명은 다른 이름과 중복되지 않도록
- 한 테이블 내에는 컬럼명이 중복되게 지정할 수 없음
- 테이블 이름을 지정하고 각 칼럼들은 괄호로 묶어 지정
- 각 컬럼들은 콤마로 구분되고 테이블 생성문의 끝은 항상 세미콜롬으로 마친다.
- 컬럼에 대해선 다른 테이블까지 고려하여 데이터베이스 내에서 일관성있게 사용
- 컬럼 뒤에 데이터 유형은 꼭 지정되어야 한다
- 테이블명과 컬럼명은 반드시 문자로 시작해야하고 벤더별로 길이에 대한 한계가 있다.
- 벤더에서 사전에 정의한 예약어는 불가하다
- A-Z, a-z, 0-9, _, $, # 문자만 허용

#### 제약조건 (Constraint)
- Check 제약 조건은 데이터베이스에서 데이터의 무결성을 유지하기 위해 테이블의 특정 컬럼에 설정하는 제약
- 기본키는 반드시 테이블 당 하나의 제약만을 정의할 수 있다.
- 고유키로 지정된 모든 컬럼들은 null 값을 가질 수 있다.
- 외래키는 테이블간의 관계를 정의하기 위해 기본키를 다른 테이블의 외래키가 참조하도록 생성

## 참조 동작 (Referential Action)
#### Delete/Modify Action
1. Cascade : 참조하는 자식도 같이 삭제
2. Restrict : 자식 테이블에 PK값이 없는 경우만 삭제 허용, PK가 있으면 취소됨
3. Set Null : 마스터 삭제 시 자식 해당 필드 Null 처리
4. Set Default : 마스터 삭제 시 자식 해당 필드 Default 값으로 설정

#### Insert Action
1. Automatic : 마스터 테이블에 PK가 없는 경우 마스터 PK를 생성하고 자식 입력
2. Set Null : 마스터 테이블에 PK가 없는 경우 자식 외부키를 Null 로 처리
3. Set Default : 마스터 테이블에 PK가 없는 경우 자식 외부키를 Default 로 설정
4. Dependent : 마스터 테이블에 PK가 존재할 때 자식 입력 허용

## Null
#### Null 특성
- Null 은 아직 정의되지 않은 값으로 0이나 공백과는 다른다.
- 공백은 문자, 0은 숫자이다.
- 테이블을 생성할 때 Not Null 또는 PK로 정의되지 않은 모든 데이터 유형은 널값을 포함할 수 있다.
- 널 값을 포함하는 연산의 경우 결과값도 널 값이다.
`Null + 2 = Null, Null * 2 = Null, Null / 2 = Null ...`
- 결과값을 Null 이 아닌 다른 값을 얻고자 할 땐 Nvl, IsNull 함수를 사용한다.
- 널 값의 대상이 숫자인 경우 주로 0으로, 문자인 경우는 공백보단 x 같이 의미없는 문자로 바꾸는 경우가 많다.

## 함수
벤더에서 제공하는 함수인 내장 함수와 사용자가 정의할 수 있는 함수로 나눌 수 있다.
### 내장 함수
#### 단일행 함수
- 문자형 함수 : 문자를 입력하면 문자나 숫자를 반환
  - Lower, Upper, Substr, Length, Ltrim, Rtrim, Trim, Ascii
- 숫자형 함수 : 숫자를 입력하면 숫자를 반환
  - Abs, Mod, Round, Trunc, Sign, Chr, Ceil, Floor, Exp, Log, Ln, Power, Cos, Tan
- 날짜형 함수 : DATE 타입 값을 연산
  - Sysdate, Extract, To_number
- 변환형 함수 : 문자, 숫자, 날짜형의 값 데이터 타입을 반환
  - To_Number, To_Char, To_date
- Null 관련 함수 : Null을 처리하기 위한 함수
  - Nvl, NullIf, Coalesce

#### 단일행 함수의 특징
- Select, Where, Order by, Update Set 절에서 사용 가능
- 각 행에 대해 개별적으로 작용하여 데이터 값들을 조작하고 각각의 행에 대한 조작 결과를 반환한다.
- 여러 인자를 입력해도 하나의 결과만 리턴한다.
- 함수의 인자로 상수, 변수, 표현식이 사용 가능하고 하나의 인수 또는 여러 개의 인수를 가질 수도 있다.
- 특별한 경우가 아니라면 함수의 인자로 함수를 사용한느 함수의 중첩이 가능

#### 단일행 Null 관련 함수
1. Nvl(표현식1, 표현식2), IsNull(표현식1, 표현식2) : 표현식1의 결과값이 Null 이면 표현식2의 값을 출력 - 다만 표현식1과 표현식2의 결과 데이터 타입이 같아야 한다.
2. NullIf(표현식1, 표현식2) : 표현식1과 표현식2가 같으면 Null, 같지 않으면 표현식1을 리턴한다.
3. Coalesce(표현식1, 표현식2, ...) : 임의의 개수 표현식에서 Null 이 아닌 최초의 표현식을 나타낸다. 모든 표현식이 Null 이면 Null 을 리턴한다.

#### 다중행 함수
- 집계 함수
  - Count, Avg, Sum, Min, Max, Stddev, Variance
- 그룹 함수
  - Rollup, Cube, Grouping Sets
- 윈도우 함수
