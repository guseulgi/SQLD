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
현실 세계를 일정한 형식에 맞추어 표현하는 <strong>추상화</strong>의 의미 <br/>
복잡한 현실을 제한된 언어나 표기법을 통하여 이해하기 쉽게 하는 <strong>단순화</strong>의 의미를 가지고 있다. <br/>
애매모호함을 배제하고 누구나 이해가 가능하도록 정확하게 현상을 기술하는 <strong>명확화</strong>의 의미를 가진다. <br/>
<br/>

#### 모델링의 관점 3
1. 데이터 관점
   - 업무가 어떤 데이터와 관련이 있는지
   - 데이터 간의 관계는 무엇인지
2. 프로세스 관점
   - 실제 업무가 무엇인지
   - 무엇을 해야하는지
3. 데이터와 프로세스의 상관관점
   - 업무가 처리하는 일의 방법에 따라 데이터는 어떻게 영향을 받는지


#### 데이터 모델링의 유의점
- 중복 -> 중복이 없어야 함
    - 데이터 모델은 같은 데이터를 사용하는 사람, 시간, 장소를 파악하는데 도움을 줌으로써 데이터베이스가 여러 장소에 같은 정보를 저장하는 잘못을 하지 않도록 한다.
- 비유연성 -> 유연해야 함
    - <strong>데이터 정의를 데이터의 사용 프로세스와 분리함</strong>으로써 데이터 모델링은 데이터 혹은 프로세스의 작은 변화가 애플리케이션과 데이터베이스에 중대한 변화를 일으킬 수 있는 가능성을 줄인다.
- 비일관성 -> 일관성 있어야 함
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

#### 프로젝트 생명주기에서 데이터 모델링
- 계획/분석 단계에선 개념적 데이터 모델링
- 분석 단계에선 논리적 데이터 모델링
- 설계 단계에서 물리적 데이터 모델링이 수행
- 현실적으로 개념적 데이터 모델링이 생략된, 개념/논리적 데이터 모델링이 분석 단계에서 수행된다.

#### 데이터 모델링에서 데이터 독립성의 이해
- 데이터 독립성은
  - 유지보수
  - 비용절감
  - 데이터 복잡성 감소
  - 데이터 중복 감소
  - 사용자 요구사항 대응... 을 위해서 필요하다.
- 데이터 독립성의 효과로는
  - 각 View 의 독립성 유지와 계층별 View 에 영향 없이 변경 가능
  - 단계별 스키마에 따라 DDL과 DML 의 다름을 제공한다.

#### 데이터 모델링의 3가지 개념
- 엔터티 : 업무가 관여하는 것 Things
- 속성 : 어떤 것이 가지는 성격
- 관계 : 업무가 관여하는 것 간의 관계

#### 데이터 모델링의 이해 관계자
- 프로젝트 개발자
- 현업 업무 전문가
- 전문 모델러
- DBA

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
사람, 장소, 물건, 사건, 개념 등 명사에 해당
#### 인스턴스
엔터티는 틀이며, 이를 이용한 실제 데이터를 인스턴스라고 한다.

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
1. 속성명 기재
2. 식별자 기재(PK, FK ...)
3. 필수값 표시 (NN)

- 엔터티에 대한 자세하고 구체적인 정보를 나타낸다.
- 하나의 엔터티는 두 개 이상의 속성을 가진다.
- 하나의 인스턴스에선 각각의 속성은 하나의 속성값을 가져야 한다. (두 개 이상의 속성값은 X)
- 속성도 집합이다.
- 각 속성은 가질 수 있는 값의 범위가 있는데, 이를 <strong>도메인</strong>이라 한다. 앤터티 내에서 속성에 대한 데이터 타입과 크기, 제약 사항을 지정하는 것이다. 도메인 외의 값을 가질 순 없다.
<br/>


#### 엔터티, 인스턴스, 속성, 속성값 사이의 관계
- 한개의 엔터티는 두 개 이상의 인스턴스의 집합이어야 한다.
- 한 개의 엔터티는 두 개 이상의 속성을 갖는다.
- 한 개의 속성은 한 개의 속성값을 가진다. (제 1정규화, 원자성과 관련 됨)


#### 속성의 특성에 따른 분류
- 기본 속성
  - 원래 가지고 있어야 하는 속성
- 설계 속성
  - 설계하면서 도출해낸 속성
  - 업무상 필요한 데이터 이외에 데이터 모델링을 위해 업무를 규칙화하기 위한 속성을 만들거나 변형하여 정의하는 속성
- 파생 속성
  - 기본 속성에서 계산된 속성
  - 데이터를 조회할 때 빠른 성능을 할 수 있도록 하기 위해
 #### 속성의 명칭 부여
 - 해당 업무에서 사용하는 이름 부여
 - 서술식 속셩명은 지양 -> 키워드
 - 약어 사용 지양
 - 전체 데이터모델에서 유일성 확보


#### 관계
상호 연관성이 있는 상태

- 존재에 의한 관계와 행위에 의한 관계로 구분된다.
  - 존재에 의한 관계 : 존재의 형태에 의해 관계가 형성 ex. 부서-사원
  - 행위에 의한 관계 : ex. 고객-주문
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

- 관계 읽기
  - 기준 엔터티를 한 개 또는 각(Each)으로 읽는다
  - 대상 엔터티의 관계참여도, 즉 개수를 읽는다
  - 관계선택사양과 관계명을 읽는다

- 관계 명명 규칙 : 애매한 동사 지양, 현재형 사용
- 관계명의  표기
  - 엔터티가 관계에 참여하는 형태 지칭
  - 하나의 관계는 소속한다/소속된다 라는 두 가지 관계명을 가지고 있다.
  - 관계명에 의해 두 가지 관점으로 표현될 수 있다.

<br/>

### 식별자
- 여러 개 집합체를 담고 있는 하나의 통에서 각각을 구분할 수 있는 논리적인 이름
- 엔터티의 인스턴스를 개별적으로 식별하기 위해 사용되는 관계 또는 속성들의 조합

#### 식별자의 종류
- 엔터티 내에서 대표성을 가지는가에 따라
  - 주식별자 : 엔터티 내에 각 어커런스를 구분할 수 있는 구분자이며, 타 엔터티와 참조관계를 연결할 수 있는 식별자 ex. 사원번호, 고객번호
  - 보조식별자 : 엔터티 내에서 각 어커런스를 구분할 수 있는 구분자이나 대표성을 가지지 못해 참조관계 연결을 못함 ex. 휴대폰 번호, 주민번호
  - 어커런스 : 정의된 레코드의 구조에 따라 데이터베이스에 구체적이고 실제적인 정보를 저장하고 있는 데이터
- 엔터티 내에서 스스로 생성되었는지 여부에 따라
  - 내부 식별자 : 엔터티 내부에서 스스로 만들어지는 식별자 ex. 고객번호
  - 외부 식별자 : 타 엔터티와의 관계를 통해 타 엔터티로부터 받아오는 식별자 ex. 주문엔터티의 고객번호
- 단일 속성으로 식별이 되는가에 따라 
  - 단일식별자 : 하나의 속성으로 구성된 식별자
  - 복합식별자 : 둘 이상의 속성으로 구성된 식별자 ex. 주문번호헤더+주문번호상세
- 원래 업무적으로 의미가 있던 식별자 속성을 대체하여 일련번호와 같이 새롭게 만든 식별자를 구분하기 위해
  - 본질식별자 : 업무에 의해 만들어진 식별자
  - 인조식별자 : 업무적으로 만들어지지 않지만 원조식별자가 복잡한 구성을 가지고 있기에 인위적으로 만들어지는 식별자/ 본질식변자 대체 ex. 주문번호->고객번호+주문번호+순번

#### 주식별자를 지정할 때 고려해야 하는 사항
1. 주식별자에 의해 엔터티 내의 모든 인스턴스들이 유일하게 구분되어야 한다. = 유일성
2. 주식별자를 구성하는 속성의 수는 유일성을 만족하는 최소의 수가 되어야 한다. = 최소성
3. 지정된 식별자의 값은 자주 변하지 않는 것이어야 한다. = 불변성
4. 주식별자가 지정이 되면 반드시 값이 들어와야 한다. = 존재성
5. 복합으로 주식별자를 구성할 경우 너무 많은 속성을 포함하지 않도록 한다. -> 인조 식별자 활용
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

#### 식별자 관계와 비식별자 관계의 결정
1. 외부 식별자는 다른 엔터티와의 관계를 통해 자식쪽에 엔터티에 생성되는 속성을 외부 식별자라 하며 데이터베이스 생성시 외래키 역할을 한다.
2. 자식 엔터티에서 부모 엔터티로부터 받은 외부 식별자를 자신의 주식별자로 이용할 것인지 -> 식별자 관계
3. 부모와 연결이 되는 속성으로서만 이용할 것인지 -> 비식별자 관계
4. 엔터티 사이 관계 유형은 업무 특성, 자식 엔터티의 주식별자 구성/SQL전략에 의해 결정


## 데이터 모델과 성능
#### 성능 데이터 모델링?
데이터베이스 성능 향상을 목적으로, 설계 단계의 데이터 모델링 때부터 성능과 관련된 사항이 데이터 모델링에 반영될 수 있도록 하는 것
* 일반적으로 성능이란, 데이터의 조회 성능을 의미한다.

#### 성능 데이터 모델링의 수행 시점
- 사전에 할수록 비용절감
- SQL 문장 튜닝
- 하드 용량 증설
- 데이터 증가가 빠를수록 성능저하

#### 성능 데이터 모델링 수행 절차
1. 데이터 모델링을 할 때 정규화를 정확하게 수행
2. 데이터베이스 용량산정을 수행
3. 데이터베이스에 발생되는 트랜잭션의 유형을 파악
4. 용량과 트랜잭션의 유형에 따라 반정규화를 수행
5. 이력모델의 조정, PK/FK 조정, 슈퍼타입/서브타입 조정 등을 수행
 - 슈퍼타입과 서브타입의 관계는 배타적 관계와 포괄적 관계가 있는데, 배타적 관계는 고객이 개인이거나 법인고객인 경우를 의미하며 포괄적인 관계는 고객이 개인고객일 수도 있고 법인고객일 수도 있는 것  
6. 성능 관점에서 데이터 모델을 검증

* 정규화가 항상 조회 성능을 저하시킨다는 것은 잘못된 생각이며 기본적으로 중복된 데이터를 제거함으로써 조회성능을 향상시킬 수 있다.
