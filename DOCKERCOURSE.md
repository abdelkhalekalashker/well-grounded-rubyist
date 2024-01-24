# Docker 
## Images
  - n image is a lightweight, standalone, and executable package that includes all the necessary code, runtime, libraries, and system tools needed to run an application.
  - it needs to be built to fetch it from docker hub or any other registery.
  - to build an image from registry:-
      ``` docker build -t <image_name>:<tag> <path_to_Dockerfile> ```
  - to list all running images
      ``` docker images ```
  - to remove specific image:-
     ``` docker rmi <image_name> or $ docker rmi <image_id> ```
  - to remove all unused images :-
       ``` docker image prune ```
  - to pull an image from docker hub
     ``` docker pull fedora:latest ``` --> this pull latest version from fedora official. 
    $ ``` docker pull fedora:2.4 ```  --> this pull version 2.4 from fedora.
    fedora is called repo and 2.4 is called tag
  - ``` docker image ls -q ``` --> list all ids of images including stopped images
  - $ ``` docker image rm $(docker image ls -q) ``` --> this command remove all given ids of image returned from ` $(docker image ls -q) ` variable
## containers
  - A container is a running instance of a Docker image.
  - containers are built on image.
  - if there are no images then there are no containers.
  - Containers provide a consistent and isolated environment, ensuring that the application runs the same way across different environments.
  - to pull image and create containers from that image in a single command --> ``` docker container run -it -p 87210:3000 --name my_rails rails:7.0.4 ```
      --name to set name for your container from the rails image
      -p to set port in the host to interact with container host port --> host port is 87210 and you can control it and set it with any port number you want but the container port is 3000 but you can not control it.
      -it is interactive terminal to interact with container you created from terminal
      -d is to run the container in background and to hide logs
  - to specify the main app in container
      $ ``` docker container run -it <image> <app> ```
        app --> is the main app in container which if i existed from the container stops
  - after stopping the container data that created on that container will be lost
  - to save this data we have to create volumes to save the container's data.

    
## Networking in Docker
  containers are isolated in docker by default so containers can not interact with each other or interact with files from another containers.
  networking is comming to solve this issue

  there are three network types for docker single machine

1. **Bridge:**
   - This is the default network for each container you created.
   - This network allows the containers in it to access each other or the internet.
   - This network uses the driver "bridge".
   - Containers of this network can connect to other networks or disconnect from the bridge network even after container creation.

2. **Host:**
   - This network is used to use your hostname as the container's hostname.
   - This network can interact with other containers and the internet.
   - You cannot create networks from this network.
   - This network uses the driver "host".
   - To connect the container to this network, you should set it up during the creation of the container.

3. **None:**
   - If the container's network is set to none, the container cannot access other containers or the internet.
   - The driver of this network is null.
   - Containers of this network can connect to other networks or disconnect from the bridge network even after container creation.


#### creation of networks
  ``` docker network create <network_name> ```
#### create container with network 
  ``` docker container run --name <container name> --network <network name> ```
#### connect to network
  ``` docker network connect <network name> <container name> ```
#### disconnect from network
  ``` docker network disconnect <network name> <container name> ```
#### internal option
  - internal option is used to make the container to access this internal network containers but not access other networks or internet
  - ``` docker network create --internal <network name> ```
