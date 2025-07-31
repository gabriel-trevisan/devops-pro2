### Mount Bind Volume

`
docker container run -it --mount type=bind,source="$(pwd)/07-bind-mount",target=/app ubuntu /bin/bash
`

`
docker container run -d -p 8080:80 -v $(pwd)/07-bind-mount/html:/usr/share/nginx/html nginx
`

### Docker Volume

`
docker volume create aula_vol
`

`
docker container run -it --mount type=volume,source=aula_vol,target=/app ubuntu /bin/bash
`

`
docker container run -it -v a64605893643dc020e982d70c671b699f866b1c0e45b3127365bb4aed97f0025:/app exemplo-volume /bin/bash
`

### Backup Docker Volume

`
docker container run --volumes-from e31363ff98b7 --rm -v $(pwd)/docker/07-docker-volume:/backup ubuntu:22.04 tar cvf /backup/backup_vol.tar /app
`
#### Restore new volume
`
docker volume create novo_volume
`

`
docker container run -v $(pwd)/docker/07-docker-volume:/backup -v novo_volume:/app ubuntu:22.04 tar xvf /backup/backup_vol.tar
`

`
docker inspect novo_volume
`

`
[
    {
        "CreatedAt": "2025-07-29T07:51:50-03:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/novo_volume/_data",
        "Name": "novo_volume",
        "Options": null,
        "Scope": "local"
    }
]
`

`
https://docs.docker.com/engine/storage/volumes/#back-up-restore-or-migrate-data-volumes
`

### Examples

`
docker container run -d -e POSTGRES_PASSWORD=minhasenha -p 5432:5432 --mount type=bind,source="$(pwd)/docker/07-docker-volume/db_vol",target=/var/lib/postgresql/data postgres
`

`
create table pessoa (
	id INT generated always as identity,
	nome varchar not null
);
`

`
docker container run -d -e POSTGRES_PASSWORD=minhasenha -p 5432:5432 --mount type=volume,source=container_postgre_vol,target=/var/lib/postgresql/data postgres
`

### Tmpfs

`
docker container run -it --mount type=tmpfs,target=/app ubuntu /bin/bash
`

`
docker container run -d -p 3306:3306 --tmpfs /var/lib/mysql -e MYSQL_ROOT_PASSWORD=rootpwd mysql
`

### Example Project

`
git clone https://github.com/gabriel-trevisan/kube-news
`

`
docker container run -d -p 5432:5432 -e POSTGRES_PASSWORD=Pg123 -e POSTGRES_USER=kubenews \
-e POSTGRES_DB=kubenews -v kubenews_vol:/var/lib/postgresql/data postgres:14.10
`

`
DB_DATABASE=kubenews DB_USERNAME=kubenews DB_PASSWORD=Pg123  node server.js
`