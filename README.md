# WEBAPPSTORE CI/CD Pipeline

A Python Flask web application that retrieves data from a clients database table and packages it as a Docker container.

## Key Features

    Docker containerization

    Database connectivity (supports multiple database backends)

    Configurable via environment variables

    Python 3 with Flask framework

## Prerequisites

    Docker installed

    up and running database mariadb container 

    Database with a clients table 

## Recommandation 
optimaziation reason use the image python:3.9-slim <br/> 
for security reason create user **webapp** than can be used as default user in the container 


## Setting up environment 
    Create new directory project 
      mkdir project 

    Create a Dockerfile 
      cd project 
      touch docker file 

    clone this repository 
      git clone https://github.com/kimynxlab/clients.git 

    execute this commande to chech project tree 
      student@Docker:~/projet/# tree 
        .
        ├── clients
        │   ├── clients.html
        │   ├── index.html
        │   ├── README.md
        │   ├── requirements.txt
        │   └── webapp.py
        └── Dockerfile

## Building docker image using Dockerfile 
the commandes bellow have to be done using Dockerfile 

    Upgrade pip (required before package installation):
      pip install --upgrade pip

    Install required Python packages:
      pip3 install flask  mysql-connector-python

    Exposed port is 5000 in TCP

 
    The application requires these environment variables:       
        **these variable can be added to the Dockerfile or injected when running the container**
        **For better flexibility inject them when running a container expet for  FLAS_APP**
 
 Requirement | Description               | default value      |Required in Dockerfile |
|------------|---------------------------|--------------------|------------------------
| FLAS_APP   | Path of the application   | /app               |      yes              |
| DBUSER     | username used for DB      | admin              |      no               |
| DBPASSWORD | password used for DB      | admin              |      no               |
| DBHOST     | IP add or FQDN of DB host | inspect container  |      no               |
| DB         | Is the name of database   | webstore           |      no               | 


    Entrypoint of the application 
         ENTRYPOINT ["flask", "run", "--host", "0.0.0.0", "-p", "5000"]


## Building the image :
docker build -t name:tag .

### example 
docker build -t webapp:latest .

## Running container example : 
docker run --name webapp -p 80:5000 \ 
    -e DBUSER=root \
    -e DBPASSWORD=root 
    -e DBHOST=172.16.0.2 \
    -e DB=clientdb \ 

**Note : you have to have mariadb container up and running with user root and password root**



