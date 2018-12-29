# Docker Hints and Techniques

## Contents

- [How to configure an mssql-server container](#how-to-configure-an-mssql-server-container)

---

## How to configure an mssql-server container

1. Pull the container image from Docker Hub

```
docker pull microsoft/mssql-server-linux
```

2. To run container image with Docker, use following command:

```
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=aerothai" -p 1401:1433 -v D:/Docker/sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux
```

> or
```
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=aerothai' -p 14331:1433 -d --name=mssql-server-01 microsoft/mssql-server-linux:latest
```

3. To view your Docker containers, use the docker ps command.

```
docker ps -a
```

4. To access the container, use following command with the container ID:

```
docker exec -it [container_id] "bash"
```

5. To start the container with existing configurations

```
docker start [container_id]
```