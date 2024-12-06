# Deploy application in Docker compose containers

## Quickstart

```shell
# git basics
git clone git@github.com:jakelime/mern-app-docker.git
cd mern-app-docker
git submodule update --init --recursive

# set up .env files (multiple)
code .
touch .env # write env variables for docker-compose
touch ./src-backend/.env # write env variables for backend app
touch ./src-frontend/.env # write env variables for frontend app
touch ./src-mongodb/.env # write env variables for mongodb app
touch ./src-nginx/.env # write env variables for nginx app

# run
docker compose up

# to stop and stop the entire system
docker compose start
docker compose stop

# to remove the whole system, rebuild and restart
docker compose down
docker compose up --build

```

## .env file for Docker compose

```text
NGINX_PORT=80
```
