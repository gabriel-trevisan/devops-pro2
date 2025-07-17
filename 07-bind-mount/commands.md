### Mount Bind Volume

`
docker container run -it --mount type=bind,source="$(pwd)/07-bind-mount",target=/app ubuntu /bin/bash
`

`
docker container run -d -p 8080:80 -v $(pwd)/07-bind-mount/html:/usr/share/nginx/html nginx
`