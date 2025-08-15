### List network

`docker network ls`

### Create network bridge

`docker network create aula_docker`

`docker network inspect aula_docker`

`docker container run --name nginx -d nginx`

`docker network connect aula_docker nginx`

`docker container inspect nginx`

### Example bridge

`docker network create --subnet=10.0.0.0/16 --gateway=10.0.0.1 outra_rede_docker`

`docker container run -it --network outra_rede_docker ubuntu /bin/bash`

`docker container run -it --name conversao-temperatura --network outra_rede_docker fabricioveronez/conversao-temperatura:v1`

`curl http://conversao-temperatura:8080`