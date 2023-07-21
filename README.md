In this article, we will explore how you can set up Netflix Conductor on your local machine using Docker with Postgres as persistence. Here we will setup a standalone

1. Conductor API Server
2. Conductor UI

## 1. Pre requisite 

### Create a Docker network.  

> docker network create --subnet=172.16.238.0/24 mynetwork

### Run the Postgres database.
if you already have a running conatiner connect it the to newly created network.
> docker network connect mynetwork postgres

else
> docker run -p 5432:5432 -d --name postgres --net mynetwork --ip 172.16.238.2 -e POSTGRES_PASSWORD=postgres postgres



## 2. Setup conductor

## Steps

### 1. Clone the Conductor Code
> $ git clone https://github.com/abhijitkushwaha1998/conductor.git
### 2. Build the Docker Server Image
> $ cd conductor

>conductor $ cd docker

>docker $ docker build -t conductor:server -f server/Dockerfile ../

### 3. Run Server Image
>  docker run -p 8080:8080 -d --name conductor_server  --net mynetwork conductor:server

### 4. Run Stand Alone UI Image

From the docker directory

> docker build -t conductor:ui -f ui/Dockerfile ../

> docker run -p 5000:5000 -d --name conductor_ui conductor:ui


This builds the image conductor:ui and runs it in a container named conductor_ui. The UI should now be accessible at localhost:5000.
