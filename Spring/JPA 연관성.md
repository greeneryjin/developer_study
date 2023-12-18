1. 매핑을 하지 않은 상태로 두 엔티티 값 저장

```JAVA
@NoArgsConstructor
@AllArgsConstructor
@Getter
@Setter
@ToString
@RequiredArgsConstructor //id를 제외한 생성자 생성
@Entity
public class Member1 {

	@Id
	@GeneratedValue
	@Column(name = "member_id")
	private long memberId;
	
	//컬럼 사이즈 20byte
	@Column(length = 20)
	@NonNull
	private String name;
	
	@Column(name="team_id")
	@NonNull
	private long teamId;
}

@NoArgsConstructor
@AllArgsConstructor
@Getter
@Setter
@RequiredArgsConstructor //id를 제외한 생성자 생성
@Entity
public class Team1 {

	@Id
	@GeneratedValue
	@Column(name = "team_id")
	private long teamId;
	
	//컬럼 사이즈 20byte
	@Column(name = "team_name", length = 20)
	@NonNull
	private String teamName;
}
```

   
```JAVA
public class Step01RunTest {

	@Test
	public void step01Test() {
		
		EntityManager em = null;
		EntityTransaction tx = null;
		
		try {
			em = DBUtil.getEntityManager();	
			tx = em.getTransaction();
			tx.begin();
			
			Team1 t1 = new Team1();
			t1.setTeamName("토트넘");
			em.persist(t1);
			em.persist(new Team1("첼시"));
			
			em.persist(new Member1("손흥민", 1));
			em.persist(new Member1("토레스", 2));
			em.persist(new Member1("박지성", 3));
			
			tx.commit();
			
		} catch(Exception e) {
			tx.rollback();
			e.printStackTrace();
		} finally {
			if(em != null) {
				em.close();
				em = null;
			}
		}
	}
```
결과: Team1, Member1의 PK값이 공유되는 문제가 발생하고 commit()할 때마다 쿼리가 발생해서 성능이 좋지 않음

---

2. 1번의 문제를 해결

```java
@NoArgsConstructor
@AllArgsConstructor
@Getter
@Setter
@ToString
@RequiredArgsConstructor //id를 제외한 생성자 생성

@SequenceGenerator(name = "member_seq", sequenceName = "member_seq_id", allocationSize = 50, initialValue = 1)
@Entity
public class Member2 {

	@Id
	@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "member_seq")
	@Column(name = "member_id")
	private long memberId;
	
	//컬럼 사이즈 20byte
	@Column(length = 20)
	@NonNull
	private String name;
	
	@Column(name="team_id")
	@NonNull
	private long teamId;
}

@NoArgsConstructor
@AllArgsConstructor
@Getter
@Setter
@RequiredArgsConstructor //id를 제외한 생성자 생성
@SequenceGenerator(name = "team_seq", sequenceName = "team_seq_id", initialValue = 1, allocationSize = 50)
@Entity
public class Team2 {

	@Id
	@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "team_seq")
	@Column(name = "team_id")
	private long teamId;
	
	//컬럼 사이즈 20byte
	@Column(name = "team_name", length = 20)
	@NonNull
	private String teamName;
}
```

결과: allocationSize로 ID값을 50까지 저장한 후, 쿼리를 보내는 방식으로 성능을 향상, GenerationType.SEQUENCE 사용해서 자동 생성하도록 개발
      하지만 존재하지 않는 팀이 멤버에 저장되는 문제가 발생 

----

3. 2의 문제 해결

```JAVA
@NoArgsConstructor
@AllArgsConstructor
@Getter
@Setter
@ToString
@RequiredArgsConstructor //id를 제외한 생성자 생성

@SequenceGenerator(name = "member3_seq", sequenceName = "member3_seq_id", allocationSize = 50, initialValue = 1)
@Entity
public class Member3 {

	@Id
	@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "member3_seq")
	@Column(name = "member_id")
	private long memberId;
	
	//컬럼 사이즈 20byte
	@NonNull
	@Column(length = 20)
	private String name;
	
	@NonNull
	@OneToOne
	@JoinColumn(name="team_id")
	private Team3 teamId;
}

@NoArgsConstructor
@AllArgsConstructor
@Getter
@Setter
@RequiredArgsConstructor //id를 제외한 생성자 생성
@SequenceGenerator(name = "team3_seq", sequenceName = "team3_seq_id", initialValue = 1, allocationSize = 50)
@Entity
public class Team3 {

	@Id
	@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "team3_seq")
	@Column(name = "team_id")
	private long teamId;
	
	//컬럼 사이즈 20byte
	@Column(name = "team_name", length = 20)
	@NonNull
	private String teamName;
	
}

public class Step03RunTest {
	
	/*
	 * Team1 데이터 저장 -> Member1 데이터 저장
	 * member는 team 반드시 등록하고 team은 반드시 존재해야함 
	 * */

	@Test
	public void step03Test() {
		
		/*
		 * 존재하지 않은 팀을 저장하는 현상이 발생하지 않음 
		 * */
		
		EntityManager em = null;
		EntityTransaction tx = null;
		
		try {
			em = DBUtil.getEntityManager();	
			tx = em.getTransaction();
			tx.begin();
			
			Team3 t1 = new Team3();
			t1.setTeamName("토트넘");
			em.persist(t1);
			
			Team3 t2 = new Team3();
			t2.setTeamName("첼시");
			em.persist(t2);
			
			em.persist(new Member3("손흥민", t1));
			em.persist(new Member3("모우라", t1));
			em.persist(new Member3("토레스", t2));
			
			tx.commit();
			
		} catch(Exception e) {
			tx.rollback();
			e.printStackTrace();
		} finally {
			if(em != null) {
				em.close();
				em = null;
			}
		}
	}
}
```

결과: 2의 문제가 해결됨. 회원 관점에서 팀의 1대1 방향으로 해결됨

----

4. 팀의 관점에서 회원 다 대 일

```JAVA
@NoArgsConstructor
@AllArgsConstructor
@Getter
@Setter
//@ToString
@Builder
@RequiredArgsConstructor //id를 제외한 생성자 생성

@SequenceGenerator(name = "member4_seq", sequenceName = "member4_seq_id", allocationSize = 50, initialValue = 1)
@Entity
public class Member4 {

	@Override
	public String toString() {
		StringBuilder builder = new StringBuilder();
		builder.append("Member4 [memberId=");
		builder.append(memberId);
		builder.append(", name=");
		builder.append(name);
		builder.append("]");
		return builder.toString();
	}

	@Id
	@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "member4_seq")
	@Column(name = "member_id")
	private long memberId;
	
	//컬럼 사이즈 20byte
	@NonNull
	@Column(length = 20, nullable = false)
	private String name;
	
	//(fetch = FetchType.LAZY): JOIN을 걸지 않고 지연시키는 의미
	@ManyToOne(fetch = FetchType.LAZY)
	@JoinColumn(name="team_id", nullable = false)
	/*
	 * Team4 타입의 컬럼 등록, 테이블에서는 NUMBER(19)로 저장
	 * */
	private Team4 teamId;
}

@NoArgsConstructor
@AllArgsConstructor
@Getter
@Setter
@Builder
//@ToString
@RequiredArgsConstructor //id를 제외한 생성자 생성
@SequenceGenerator(name = "team4_seq", sequenceName = "team4_seq_id", initialValue = 1, allocationSize = 50)
@Entity
public class Team4 {

  // 무한 순환 방지 
	@Override
	public String toString() {
		StringBuilder builder = new StringBuilder();
		builder.append("Team4 [teamId=");
		builder.append(teamId);
		builder.append(", teamName=");
		builder.append(teamName);
		builder.append("]");
		return builder.toString();
	}

	@Id
	@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "team4_seq")
	@Column(name = "team_id")
	private long teamId; //ORACLE은 NUMBER(19)로 저장
	
	//컬럼 사이즈 20byte
	@Column(name = "team_name", length = 20, nullable = false)//nullable은 column의 불허
	@NonNull //엔티티의 null값 불허, 생성자 초기화
	private String teamName;
	
	@OneToMany(mappedBy = "teamId")
	private List<Member4> memberList = new ArrayList<>();
	
	public int getMembersCount() {
		return memberList.size();
	}


@Test
	public void step04Test() {
		EntityManager em = null;
		EntityTransaction tx = null;
		
		try {
			em = DBUtil.getEntityManager();	
			tx = em.getTransaction();
			tx.begin();
			
			// 두 명의 선수 생성 및 하나의 팀 생성
			Team4 t1 = Team4.builder().teamName("fisa1팀").build();
			Member4 m1 = Member4.builder().name("김연경").teamId(t1).build();
			Member4 m2 = Member4.builder().name("이동욱").teamId(t1).build();
		
			em.persist(t1);
			em.persist(m1);
			em.persist(m2);
			
			tx.commit();
			em.clear();
		
			Team4 newTeam = em.find(Team4.class, 1L);
//			System.out.println(newTeam.getTeamId());  // 0
//			System.out.println(newTeam.getTeamName());
//			System.out.println(newTeam.getMembersCount());	
			
			System.out.println("*********************");
			System.out.println(newTeam.getMemberList().get(0));	
			//ToString()으로 Team4 -> Member4 -> Team4 -> Member4 호출로 무한 순환 참조가 발생합니다. 

			//(fetch = FetchType.LAZY)걸면 team에 대한 join 쿼리를 하지 않음 
			Member4 m1 = em.find(Member4.class, 1L);
			System.out.println(m1);
			System.out.println(m1.getMemberId());
			System.out.println(m1.getName());
			
			//(fetch = FetchType.LAZY)으로 인해서 join 쿼리가 나감 
			System.out.println(m1.getTeamId().getTeamName());
		} catch(Exception e) {
			e.printStackTrace();
			tx.rollback();
		} finally {
			if(em != null) {
				em.close();
				em = null;
			}
		}
	}
}
```
