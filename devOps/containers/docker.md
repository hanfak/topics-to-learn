# Docker

- what is it?
  - https://www.docker.com/what-docker
  - https://www.youtube.com/watch?v=-NzfOhSAZpA
  - https://www.linkedin.com/pulse/beginner-friendly-intro-containers-vm-docker-preethi-kasireddy/

## Containers

- Containers
  - https://www.docker.com/what-container
- Virtual machines

- List all existing containers (running and not running).
  - `docker ps -a`
- List all running containers
  - `docker ps`
- Stop a specific container
  - `docker stop [container name]`
- Stop all running containers.
  - `docker stop $(docker ps -a -q)`
- Delete a specific container (only if stopped).
  - `docker rm [container name]`
- Force delete a specific container
  - `docker rm -f [container name]`
- Delete all containers (only if stopped).
  - `docker rm $(docker ps -a -q)`
- Display logs of a container.
  - `docker logs [container name]`

## Pushing image to repository

### Pushing image to docker repo

### Pushing image to some other repository

## other


## Java api


## Fabric8

- https://www.javacodegeeks.com/2019/02/docker-ise-java-application-maven-plugin.html

## Dockerfile

## Volumes

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
- Delete all existing images
  - `docker image rm $(docker images -a -q)`
- https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes

## Multistage docker image build

- https://dzone.com/articles/multi-stage-docker-image-build-for-java-apps


### Fat jars/ layering

- https://phauer.com/2019/no-fat-jar-in-docker-image/

## Performance

- https://www.thedevcoach.co.uk/docker-performance-tips-and-tricks/


## Disadvantages or not to use

- https://www.freecodecamp.org/news/7-cases-when-not-to-use-docker/
  - Do Not Use Docker if You Need to Boost Speed
  - Do Not Use Docker if You Prioritize Security
  - Do Not Use Docker if You Develop a Desktop GUI Application
  - Do Not Use Docker if You Want to Light Up Development and Debugging
  - Do Not Use Docker if You Need to Use Different Operating Systems or Kernels
  - Do Not Use Docker if You Have a Lot of Valuable Data to Store
  - Do Not Use Docker if You Are Looking for The Easiest Technology to Manage

## Links

- https://docs.docker.com/
- https://docker-curriculum.com/
- https://www.tutorialspoint.com/docker/index.htm
- https://github.com/LeCoupa/awesome-cheatsheets/blob/master/tools/docker.sh
- https://github.com/Albertoimpl/k8s-for-the-busy/blob/master/containerizing-java/README.adoc
- https://www.freecodecamp.org/news/a-beginners-guide-to-docker-how-to-create-your-first-docker-application-cc03de9b639f/
- https://www.freecodecamp.org/news/a-practical-guide-to-containers-dfa66d37ac30/?source=rss----336d898217ee---4
