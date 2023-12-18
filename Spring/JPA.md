

### JPA(Java Persistence API)

특징 

+ JAVA ORM 기술 표준 명세로 JAVA에서 제공하는 API
+ JAVA 어플리케이션에서 관계형 데이터 베이스를 사용하는 방식을 정의한 인터페이스 
+ ORM은 자바 클래스와 DB 테이블을 매핑
+ JPA를 사용하기 위해서는 Hibernate, EclipseLink, DataNucleus와 같은 ORM 프레임 워크를 사용해야함 

Repository 클래스에 JPA를 주입해서 Hibernate로 사용하고 Hibernate가 JDBC API 통해 DB와 소통합니다. 

#### ORM

: 객체와 DB 테이블을 매핑시켜주는 것을 의미합니다. ORM을 사용하면 SQL Query가 아닌 java 코드로 데이터를 조작할 수 있습니다. 


JPA 동작 과정

: JAVA -> JPA -> JDBC -> DB

  JPA 내부에 Hibernate를 사용해서 JPA를 구현합니다.

<br>

#### Hibernate

: JPA 구현체의 한 종류로 JPA는 DB와 자바 객체를 매핑하기 위한 API를 제공하고 JPA 구현체를 구현한 것입니다.
  Hibernate 내부에 JDBC API가 동작하고 있기 때문에 DB와 소통할 수 있습니다. HQL이라는 Hibernate Query Language을 사용해서 SQL의 문장을 객체로 반환해줍니다. 

#### 영속성

: 데이터를 생성한 프로그램이 종료되어도 사라지지 않는 데이터의 특성입니다. 

영속성 계층
  
  + 프레젠테이션 계층: UI 
  + 애플리케이션 계층: 서비스 
  + 비즈니스 논리 계층: 도메인 
  + 데이터 접근 계층: 영속 계층

JPA에서 객체를 관리하는 방법

: JPA 실행되면 엔티티 매니저 팩토리에서 엔티티 매니저을 통해 객체를 관리합니다. 엔티티 매니저가 활성화된 상태에서 트랜잭션안에서 DB에서 데이터를 가져오면 영속 상태가 됩니다. 영속 상태로 된 객체는 JPA에서 계속 관리합니다.  

<br>

영속 종류

+ 비영속: 엔티티 객체가 만들어지지 않은 상태로 영속성 컨텍스트에 존재하지 않음

+ 영속: 엔티티 객체가 만들어진 상태로 영속성 컨텍스트에 존재하고 관리하는 객체

+ 준영속: 엔티티 객체가 만들어진 상태로 영속성 컨텍스트에 존재하고 관리했다가 분리된 상태입니다. 영속성 컨텍스트가 관리하지 않음 

+ 삭제: 엔티티를 영속성 컨텍스트와 DB에서 삭제

<br>
엔티티 CRUD

````JAVA 
  			//존재하는 테이블에 데이터 저장
			em = DBUtil.getEntityManager();
			//트랜잭션
			EntityTransaction tx = em.getTransaction();

			
			//데이터 검색
//			DB 검색 전 영속성컨텍스트 확인 후 없으면 DB SELECT 조회, 있으면 영속성 객체 반환
//			Dept one = em.find(Dept.class, 10);
//			System.out.println(one.getLoc());	
//			Emp two = em.find(Emp.class, 7369);
//			System.out.println(two.getEname());
		
			//데이터 저장 
//			tx.begin();
//			persist호출 시 영속성 컨텍스트에 저장 
//			em.persist(new Dept(1, "cloud engineer", "상암"));
//			tx.commit();		
//			commit 시 영속성 컨텍스트에서 자동으로 flush()호출되고 영속성 컨텍스트의 내용을 DB와 동기화하고 commit실행 
			
			//데이터 수정  
//			tx.begin();
//			Dept one = em.find(Dept.class, 1);
//			one.setLoc("한국");
//			tx.commit();
//			수정 시 영속성에 있던 객체를 스냅샷을 사용해서 상태를 저장하는데 자동으로 flush()를 통해 변경된 데이터와 변경전 데이터를 비교해서 수정하고 commit을 합니다. 
//			System.out.println(one.getLoc());
			
			//데이터 삭제 
			tx.begin();
			Dept one = em.find(Dept.class, 1);
			if(one != null) {
				em.remove(one);				
			}
//			삭제 시 자동으로 flush호출 후 변경 내용을 DB와 동기한 후, commit을 진행합니다. 
			tx.commit();
````

#### JPA 메소드

1. flush()

: 영속성 컨텍스트의 내용을 DB에 반영합니다. 저장, 수정, 삭제에서 사용됩니다. 

2. defach()

: 특정 엔티티를 준영속 상태로 만듭니다. 

3. clear()

: 영속성 컨텍스트를 초기화합니다.

4. close()

: 영속성 컨텍스트를 종료합니다. 

5. merge()

: 준영속 상태의 엔티티로 만들어줍니다.
