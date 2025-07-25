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