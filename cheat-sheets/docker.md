house keeping
```bash
docker kill $(docker ps -q) # unlike stop this fucks containers pronto
docker builder prune
docker image prune # docker usually have dangling images after build
docker system prune # full clean except volumes
```

single file mount
```bash
docker run --mount type=bind,source=/local/file,target=/remote/file,readonly alpine
```

view
```bash
docker ps --size # check running container size
```

copy from container to local
```bash
docker cp container:/path/to/file/in/container /path/to/local
```

build image from running container
```bash
docker commit container image:latest
docker run --rm -it image
docker push /path/to/registry
```

docker run
```bash
# run multiple commands within docker
docker run --rm busybox bash -c "whoami && pwd"

# runtime options, good for benchmarking
docker run --rm --cpu 0.8 --memory 256m busybox

# overwrite entrypoint, sadly can't do anything for CMD
docker run --entrypoint bash grafana/k6
```

docker build, save and load somewhere else
>can be used to load images in cri for kubernetes when loading images
```bash
# build image
docker build -t image:latest .
# save image to local
docker save image:latest -o image.tar
# load image in another docker runtime
docker load -i image.tar
```

[ghcr.io](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry)

# more cheat-sheets:
- https://dockercheatsheet.com/