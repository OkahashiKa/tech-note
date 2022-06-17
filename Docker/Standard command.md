# Docker standard command

## create docker image

``` Bash
docker build -t [image_name]:[tag] [target_dir_path]
```

## show docekr image list

``` Bash
docker images
```

## create and run docker container

``` Bash
docker run -d --name [container_name] -p [outer_port]:[inner_port] [image]:[tag]
```

## show docker container list

``` Bash
docker ps
```
