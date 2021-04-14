# Docker to run DIVE
DIVE is a great open source project that allows data to be injested, has mixed initiative visualisation recommendation and allows visualisations to be assembled into stories. 

The original DIVE frontend and backend have been forked and updated:
* https://github.com/aneesha/DIVE-frontend
* https://github.com/aneesha/DIVE-backend <- ported to Python 3.8

Docker compose is used to create the following containers:
* Build DIVE-frontend from the git repo
* Run Postgres
* Run RabbitMQ
* Run DIVE-backend api (Flask with gunicorn)
* Run Web Worker (inc celery)
* Run nginx (with SSL and certs)

## Todo
- [ ] Make compose file for running locally with python and react hotloading
- [ ] Make env files for RabbitMQ and Postgres username and password

## Instructions 

1. Git clone this repo and cd DIVE-docker
```
$ git clone https://github.com/aneesha/DIVE-docker.git
$ cd DIVE-docker
```
2. Git clone the backend repo into dive-api folder
```
$ cd dive-api
$ git clone https://github.com/aneesha/DIVE-backend.git
$ cd ..
```
3. Copy SSL certs into the nginx/certs folder
4. Run docker compose
```
$ docker-compose -f docker-compose.prod.yaml up -d --build
```
5. Setup database migrations
```
$ docker-compose -f docker-compose.prod.yaml exec dive-api python manager.py db init
$ docker-compose -f docker-compose.prod.yaml exec dive-api python manager.py db migrate
$ docker-compose -f docker-compose.prod.yaml exec dive-api python manager.py db upgrade
```
6. Shut down containers
```
$ docker-compose -f docker-compose.prod.yaml down -v
```





