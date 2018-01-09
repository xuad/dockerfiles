# Default dockerfiles

## PHP-CLI-DEV Docker container

1. Check your current local ip address with: 

```bash
ifconfig
```

2. Set environment variables

```bash
echo 'export DOCKER_ENV_USER_ID="$(id -u)"' >> ${HOME}/.bashrc && \
echo 'export DOCKER_ENV_GROUP_ID="$(id -g)"' >> ${HOME}/.bashrc && \
echo 'export DOCKER_ENV_CERT_PATH="${HOME}/docker/data/certs"' >> ${HOME}/.bashrc && \
echo 'export DOCKER_PHP_XDEBUG_REMOTE_HOST="192.168.1.x"' >> ${HOME}/.bashrc
```

3. Build docker container

docker build php-cli-dev-7.2 \ 
--no-cache \
--build-arg PHP_USER_ID=${DOCKER_ENV_USER_ID} \ 
--build-arg PHP_GROUP_ID=${DOCKER_ENV_GROUP_ID} \ 
--build-arg REMOTE_HOST=${DOCKER_PHP_XDEBUG_REMOTE_HOST} \
-t xuad/php-cli-dev:7.2