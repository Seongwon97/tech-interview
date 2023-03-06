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
