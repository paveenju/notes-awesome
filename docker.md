# Docker Hints and Techniques

## Contents

- [How to configure an MS SQL Server container](#how-to-configure-an-ms-sql-server-container)
- [How to configure an MySQL Server container](#how-to-configure-an-mysql-server-container)

---

## How to configure an MS SQL Server container

1. Pull the container image from Docker Hub

    ```console
    docker pull microsoft/mssql-server-linux
    ```

2. Run container image with Docker with following command:

    ```console
    docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=aerothai" -p 1401:1433 -v D:/Docker/sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux
    ```

    OR

    ```console
    docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=aerothai' -p 14331:1433 -d --name=mssql-server-01 microsoft/mssql-server-linux:latest
    ```

3. To view your Docker containers, use the `docker ps` command.

    ```console
    $docker ps -a
    ```

4. To access the container, use the `docker exec` specifying its container ID:

    ```console
    $docker exec -it [container_id] "bash"
    ```

5. To start the container with existing configurations

    ```console
    $docker start [container_id]
    ```

## How to configure an MySQL Server container

1. Download the MySQL Community Server image, run this command:

    ```console
    $docker pull mysql/mysql-server:5.7.20
    ```

2. Start a new Docker container for the MySQL Server with this command:

    ```console
    $docker run --name=mysql_db -e MYSQL_ROOT_PASSWORD="password" -p 33061:3306 -d mysql/mysql-server:5.7.20
    ```

3. Connecting to MySQL Server from within the Container

    ```console
    $docker exec -it mysql_db mysql -uroot -p
    ```

4. Container shell access

    ```console
    $docker exec -it mysql_db bash
    ```

5. Start, Restart and Stop the MySQL Server container

    ```console
    $docker start mysql_db
    $docker restart mysql_db
    $docker stop mysql_db
    ```

6. Remove the container

    ```console
    $docker rm mysql1
    ```

7. Enable the connection from remote host with following steps:
    - Connect to MySQL
    ```cmd
    $mysql -u root -p
    ```

    - Create a user
    ```console
    mysql>CREATE USER 'user'@'%' IDENTIFIED BY 'password';
    ```

    - Grant permissions
    ```console
    mysql> GRANT ALL PRIVILEGES ON *.* TO 'user'@'%' WITH GRANT OPTION;
    ```

    - Flush priviledges
    ```console
    mysql>FLUSH PRIVILEGES;
    ```