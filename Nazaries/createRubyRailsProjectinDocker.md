### Create Ruby on Rails (RoR) project on Docker

- Prerequisites:
  - Having WLS2 active (using Ubuntu)
  - Download Docker

1. Create folder to hold project (in WSL2 side)
2. Create project in VS
   - **Dockerfile**
    ``` 
    FROM ruby:3.0
    RUN apt-get update && apt-get install -y nodejs
    RUN mkdir /rubyExample
    WORKDIR /rubyExample
    ```

   - **docker-compose.yml**
    ```
    version: '3.1'
    ```

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

    ```
    volumes: 
    db: 
    gems:
    ```
3. Launch project
    - On Ubuntu
    - Un Rails
    - Change of folder permisions

4. Useful commands
   - ``` $docker-compose build ```
   - ``` $docker-compose up ```
   - ``` $docker-compose run ```
