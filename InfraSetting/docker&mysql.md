
    docker run --name mysqlserver -e MYSQL_ROOT_PASSWORD=root -d -p 3306:3306 mysql:812:25

    docker exec -it mysqlserver mysql -uroot -p
