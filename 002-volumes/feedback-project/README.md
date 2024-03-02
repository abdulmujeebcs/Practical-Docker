- docker build --t feedback-node .
- docker run -p 3000:80 --name feedback-app -d --rm feedback-node
- here feedback-node is the tag of image
# Named Volumes  
- Volume flag
- docker run -p 3000:80 --rm -d --name feedback-node -v feedback:/app/feedback feedback-node:volume
- VolumeName:path of volume for container
- Anonymous volumes deleted when container stopped.