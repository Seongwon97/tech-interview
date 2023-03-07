# Database
<details>
<summary>SQL이란 무엇일까요?</summary>

<br>

SQL(Structured Query Language)란 관계형 데이터베이스 관리 시스템의 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어이며 관계형 데이터베이스 관리 시스템에서 자료의 검색, 관리, 데이터베이스 스키마 생성과 수정, 데이터베이스 객체 접근 조정 관리를 위해 고안되었다.

</details>


<details>
<summary>트랜잭션이란?</summary>

<br>

- 트렌잭션이란 데이터베이스의 상태를 변화시키기 위해 수행하는 작업의 단위 또는 한꺼번에 모두 수행되어야 할 일련의 연산들을 뜻한다.
- 트랜잭션은 데이터의 정합성을 보장하기 위해 고안되었으며 데이터베이스 시스템에서 병행제어 및 회복 작업을 할 시 처리되는 작업의 논리적인 단위가 된다.

[트랜잭션이란?](https://seongwon.dev/Database/20221001-트랜잭션이란/)

</details>


<details>
<summary>트랜잭션의 특징인 ACID에 대해 설명해주세요 </summary>

<br>

- Atimicity(원자성)
  - 트랜잭션의 연산은 DB에 모두 반영되거나 아예 반영되지 않아야 한다,
- Consistency(일관성)
  - 트랜잭션이 성공적으로 작업을 수행한 후에도 데이터베이스는 일관성있는 상태를 유지해야한다.
  - e.g. 돈을 송금하기 전/후의 돈의 총 합은 같아야 한다.
- Isolation(독립성)
  - 둘 이상의 트랜잭션이 실행되고 있을 경우 어떤 트랜잭션이라도 다른 트랜잭션의 연산에 끼어들 수 없다.
- Durability(지속성, 영속성)
  - 성공적으로 수행을 마친 트랜잭션의 결과는 시스템이 고장나도 영구적으로 반영되어야 한다.

[트랜잭션이란?](https://seongwon.dev/Database/20221001-트랜잭션이란/#트랜젝션의-특징-acid)

</details>


<details>
<summary>다수의 트랜잭션이 하나의 자원을 접근할 때 발생할 수 있는 문제들은 무엇이 있을까요?</summary>

<br>

- Dirty Read
  - Uncommitted 결과를 다른 트랜젝션에서 확인하는 현상을 말한다.
- Non-Repeatable Read
  - 하나의 트랜잭션에서 같은 데이터를 두 번 조회하였을 때 같은 결과를 가져와야 한다는 REPEATABLE READ정합성에 어긋나게 다른 데이터를 읽어오는 문제이다.
- Phantom Read
  - 한 트랜잭션 안에서 일정 범위의 레코드를 두 번 이상 읽었을 때, 첫번째 쿼리에서 없던 데이터가 두번째 쿼리에서 나타나는 현상이다.

[트랜잭션이란?](https://seongwon.dev/Database/20221001-트랜잭션이란/#다수의-트랜젝션이-하나의-자원을-경쟁할-때의-문제들)

[트랜잭션의 격리수준(Isolation level)이란?](https://seongwon.dev/Database/20221022-트랜잭션-격리수준이란/)

</details>


<details>
<summary>트랜잭션의 격리 레벨에 대해 설명해주세요</summary>

<br>

트랜잭션 격리수준이란 여러 트랜잭션이 동시에 처리될 떄 특정 트랜잭션이 다른 트랜잭션에서 변경하거나 조회하는 데이터를 볼 수 있게 허용할지 말지를 결정하는 것입니다. 격리 수준을 어떻게 설정하느에 따라 데이터 부정합 문제와 성능에 영향을 줄 수 있다.

격리 수준은 `READ UNCOMMITTED`(Level0), `READ COMMITTED`(Level1), `REPEATABLE READ`(Level2), `SERIALIZABLE`(Level3)이 존재한다.

### READ UNCOMMITTED

- 트랜잭션의 변경 내용을 commit 여부의 상관없이 다른 트랜잭션이 조회할 수 있다.
- 격리가 되지 않은 상태라 **Dirty Read, Non-Repeatable Read, Phantom Read가 모두 발생할 수 있다.**

### READ COMMITTED

- 트랜잭션에서 데이터를 변경하였더라도 Commit이 완료된 데이터만 다른 트랜잭션에서 조회할 수 있다.
- MySQL에서는 언두로그를 이용해 데이터의 변경이 발생하면 변경 이전 데이터를 언두(Undo)로그에 복사하고 조회 요청이 오면 언두로그의 데이터를 반환하는 구조로 동작하여 다른 트랜잭션들에게는 변경 이전의 데이터를 보여주는 구조로 동작하여 Dirty Read를 해결하였다.
- **Non-Repeatable Read, Phantom Read가 발생할 수 있다.**

### REPEATABLE READ

- 하나의 트랜잭션에서 같은 데이터를 두 번 조회하였을 때 같은 결과를 가져오는 REAPETABLE READ를 보장한다.
- MySQL InnoDB에서는 MVCC 방식으로 언두 영역에 백업해둔 데이터를 이용해 하나의 트랜잭션에서 발생하는 같은 조회 쿼리에 대해서는 동일한 결과를 보장하고 있다. → 각각의 트랜잭션은 언두로그에서 자신이 부여받은 트랜잭션 ID보다 더 작은 ID의 데이터만 볼 수 있다.
- **Phantom Read가 발생할 수 있다.** (MySQL InnoDB는 넥스트 키 락 덕분에 REPEATABLE READ에서도 발생하지 않는다.)

### Serialize

- 한 트랜잭션에서 읽기, 쓰기 등의 모든 데이터들은 다른 트랜잭션이 접근할 수 없게 한다.
- 모든 동작이 직렬화하게 작동하여 완벽한 읽기 일관성 모드를 제공한다.
- 데이터에 접근하는 것 만으로도 다른 트랜잭션은 해당 데이터에 접근할 수 없기에 REPEATABLE READ에서 발생하는 Phantom Read는 발생하지 않는다.

[트랜잭션의 격리수준(Isolation level)이란?](https://seongwon.dev/Database/20221022-트랜잭션-격리수준이란/)

</details>


<details>
<summary>DDL, DML, DCL 은 무엇일까요?</summary>

<br>

**DDL(Data Definition Language)**

- 데이터베이스 스키마를 정의하거나 조작하기 위한 언어
- 대상은 SCHEMA, DOMAIN, TABLE, VIEW, INDEX 등이 있다.
- 명령어를 입력하는 순간 작업이 즉시 완료(Auto Commit)된다.
- CREATE, ALTER, DROP. RENAME, COMMENT, TRUNCATE

**DML(Data Manipulation Language)**

- 데이터베이스 내부 레코드를 관리하기 위한 언어로 데이터 추가, 변경, 삭제 등의 작업을 수행한다.
- AUTO COMMIT이 되지 않아, 작업 완료시 트랜잭션 내에서 COMMIT 명령어를 통해 반영을 해야하며 ROLLBACK이 가능하다.
- SELECT, INSERT, UPDATE, DELETE 등

**DCL(Data Control Language)**

- 데이터베이스에 접근하거나 객체에 권한을 주는 등의 역할을 하는 언어이다.
- GRANT, REVOKE, COMMIT, ROLLBACK

</details>


<details>
<summary>Key에 대해 설명해주세요</summary>

<br>

**후보키 (candidate key)**

- 릴레이션을 구성하는 속성들 중 튜플을 유일하게 실별할 수 있는 속성들의 부분집합을 의미한다.
- 모든 릴레이션은 반드시 하나 이상의 후보키를 가져야 한다.
- 릴레이션에 있는 모든 튜플에 대해 유일성과 최소성을 만족시켜야 한다.
  - 유일성: Key로 하나의 Tuple을 유일하게 식별할 수 있다.
  - 최소성: 꼭 필요한 속성으로만 구성된다.

**기본키 (Primary Key)**

- 한 릴레이션에서 특정 튜플을 유일하게 구별할 수 있는 속성으로 후보키중에서 선택된 Main key이다.
- 무결성 특징을 갖는다.
  - Null값을 가질 수 없다.
  - 중복된 값이 저장될 수 없다.

  > 데이터의 정확성과 일관성을 유지하고, 데이터의 결손과 부정합이 없음을 보증하는 것
>

> 기본키는 수정이 가능할까?
>
> - 기본키를 수정하기 위해서는 삭제를 한 후 추가를 하는 식으로 동작한다.

**대체키 (Alternate Key)**

- 후보키가 둘 이상일 때 기본키를 제외한 나머지 후보키를 의미한다.
- 보조키라고 부른다

**슈퍼키 (Super key)**

- 한개의 릴레이션 내에 있는 속성들의 집합으로 구성된 키이다.
  - ex) <학생> 릴레이션에 '학번', '주민번호', '학번'+'주민번호', '학번'+'주민번호'+'성명' 등으로 슈퍼키를 구성할 수 있습니다.
- 릴레이션을 구성하는 모든 튜플에 대해 유일성은 만족하지만 최소성은 만족시키지 못한다.
  - 집합에 속한 모든 속성을 엮지 않아도 유일성이 있는 슈퍼키를 만들 수 있는 상황이 존재하여 최소성을 만족하지 못한다 한다.

**외래키 (Foreign Key)**

- 참조되는 릴레이션의 기본키와 대응되어 릴레이션 간에 참조 관계를 표현하는데 중요한 도구로 사용된다.
- **참조 무결성의 조건으로 외래키로 참조 테이블의 기본키에 없는 값은 입력할 수 없다.**

</details>


<details>
<summary>외래키 값은 NULL이 들어올 수 있나요?</summary>

<br>

Yes. 외래키는 Null이 허용된다.

하지만 참조 무결성을 위해 null을 하지 않는 것이 좋다.

</details>


<details>
<summary>View란 무엇일까요?</summary>

<br>

데이터베이스에서 뷰는 사용자에게 접근이 허용된 자료만을 보여주기 위해 한개 이상의 테이블을 조인하여 만든 **가상 테이블**이다. 뷰는 저장 장치에 물리적으로 존재하지 않지만 사용자에게는 실제로 존재하는 것처럼 간주된다.

사용은 사용자에게 특정 정보만을 제공하고 싶은 경우나 데이터 보정 작업, 처리과정 시험 등 임시적인 작업을 위한 용도로 활용된다.

> View에 DML 문을 사용하면 기본 테이블의 데이터도 변경된다.
>

**장점**

- 논리적인 데이터의 독립성을 제공한다. (물리적인 공간이 필요 없다)
- 복잡한 쿼리를 단순화하고 데이터 조회가 용이하다.
- 접근 제어를 통한 보안이 제공된다.

**단점**

- 뷰에 인덱스를 구성할 수 없다.
- 뷰의 정의를 변경할 수 없다.
- 뷰로 구성된 내용에 대한 삽입, 삭제, 갱신, 연산에 제약이 따른다.

**뷰에 데이터의 CUD 연산의 제약이 걸리는 경우**

- 뷰 정의에 포함되지 않은 컬럼 중에서 기본 테이블의 컬럼이 Not Null 제약조건이 지정되어있는 경우 Insert 불가
- `Data * 2` 와 같이 산술 표현식으로 정의된 가상 컬럼이 뷰에 정의되면 Insert, Update 불가
- Distinct를 포함하는 경우에 DML 명령 사용 불가
- 그룹 함수나 Group By 절을 포함한 경우 DML 명령 사용 불가

[SQL 단순 VIEW 수정 & 삭제](https://pathas.tistory.com/73)

[[DB기초] 뷰(View)란 무엇인가? + 간단한 예제](https://coding-factory.tistory.com/224)

</details>


