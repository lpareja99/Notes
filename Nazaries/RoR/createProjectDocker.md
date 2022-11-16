### Create Ruby on Rails (RoR) project on Docker

- Prerequisites:
  - Having WLS2 active (using Ubuntu)
  - Download Docker

#### 1. Create folder to hold project (in WSL2 side)
#### 2. Create project in VS
##### Dockerfile
  ``` 
  FROM ruby:3.0
  RUN apt-get update && apt-get install -y nodejs
  RUN mkdir /rubyExample
  WORKDIR /rubyExample
  ```

  - ``` FROM ruby:3:0 ```
    Indicates which image/gem are we using. We can find gems here. Good practive is to include the version we want to install. That way we avoid future problems of different versions. If we do not specify version it intalls teh latest. Use official images.
  - ``` RUN apt-get update && apt-get install -y nodejs ```
    Command to install/update nmp and node.js
  - ``` RUN mkdir /rubyExample ```
    Creation of folder where we are going to hold our project.
  - ``` WORKDIR /rubyExample ```
    Idicates which directory we are going to be using for the project. The same one that we just created in the previous step.
---
##### docker-compose.yml
```
version: '3.1'
```
Version used. In latests versions is not necessary (I think)

- **Database elements:**
```
db: 
    image: mysql:8.0.31
    command: --default-authentication-plugin=mysql_native_password --port 4306
    environment:
    MYSQL_ROOT_PASSWORD: ''
    MYSQL_ALLOW_EMPTY_PASSWORD: 'yes'
    volumes:
    - db:/var/lib/mysql
    ports: 
    - 4306:4306
```
- image: which gem and version of it are we using for the database. By default Rails uses SQLite. But we are using MySQL.
- command: **TODO**
- enviroment: we want to access without password
- volumes: which volume are we using/creating and where. This needs to be declared again down in volumes because it is not a ¿fisical place?
- ports: which port are we using. Inidicate 4306 to not use default one that way different projects would not use the same port.

- **App:**
```
app:
    build: .
    command: bash -c "rm -f /tmp/pids/server.pid && rails s -b 0.0.0.0"
    environment:
    DATABASE_USERNAME: 'root'
    DATABASE_PORT: '4306'
    DATABASE_HOST: 'db'
    volumes:
    - gems:/usr/local/bundle:delegated
    - .:/rubyExample
    ports:
    - 3000:3000
    depends_on: 
    - db
```
- build: directory we are building from
- command: delete files in case they were not deletd and start rails app.
- enviroment: user, port and host of database
- volumes: **TODO**
- ports: which port to use (usng default)
- depends_on: makes sure to create database before running app.

- **Volumes:**
```
volumes: 
    db: 
    gems:
```

#### 3. Launch project
  - On Ubuntu
  - Un Rails
  - Change of folder permisions

#### 4. Commands explanations
   -  ``` $docker-compose build ``` 
Build the project (once both files are up?)
   - ``` $docker-compose run app bash``` **TODO:** understand this one
   - ``` $docker-compose up ``` To get the app running un server once is constructed.
   - ``` $sudo chown -R {previous_owner}:{new_owner} /{path} ``` (ex:sudo chown -R lpareja:lpareja .) To change owners of files and folders recursively