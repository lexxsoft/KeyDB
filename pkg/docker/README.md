This Dockerfile will clone the KeyDB repo, build, and generate a Docker image you can use

To build, use experimental mode to enable use of build args. Tag the build and specify branch name. The command below will generate your docker image:

```bash
# DOCKER_CLI_EXPERIMENTAL=enabled docker build --build-arg BRANCH=<keydbBranch> -t <yourImageName>

# run from repo root to ensure context is correct
DOCKER_CLI_EXPERIMENTAL=enabled docker build -f pkg/docker/Dockerfile -t keydb:6.3.4 .
```

## Notes

```bash
git pull https://github.com/Snapchat/KeyDB --recursive
git fetch --all
git checkout tags/v6.3.4

git pull https://github.com/redis/redis --recursive
git fetch --all
git checkout tags/8.2.2
```

patches from https://github.com/redis/redis/commits/8.2.2

Test with

```bash
docker run -it --rm --name some-keydb keydb:6.3.4
docker run -it --rm --link some-keydb keydb:6.3.4 keydb-cli -h some-keydb -p 6379
docker run -it --rm --link some-keydb keydb:6.3.4 keydb-benchmark -h some-keydb -p 6379
```
