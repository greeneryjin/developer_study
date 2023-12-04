
1. 최신 패키지 리스트 업데이트

       sudo apt-get update


2. docker 다운로드  관련 패키지 설치

       sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common

       apt-transport-https: https를 통해 데이터나 패키지에 접근 가능
       ca-certificates: SSL 기반 웹 애플리케이션이 SSL 연결의 진위여부를 판달하게 해줌
       curl: 링크로 데이터를 다운받을 수 있도록 해주는 도구
       software-properties-common: 우분투에서 PPA를 사용하기 위한 패키지

4. docker repository 접근을 위한 GPG key 설정

       curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

       신뢰할 수 있는 APT Repository 키로 저장
       gpg: 배포 파일의 인증을 확인하는데 사용되는 패키지
       sudo apt-key add - 패키지 키 추가

5. Docker 공식 apt 저장소를 추가
   
       sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

6. 최신 패키지 리스트 업데이트

       sudo apt-get update

7. docker 설치

       sudo apt install docker-ce

   7-1 docker 실행 상태 확인

        sudo systemctl status docker
      
8. 일반 사용자 계정으로 docker 명령어 사용

       sudo usermod -aG docker ${USER}
       id -nG
   
   
