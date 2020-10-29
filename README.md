### About

Run your development environment with a single command using docker-compose. 

Based on the following containers:
- dphp      (php:7.4-fpm)
- dnginx    (nginx:latest)
- mariadb   (mariadb:latest)
- phpmyadmin

Container names will be generated using the following mask: 

<code>nginx - $ {PROJECT_NAME}</code>

### Runing 

1) install <a href="https://docs.docker.com/engine/install/">Docker</a> and <a href="https://docs.docker.com/compose/install/">Docker-compose</a>
2) clone the repository:

<code>git@github.com:tt0y/docker-dev-environment.git</code>  

3) create the config file 

<code>cp .env.example .env</code>

4) enter the required data in .env file
 
5) run following command in the terminal:

<code> docker-compose up --build "$@" </code>

--- 

to start use:
<code>./docker/start</code>

to stop use:
<code>./docker/kill</code>