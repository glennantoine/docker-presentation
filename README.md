Docker Presentation: docker-nginx
=================================

There are several ways to access this presentation:
1) Clone the repository, change to app1_presentation directory, run npm install, and grunt serve
2) Clone the repository, and run docker or docker-compose as per the directions below
3) Browse to [http://play-with-docker.com](http://play-with-docker.com) follow either step above

---
For example: 
* Browse to [http://play-with-docker.com](http://play-with-docker.com)
* Start an instance
* git clone [https://github.com/glennantoine/docker-presentation.git](https://github.com/glennantoine/docker-presentation.git) docker
* cd docker
* docker-compose up -d


### Running Multiple docker nginx images 
* Note: If using Play-with-Docker the available ports will be displayed near the top of the page 

--- 
#### Without docker-compose:
```bash
# build images
docker build --tag app1_presentation  --file Dockerfile.app1 .
docker build --tag app2_demosite  --file Dockerfile.app2 .

# run containers
docker run --detach --name app1_presentation --publish 8081:80 app1_presentation:latest
docker run --detach --name app2_demosite --publish 8082:80 app2_demosite:latest

# Use the below URLs in your browser
App1 (Presentation):
http://localhost:8081

App2 (Demo Site)
http://localhost:8082

or 
curl -s http://localhost:8081
curl -s http://localhost:8082

# stop containers
docker stop app1_presentation app2_demosite
docker rm app1_presentation app2_demosite

# remove image
docker rmi app1_presentation app2_demosite
```
--- 
#### With docker-compose:
```bash
# create and start containers
docker-compose up -d

# Use the below URLs in your browser
App1 (Presentation):
http://localhost:8081

App2 (Demo Site)
http://localhost:8082

or 
curl -s http://localhost:8081
curl -s http://localhost:8082

# stop containers
docker-compose stop
docker-compose rm -f
```
--- 
#### Cleaning Up your local docker environment:
```bash

# Generally safe cleanup commands
----------------------------------
# Delete Orphaned And Dangling Volumes
docker volume rm $(docker volume ls -qf dangling=true)

# Delete Dangling And Untagged Images
docker rmi -f $(docker images -q -f dangling=true)


# Cleanup commands, if you know what you're doing OR like living on the edge
----------------------------------------------------------------------------
# Kill All Running Containers
docker kill $(docker ps -q)

# Delete Exited Containers
docker rm $(docker ps -aqf status=exited)

# Delete All Images
docker rmi -f $(docker images -q)

# Delete All Containers
docker rm -f $(docker ps -aq)

# The 'official' Docker cleanup method (as of Docker 1.13)
# Delete Stopped Containers, And Volumes And Networks That Are Not Used By Containers
docker system prune -a

```

