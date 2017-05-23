Save & Load Docker Images
=========================

Scenario: 
To save a docker image from a docker repository and save it as a tar file locally

```bash
# build our Docker Image (don’t forget the . period at the and of the command)
docker build --tag app1_presentation  --file Dockerfile.app1 .

# save the image as a tarball
docker save app1_presentation:latest > archive/app1_presentation.tar

# zip the image
gzip archive/app1_presentation.tar

# copy the tarball to the new machine.
scp app1_presentation.tar.gz <foreign machine>

# unzip The tarball
gunzip app1_presentation.tar.gz

# load the docker image
docker load < app1_presentation.tar

# find the Image ID
docker images

# tag the image
docker tag app1_presentation:tag

```

Publishing your Custom Docker Image on Docker Hub
=================================================

To do so, you will need the ID and the TAG of the “presentation_app1” image.
Run again the "docker images" command and note the ID and the TAG of the Docker image

```bash
docker images

docker tag a69f3f5e1a31 accountname/app1_presentation:latest

# Next, use the "docker login" command to log into the Docker Hub from the command line
docker login --username=yourhubusername 

# Now you can push your image to the newly created repository
docker push accountname/app1_presentation

```


