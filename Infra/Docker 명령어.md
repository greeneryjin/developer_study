docker run

    //백그라운드 실행, 이름 지정, 포트 지정 
    docker run --name 이름 -d -p 8080:8080 컨테이너ID

네트워크 조회

    docker network ls

컨테이너 접속
  
    docker exec -it 컨테이너이름 bash

컨테이너 종료 없이 나가기

    Ctrl + P + Q

실행 중인 컨테이너 목록

     docker ps

중지된 컨테이너 + 실행 중인 컨테이너 목록

    docker ps -a
    

컨테이너 로그 확인

    docker logs (—tail)
    $docker logs <container_id>
    $docker logs -f <container_id>
    -f option : follow output, 백그라운드로 실행된 컨테이너의 로그 확인
    종료 : <CTRL>+<C>

docker image 목록

    docker images

docker 이미지 삭제

    docker rmi 

docker-compose로 컨테이너 종료

    docker-compose down

모든 컨테이너 중지/삭제/이미지 삭제

    docker stop $(docker ps -a -p)
    docker rm $(docker ps -a -p)
    docker rmi $(docker images -q)
    sudo rm -rf: 호스트 명령으로 삭제하고 하위 폴더까지 포함   


    //어드민이 아닐 경우
    sudo docker stop $(sudo docker ps -aq)
    sudo docker rm -f $(sudo docker ps -aq)

사용하지 않는 도커 볼륨 삭제

    docker volume prune

지금까지 작성한 명령어 

    history

docker 이미지 히스토리 

    docker history 이미지

docker registory에 push/pull

    docker tag tag이름 도커허브이름/컨테이너이름
    docker push 도커허브이름/컨테이너이름
    docker pull 도커허브이름/컨테이너이름

docker image registory에 push/pull

    docker tag 이미지명 도커허브이름/컨테이너이름
    docker push 도커허브이름/컨테이너이름

docker 게스트 os에서 확인하기(컨테이너 접속 X)

    docker exec <container_id> sh -c  ‘명령어’
    ex) docker exec 5d22d12b0c93 sh -c 'cat /usr/share/nginx/html/index.html' nginx index파일

호스트에서 컨테이너로 파일 복사

    docker cp hostmakefile.txt 컨테이너id: 카피 경로

호스트에서 편집한 문서 docker와 동기화하기

    mount: 호스트의 파일 시스템 경로를 컨테이너 내부에 연결하는 것을 의미로 호스트 머신의 디렉토리나 파일을 도커 컨테이너 내부에서 사용하거나 읽을 수 있게 됩니다.

    volume: 볼륨은 도커 컨테이너에서 데이터를 저장하고 공유하기 위한 디렉터리 또는 파일로 컨테이너가 삭제가 되더라도 데이터를 유지할 수 있게 만드는 것입니다. 
    
    
도커 컴포우즈

    sudo curl -SL https://github.com/docker/compose/releases/download/v2.24.5/docker-compose-     linux-x86_64 -o /usr/local/bin/docker-compose

도커 컴포우즈 버전

    docker -compose --version   


도커 컴포우즈 권한

    sudo chmod +x /usr/local/bin/docker-compose

도커 사용하지 않는 오브젝트 삭제

    이미지
    docker image prune

    컨테이너 
    docker container prune

    볼륨
    docker volumn prune

    네트워크
    docker network prune

