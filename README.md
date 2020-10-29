### About

Run your development environment with a single command using docker-compose. 

Based on the following containers:
- dnginx    (nginx:latest)
- dphp      (php:7.4-fpm)

### Runing 

1) install <a href="https://docs.docker.com/engine/install/">Docker</a> and <a href="https://docs.docker.com/compose/install/">Docker-compose</a>
2) clone the repository:

<code>git@github.com:tt0y/docker-dev-environment.git</code>  


3) create the config file 

<code>cp .env.example .env</code>

4) enter the required data in
 
5) run following command in the terminal: 

to start
<code>./docker/start</code>

to stop
<code>./docker/kill</code>