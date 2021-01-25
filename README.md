# vscode_with_docker_tutorial

## Install VScode
https://code.visualstudio.com/

### install extentions for local host
* Python
* Jupyter
* Docker
* Remote - Containers

## make new project & clone it
https://github.com/

## use virtualenv
* default python lib management
```shell
# tutorial with virtualenv
# TODO
```

## make dev env
* make env files
    * command + shift + p
    * select remote-containers.createDevContainerFile
    * select from DockerCompose
* open & copy CMDs to Dockerfile
```shell
# change FROM ~~~ with below
FROM pytorch/pytorch:1.7.1-cuda11.0-cudnn8-runtime
...
# add RUN
RUN pip3 install torch==1.7.1 torchvision==0.8.2 jupyter tensorboard  
```
* open & add `ports` to docker-compose.yml
```shell
...
services:
  app:
    image: <image_name>
    ...
    ports:
      - "6007:6006"
      - "8889:8888"
    ...
```
* open & add `forwardPorts` to devcontainer.json
```shell
...
	"forwardPorts": [6006,8888],
...
```

* (option)jupyter notebook execution
  * nohup jupyter notebook --port=8888 --no-browser --ip=0.0.0.0 --NotebookApp.token='' --NotebookApp.password='' --allow-root &

## Docker image usage
### Dockerhub
* login on https://hub.docker.com/
* push your image to dockerhub
```shell
# push
$ docker login
$ docker commit <container_name>
$ docker tag <image_name>:<version> <username>/<imagename>:<version>
docker push <username>/<imagename>:<version>

# pull
$ docker pull <username>/<imagename>:<version>
```
### Save image file
```shell
$ docker save verse_gapminder > verse_gapminder.tar
```
