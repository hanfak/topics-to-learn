# Docker

- what is it?
  - https://www.docker.com/what-docker
  - https://www.youtube.com/watch?v=-NzfOhSAZpA

## Containers

- Containers
  - https://www.docker.com/what-container
- Virtual machines

## Pushing image to repository

### Pushing image to docker repo

### Pushing image to some other repository

## other

- remove images
  - https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes


## Java api

## Deploying

- https://www.javacodegeeks.com/2018/02/docker-java-developers-deploy-docker.html

## images

- build image
  - `docker build -t <name of image> /{path to dockerfile}`

- run image
  - `docker run --name <alias you choose> -d -p 8080:8080 <name of image>`
    - -p 8080:8080 : This is setting the port to be used in you app and expoing in the docker image. This has to match the port in the dockerfile


- Passing arguments
  - https://forums.docker.com/t/is-it-possible-to-pass-arguments-in-dockerfile/14488/3
  - https://vsupalov.com/docker-env-vars/

- remove images
  - `docker system prune`
  - `docker rmi <image>`

## Links

- https://docs.docker.com/
- https://docker-curriculum.com/
- https://www.tutorialspoint.com/docker/index.htm
- https://github.com/LeCoupa/awesome-cheatsheets/blob/master/tools/docker.sh
