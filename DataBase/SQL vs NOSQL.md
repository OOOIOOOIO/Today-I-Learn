# SQL과 NOSQL의 차이와 선택
> 웹, 앱을 개발할 때 어떤 데이터베이스를 선택할지 고민하게 된다.
> 보통 Java, Spring에서 개발할 때는 MySQL과 같은 관계형 DB, 파이썬, Node.js을 사용한다면 MongoDB를 주로 사용했을 것이다.
> 하지만 그냥 단순히 프레임워크에 따라 결정하는 것이 아닌 진행할 프로젝트에 맞춰 데이터베이스를 선택해야할 것이다.


## SQL(관계형 DB)
- SQL을 사용하면 RDBMS에 데이터를 조회, 저장, 수정 그리고 삭제 를 할 수 있다.

### 특징
- 데이터는 정해진 데이터 스키마에 따라 테이블에 저장된다.
- 데이터는 관계를 통해 여러 테이블에 분산된다.
> 데이터는 테이블에 레코드로 저장된다. 각 테이블마다 명확하게 정의된 구조가 있다. 해당 구조는 필드의 이름과 데이터 유형으로 정의된다.
> 따라서 스키마를 준수하지 않은 레코드는 테이블에 추가할 수 없다. 즉, 스키마를 수정하지 않는 이상 정해진 구조에 맞는 레코드만 추가가 가능한것이
> RDMBS의 특징 중 하나이다.









