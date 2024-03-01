# Docker Images
- images contain the code, setup and meet
- containers are the running instances of those images

## All Running containers
- docker ps -a
## Interactive Container
- docker run -it node 
- where we can run node basic commands and APIs like filesystems

## Dockerfile
- contains the instructions for the Docker that we wanna execute when we build our own image
- starts with FROM which will built your image on another built in image like node
- COPY . /app copy all the current directory files and sub folders inside the docker container "app" directory  
- inside the image you want to run command with RUN
- but there is issue By default, all those comands will be executed in the working directory if your cotnainer. by defualt working drectory is root directory.
- bcz we copy all files into app directory so we need to set instruction for docker to change the WORK DIR
- COPY . / bcz due to WORKDIR not just RUN command but also COPY will execute relative to this working directory
- you can also more explicitly here COPY . /app so we dont have to guess what WORKDIR is
- All the instructions in the Dockerfile for building image
- incorrect: RUN node server.js it will only executed when this image will built (keep in mind image should be template for the container bcz in the end container is runnig not image)
- correct way:must write CMD command at last
- CMD (will only executed when container starts)
- CMD ["node", "server.js"]
- EXPOSE certain port (optional) only used for documentation purposes
- must use flag -p 3000:80 (-p publish <localhost Port>:<internal docker container port>)
  
# Images are read only
- (no changes reflection) we copy our source code into the image and we snapshot our code in the time of copy.
- we have to rebuilt image every time we change
- images are readonly after built. you cannot change anything in image after built

# Understanding image layers
- Layer based: Superfast after again building same image. Docker used cache as you know docker already executed these instructions before bcz there is no change.
- every instruction in your Dockerfile creates a layer.
- UseCase: docker only rebuilt or reexecutes what needs to be reexecuted.
- everytime we change code in other files then npm i run everytimes.
- so in the future npm i will not run again if we copy all files after runing npm install
## Help
- any docker comand with --help to view all the arguments of command

# Stopping & Restarting containers
-  docker ps show running containers
-  docker ps -a show all containers you had in the past incl stopped containers
-  docker run (you create new container) sometimes we want to run stopped so u just  need to restart docker start name_of_container.

# Understanding Detached & Attached Containers
- when we enter docker run command we stuck in the process unable to enter anything (The containers is running in foreground) but with docker start run in the background.
- Attached mode while run command and start having detached mode.
- In application, console.log() is written to terminal we are unable to see this in detached mode (docker start).
- Attached means we are listening to the output of that container.
- we can also run docker run with flag -d for detached mode run container in background.
- if you want to work on same terminal use detached mode easily.
- we can attach running container as well with docker attach <container_name>
- docker logs command to fetch logs that printed by container 
 docker logs <container_name>
- docker logs -f <container_name> future logs
- docker start -a <container_name> start container in attached mode

# Interactive mode
- console application like in Python project we need to run container in interactive mode so we can enter our input so use docker run -i or if want terminal as well use -it
- docker start -a -i <container>

# Remove containers & images
- docker rm <container names sperated by space> container1 container2
- docker images (list images)
- docker rmi ImageId
- get rid of all unused images -> use docker image prune
- docker run -p 3000:80 -d --rm CONTAINER_NAME (Automatically removes the container when its stopped)
# Docker image inspect
- docker containers are thin layer on top of images. multipel runing on the same image which means applciation code and enironment ahs been shared with others containers not copied that why the code inside of the image is also locked but you can create files on containers.
- docker image inspect (all info about image)
- docker naming with --name flag

# Copying files from & to the container
- docker cp dummy/. cotnainername:/test
- above command copy all files in dummy folder to test folder in container
# Image Tagging
- tag consists of name:tag (tag is for version or specialized image within group of images). combined a unique identifier.
- when building image use -t for tag
- docker build -t lamp:1.0 .
-  now you can use image tags in running cotainer docker run lamp:1.0

# Sharing Image
- Share built image: download an image and run container based on it. no build step required.