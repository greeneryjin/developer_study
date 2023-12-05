

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

docker image 목록

    docker images

docker 이미지 삭제

    docker rmi 

docker-compose로 컨테이너 종료

    docker-compose down

모든 컨테이너 중지/삭제/이미지 삭제

    docker stop $(docker ps -a -p)
    docker rm $(docker ps -ap)
    docker rmi $(docker images -q)
    sudo rm -rf: 호스트 명령으로 삭제하고 하위 폴더까지 포함    

사용하지 않는 도커 볼륨 삭제

    docker volume prune


    
