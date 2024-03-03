- docker build --t feedback-node .
- docker run -p 3000:80 --name feedback-app -d --rm feedback-node
- here feedback-node is the tag of image
# Named Volumes  
- Volume flag
- docker run -p 3000:80 --rm -d --name feedback-node -v feedback:/app/feedback feedback-node:volume
- VolumeName:path of volume for container
- Anonymous volumes deleted when container stopped.
# Bind Mounts
- Problem with Named Volumes that we need rebuild image again after every vhange in code here comes bind mounts
- Bind mounts you need to specify your local host folder path and container path in docker run command with -v flag
- -v <absolute Path to your project>:<containerPath>
- but nodemodules override due to dockerfile instructions and this bind mount you we have to sue anonymous volume to add node_modules again bcz internal longer path wins
- docker run -d -p 3000:80 --name feedback-app -v feedback:/app/feedback -v "<projectAbsolutePath>:/app" -v /app/node_modules feedback-node:volume