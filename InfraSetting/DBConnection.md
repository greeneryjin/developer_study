 1. Mysql 

    + SSH
  
       (1) HOST/IP: Host ip 작성
    
       (2) Port: 연결할 포트 번호
    
       (3) 우분투 접속 아이디
    
       (4) 우분투 접속 비번

    + Main

       (1) server Host: localhost

       (2) Port: 3306

       (3) username: mysql 계정 아이디

       (4) password: mysql 계정 비밀번호

   
    + Driver propeties

       - allowPublicKeyRetrieval: true

---

 2. Oracle

    + SSH

      (1) HOST/IP: Host ip 작성

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

  			Class.forName("com.mysql.cj.jdbc.Driver");
        Connection con = DriverManager.getConnection("jdbc:mysql://HOSTIP:연결port/fisa?useSSL=false&allowPublicKeyRetrieval=true", "mysqlID", "mysqlPASSWORD");		

        Class.forName("oracle.jdbc.driver.OracleDriver");
  			Connection con = DriverManager.getConnection("jdbc:oracle:thin:@192.168.0.55:1521:xe", "oracleID", "oraclePASSWORD");
			
        
