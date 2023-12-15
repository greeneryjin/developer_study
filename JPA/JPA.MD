
### JPA(Java Persistence API)

특징 

+ JAVA ORM 기술 표준 명세로 JAVA에서 제공하는 API
+ JAVA 어플리케이션에서 관계형 데이터 베이스를 사용하는 방식을 정의한 인터페이스 
+ ORM은 자바 클래스와 DB 테이블을 매핑
+ JPA를 사용하기 위해서는 Hibernate, EclipseLink, DataNucleus와 같은 ORM 프레임 워크를 사용해야함 

Repository 클래스에 JPA를 주입해서 Hibernate로 사용하고 Hibernate가 JDBC API 통해 DB와 소통합니다. 

#### ORM

객체와 DB 테이블을 매핑시켜주는 것을 의미합니다. ORM을 사용하면 SQL Query가 아닌 java 코드로 데이터를 조작할 수 있습니다. 


JPA 동작 과정

: JAVA -> JPA -> JDBC -> DB

  JPA 내부에 Hibernate를 사용해서 JPA를 구현합니다.


#### Hibernate

: JPA 구현체의 한 종류로 JPA는 DB와 자바 객체를 매핑하기 위한 API를 제공하고 JPA 구현체를 구현한 것입니다.
  Hibernate 내부에 JDBC API가 동작하고 있기 때문에 DB와 소통할 수 있습니다. 

