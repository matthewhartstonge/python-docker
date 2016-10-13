# Python+docker

Python+Docker includes python and the docker-engine to ease CI/CD. By 
integrating the docker-engine into the package one needs to only map the docker 
socket into the container in order to build docker images and push to a remote
registry.

Please note: This container does not set out to be secure, it sets out to be
usable as a tool in a self-contained private CI/CD setting.

## Supported tags
- `latest`, `python2-docker1.12.2` [(python2-docker1.12.2/Dockerfile)](https://github.com/MatthewHartstonge/python-docker/blob/python2-docker1.12.2/Dockerfile)
- `python2-docker1.12.1` [(python2-docker1.12.1/Dockerfile)](https://github.com/MatthewHartstonge/python-docker/blob/python2-docker1.12.1/Dockerfile)
- `python2-docker1.12.0` [(python2-docker1.12.0/Dockerfile)](https://github.com/MatthewHartstonge/python-docker/blob/python2-docker1.12.0/Dockerfile)
- `python2-docker1.11.2` [(python2-docker1.11.2/Dockerfile)](https://github.com/MatthewHartstonge/python-docker/blob/python2-docker1.11.2/Dockerfile)
- `python2-docker1.11.1` [(python2-docker1.11.1/Dockerfile)](https://github.com/MatthewHartstonge/python-docker/blob/python2-docker1.11.1/Dockerfile)
- `python2-docker1.11.0` [(python2-docker1.11.0/Dockerfile)](https://github.com/MatthewHartstonge/python-docker/blob/python2-docker1.11.0/Dockerfile)
- `python2-docker1.10.3` [(python2-docker1.10.3/Dockerfile)](https://github.com/MatthewHartstonge/python-docker/blob/python2-docker1.10.3/Dockerfile)
- `python2-docker1.10.2` [(python2-docker1.10.2/Dockerfile)](https://github.com/MatthewHartstonge/python-docker/blob/python2-docker1.10.2/Dockerfile)
- `python2-docker1.10.1` [(python2-docker1.10.1/Dockerfile)](https://github.com/MatthewHartstonge/python-docker/blob/python2-docker1.10.1/Dockerfile)
- `python2-docker1.10.0` [(python2-docker1.10.0/Dockerfile)](https://github.com/MatthewHartstonge/python-docker/blob/python2-docker1.10.0/Dockerfile)
- `python2-docker1.9.1`  [(python2-docker1.9.1/Dockerfile)](https://github.com/MatthewHartstonge/python-docker/blob/python2-docker1.9.1/Dockerfile)
- `python2-docker1.9.0`  [(python2-docker1.9.0/Dockerfile)](https://github.com/MatthewHartstonge/python-docker/blob/python2-docker1.9.0/Dockerfile)

## Quickstart
Since this image is based on dockerhub's [python](https://hub.docker.com/_/python/),
all actions follow through on this container, with the exception of the 
addition of the docker-engine.

The underlying OS is debian:jessie. 

To get access to your host, simply map the docker socket into the container on
startup.

```sh
docker run -it \
    -v "/var/run/docker.sock:/var/run/docker.sock"
    matthewhartstonge/python-docker
    docker ps
```

## Development
Each python/docker version is split out into a separate branch. Please feel free 
to add Pull Requests to add the different versions you use as a token of thanks
and also to give back to the community. 

### Pip build tools
For those that are using anything that requires C based python/pip modules you 
will need to install the required build tools. 

#### Dockerfile
```
FROM matthewhartstonge/python-docker:latest

RUN apt-get update \
    && apt-get install \
        python-dev \
    && pip install -r requirements.txt \
    && apt-get remove --purge \
        python-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
```

#### CI Script
```sh
script:
  - apt-get update && apt-get install python-dev
  - ...
```

## Deployment
Simply pull your required version from dockerhub

```sh
docker pull matthewhartstonge/python-docker
```

## Testing
To use CI testing with this image, install run your favourite python tester.
For example, using Tox in your .drone, .jenkinsfile, .whatever add:

```sh
script:
  - apt-get update && apt-get install python-dev
  - pip install -r requirements.txt
  - pip install tox
  - tox
```
