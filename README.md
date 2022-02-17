# docker-process
Testing Drone Simulation in docker

# Installation 
## Docker

You can find these installation instructions [here](https://docs.px4.io/master/en/test_and_ci/docker.html).

## Installing Docker

#### Install docker using [convenience script](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-convenience-script)
    
    sudo apt-get install curl
    curl -fsSL get.docker.com -o get-docker.sh
    sudo sh get-docker.sh

#### Steps to use docker without having to use sudo
    
    sudo groupadd docker
    # Add your user to the docker group.
    sudo usermod -aG docker $USER
    # Close the terminal or restart computer to see effects

# Setting up the workspace on users computer

    mkdir -p drone/home

   # enable access to xhost from the container
    xhost +

   # Run docker and open bash shell

    docker run -it --privileged --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" -v ~/drone/home:/home/:rw --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" -p 14556:14556/udp --name=drone avi241/drone-pc bash
   ### start docker container
    docker start drone
   ### stop the container
    docker stop drone
   ### remove the container
    docker rm drone
   ### list container
    docker container ls -a # -a is for all whether container is running or not
   ### list docker images
    docker image ls -a
   ### remove image
    docker image rm avi241/drone-pc
   ### open a new bash shell of this container
    docker exec -it drone bash
    
   # Pushing our own container to repo
   
   ### login in docker account
    docker login
   ### logout 
    docker logout
   ### Commiting the container to make it an image
    docker commit {container_name} {repo name}
    eg: docker commit drone avi241/drone-pc2
   ### Pushing the image to repo
    docker push avi241/drone-pc2
   
