# Goals Project ~ Dockerize multiple services
- docker run --name goals-backend-app --network goals-nt -it -p 3003:80 goals-backend

- docker run --name goals-frontend-app -it -p 3000:3000 goals-frontend 

(no need for network bcz reacjs code runs on browser so docker Ip resolvers for containers name like http://goasl-backend-app/ will ot reoslved bcz react code does not run in cotnainer but in browser)

- docker run --name mongodb --network goals-nt mongo
# Data persistance in mongo

- use named volume just name:path to mongo data
- forexample -v data:/data/db
- docker run --name mongodb -d -v data:/data/db --network goals-nt mongo
# authentication for mongo (others container to authenticate)
docker run --name mongodb -d -v data:/data/db -e MONGO_INITDB_ROOT_USERNAME=mongoadmin -e MONGO_INITDB_ROOT_PASSWORD=Docker2024 --network goals-nt mongo