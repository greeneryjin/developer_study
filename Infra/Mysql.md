
1. mysql - server 설치

       sudo apt-get install mysql-server

2. mysql version 확인

       mysql --version
   
3. mysql 구동 확인 (만약 window 내부에서 mysql 사용할 경우 중지하는 것을 추천)

       sudo systemctl status mysql

4. mysql 접속

        sudo mysql -u root -p

        root 계정은 자동 생성되기 때문에 입력하지 않아도 접속이 가능합니다.
        alter 명령어로 root 계정 비밀번호를 생성해줘야 합니다.

        ex) alter user 'root'@'localhost' identified with mysql_native_password by '비밀번호';
   
6. 데이터 베이스 확인 

        show databases;

     데이터베이스 생성

       CREATE DATABASE TEST;

8. 데이터 베이스 선택

       USE mysql;

9. 계정 확인

       SELECT User, Host, plugin FROM mysql.user;

   계정을 생성하는 것이 보안에 좋고, 사용자 역할마다 특정 권한을 부여하는 것이 좋습니다.

   5-1 계정 생성

       //내부ip(localhost) 접속 가능 계정
       CREATE USER '계정아이디'@'localhost' IDENTIFIED BY '비밀번호';
       ex) create user 'testId1'@'localhost' identified by 'testPw1';

       //외부ip 접속 가능 계정
       CREATE USER '계정아이디'@'%' IDENTIFIED BY '비밀번호';
       ex) create user 'testId1'@'%' identified by 'testPw1';

     'localhost' '%'
     + localhost 내부 ip만 접속할 수 있는 계정
     
     + %는 외부 ip에서도 접속할 수 있는 계정  


10. 권한 부여

       //모든 DB에 모든 권한 부여
       GRANT ALL PRIVILEGES ON *.* TO '계정아이디'@'호스트';
       ex) grant all privileges on *.* to 'testId1'@'loalhost';

       //특정 DB에 모든 권한 부여
       GRANT ALL PRIVILEGES ON 데이터베이스명.* TO '계정아이디'@'호스트';
       ex) grant all privileges on board.* to 'testId1'@'loalhost';

       //특정 DB에 특정 권한 부여
       GRANT SELECT, INSERT, UPDATE ON 데이터베이스명.* TO '계정아이디'@'호스트';
       ex) grant select, insert, update on board.* to 'testId1'@'loalhost';

11. 권한 적용

       FLUSH PRIVILEGES;

12. 권한 부여 확인SSH는 네트워크 상 다른 컴퓨터의 쉘을 사용할 수 있게 해 주는 프로그램 혹은 그 프로토콜

       SHOW GRANTS FOR '계정아이디'@'호스트';

   8-1 계정 삭제

       DROP USER '계정아이디'@'호스트';
       ex) drop user 'testId1'@'localhost';

       DELETE FROM USER WHERE USER = '계정아이디';
       ex) delete from user where user = 'testId1';

window에서 Ubuntu 사용할 때 통신하는 방법

putty, MobaXterm으로 SSH 통신을 사용해서 두 운영체제가 통신합니다.

----

SSH

: 네트워크 상 다른 컴퓨터의 쉘을 사용할 수 있게 해 주는 프로그램 혹은 프로토콜


dbeaver 연동 시 SSH 접속 

1. public key retrieval is not allowed 에러

       -> Diver properties에서 allowPublicKeyRetrieval를 true로 변경

2. Access denied for user 'root'@'localhost';

       -> update user set plugin='mysql_native_password' where user='root';
       -> plush privileges;
       -> select user, host, plugin from user;
       -> mysql 종료
       -> sudo systemctl restart mysql;


dbeaver 연동 시 Main 접속

       ubuntu 내부 mysql을 화면으로 볼 수 있도록 환경 제공


ssh key 충돌 해결 방법
       
       원인
       : 기존에 접속하던 시스템의 변경 문제(시스템 재설치 혹은 교체)로 저장된 원격 시스템의 고유값이 기존에 저장된 값과 다를 때 발생

       해결 방법
       : /root/.ssh/known_hosts  파일에 들어가서 해당 ip로 저장된 키 값이 저장된 라인을 삭제한 후 재접속을 시도

