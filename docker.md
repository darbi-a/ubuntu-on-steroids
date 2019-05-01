## Docker Cheatsheet
#### List Images / Containers
```sh
# list all images
docker images

# list all images (including intermediate)
docker images -a

# list running containers
docker container ls

# list all containers
docker container ls -a

# inspect a container
docker inspect <container_id>
```

#### Build Image
```sh
# build a docker image from the local files in <local_app_dir>
docker build --tag=<username>/<repository>:<version> <local_app_dir>

# tag an already built image
docker tag <existing_tag> <username>/<repository>:<version>
```

#### Run Image
**`docker run`** *will attempt to fetch the image from public registry if it's not found in local machine.*
```sh
# map the <exposed_port> in Dockerfile to <machine_port> that the app will be served
docker run -p <exposed_port>:<machine_port> <tag>

# run image in detached mode
docker run -d -p <exposed_port>:<machine_port> <tag>

# mount the volume 'my-vol' into '/app/' in the container
docker run -d \
    --mount source=my-vol,target=/app \
    -p <exposed_port>:<machine_port> \
    <tag>

# same as above, but mounts the volume as read-only
docker run -d \
    --mount source=my-vol,target=/app,readonly \
    -p <exposed_port>:<machine_port> \
    <tag>

# run image in interactive mode, open up a shell, and remove container on exit
docker run --rm -ti <tag> /bin/bash
```

#### Stop Container
```sh
# gracefully stop container
docker container stop <hash>

# force shutdown
docker container kill <hash>
```

#### Remove Images / Containers
```sh
# remove container from machine
docker container rm <hash>

# remove image from machine
docker image rm <image_id>
```

#### Volumes
```sh
# create a volume named 'my-vol'
docker volume create my-vol

# list volumes
docker volume ls

# inspect the 'my-vol' volume
docker volume inspect my-vol

# remove the 'my-vol' volume
docker volume rm my-vol

# remove all unused volumes
docker volume prune
```

#### Public Registry
```sh
# login to public registry
docker login

# logout from public registry
docker logout

# upload image to public registry
docker push <username>/<repository>:<tag>
```

#### Docker Compose
```sh
# build images
docker-compose build

# build missing images & run containers
docker-compose up

# re-build images if Dockerfile or image files have changed
docker-compose up --build

# start in detached mode
docker-compose up -d

# stop containers
docker-compose down

# list containers
docker-compose ps

# access all container logs
docker-compose logs

# push images to registry
docker-compose push

# pull images into a new machine
docker-compose pull
```