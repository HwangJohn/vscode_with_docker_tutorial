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

# simple dev env

---
**NOTE**
<p>
This is for ubuntu installation. 
If you use other os, you should follow the installation guide on github
</P>

---

* installation
  * python (the version you want) > pip > virtualenv > venv
```shell
# example
sudo apt-get install python3-pip
pip3 install virtualenv
virtualenv -p /usr/bin/python3 .venv
```
* usage
```shell
source .venv/bin/activate
pip list
pip install -r requirements.txt
pip list
```

## use pyenv+pyenv-virtualenv and conda
* default python lib management
  * pyenv: https://github.com/pyenv/pyenv 
  * pyenv-virtualenv: https://github.com/pyenv/pyenv-virtualenv
```shell
# installation of pyenv
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
cd ~/.pyenv && src/configure && make -C src # option
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile
exec "$SHELL"
sudo apt-get update; sudo apt-get install --no-install-recommends make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev

# installation of pyenv-virtualenv
git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bash_profile # option

## in ~/.zshenv, adding these two lines
status --is-interactive; and pyenv init - | source
status --is-interactive; and pyenv virtualenv-init - | source

## in ~/.zshrc, adding this line
eval "$(pyenv init -)"

exec "$SHELL"
```

* usage
```shell
# example of python 3.9.1
pyenv install --list
pyenv install 3.9.1
pyenv virtualenv 3.9.1 myvenv
pyenv virtualenvs

pyenv activate myvenv
pip list
pip install -r requirements.txt
pip list
pyenv deactivate

# example of miniconda3-latest
pyenv install miniconda3-latest
pyenv activate miniconda3-latest
conda env list
conda create -n myminiconda3 python=3.9.1
conda env list
conda activate myminiconda3
pip list
pip install numpy
pip list 
conda list
... so on
```

## docker env
![docker engine](https://docs.docker.com/engine/images/engine-components-flow.png)
### Docker
* overview: https://docs.docker.com/get-started/overview/
* Get started
* Develop with Docker: https://docs.docker.com/develop/
* https://docs.docker.com/compose/
### Docker-compose
* overview: https://docs.docker.com/compose/
### Docker-registry
* overview: https://docs.docker.com/registry/

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
docker login
docker commit <container_name>
docker tag <image_name>:<version> <username>/<imagename>:<version>
docker push <username>/<imagename>:<version>

# pull
docker pull <username>/<imagename>:<version>
```
### Save image file
```shell
docker save verse_gapminder > verse_gapminder.tar
```
