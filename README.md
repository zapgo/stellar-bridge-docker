# Docker-compose setup for Stellar Bridge Server

Get the Stellar Bridge Server up and running in a docker container. This repository may not contain the latest Stellar Bridge Server and is intended more as a quickstart example.

## Requirements
 - Docker
 - Docker-compose

## Instructions
### 1. Build the docker image:
`docker-compose build bridge`

### 2. Create the config file:
Create a the file app/bin/config_bridge.toml.
`cp config_bridge_example.toml app/bin/config_bridge.toml`

Make sure the MySQL DB IP address matches the static address set in your docker compose file. e.g:
> url = "root:mysql@tcp(172.16.238.10:3306)/mysql?parseTime=true"

### 2. Run the bridge server:
docke-compose up

### Optional copy compiled code:
This repository contains the compiled code in the /app directory, so the following steps are not neccessary:

When building the docker container in step one, the code is compiled to /go/src/app/ in the container.

Let's copy this to the /app/ directory on the host machine:
`docker run -d --name bridge stellarbridgedocker_bridge bash -c "godoc -goroot=. -http=:6060"`  
`docker cp bridge:/go/src/app/ ./`  
`docker stop bridge`  
`docker rm bridge` 

Be sure to repeat step 2 after running this.