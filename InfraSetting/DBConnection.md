 1. Mysql 

    + SSH
  
       (1) HOST/IP: Host ip 주소
    
       (2) Port: 연결할 포트 번호
    
       (3) 우분투 접속 아이디
    
       (4) 우분투 접속 비번

    + Main

       (1) server Host: localhost ip 주소

       (2) Port: 3306

       (3) username: mysql 계정 아이디

       (4) password: mysql 계정 비밀번호

   
    + Driver propeties

       - allowPublicKeyRetrieval: true

---

 2. Oracle

    + SSH

      (1) HOST/IP: Host ip 주소

      (2) Port: 연결할 포트 번호

      (3) 우분투 접속 아이디

      (4) 우분투 접속 비번

    + Main

       (1) server Host: localhost

       (2) Port: 1521

       (3) username: mysql 계정 아이디

       (4) password: mysql 계정 비밀번호

       (5) 교육용은 xe로 Database에 넣기

---

 3. eclipse      

```JAVA

        Mysql
        Class.forName("com.mysql.cj.jdbc.Driver");
        Connection con = DriverManager.getConnection("jdbc:mysql://HOST_IP:연결_port/fisa?useSSL=false&allowPublicKeyRetrieval=true", "mysqlID", "mysqlPASSWORD");

	//접속 확인
	System.out.println(con);

	Statement - sql 문장 실행 객체 생성 

	ResultSet - select query 전용 객체(insert, update, delete는 사용하지 않음)

	rs.next() - 데이터 반환으로 boolean 타입

	//객체 메모리 반환 
	rs.close();
	stmt.close();
	con.close();

	Oracle
        Class.forName("oracle.jdbc.driver.OracleDriver");
     	Connection con = DriverManager.getConnection("jdbc:oracle:thin:@HOST_IP:연결_port:xe", "oracleID", "oraclePASSWORD");
			
```  
