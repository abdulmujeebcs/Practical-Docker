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
-  