
계정 생성

    CREATE USER 계정명 IDENTIFIED BY 비밀번호;

권한 부여

    GRANT CONNECT, resource, dba TO 계정명;

사용자로 변경

    CONNECT 계정/비밀번호; 
