### List of basic Docker commands

1. List running docker container
```
docker ps
```

2. List all running docker container
```
docker ps -a
```

3. List docker images
```
docker image ls
```

4. Remove docker image
```
docker rmi <IMAGE_ID>
```

5. Remove docker container
```
docker rm <CONTAINER_ID>
```

6. Running a docker contianer in detached mode
```
docker run -d --name <CONTAINER_NAME> -p <EXTERNAL_PORT>:<INTERNAL_PORT> <REPOSITORY>:<TAG>
Ex: docker run -d --name tomcat-container -p 8080:8080 docker.io/amd64/tomcat:8.5-jre8
```
