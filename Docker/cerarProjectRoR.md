## Create basic RoR project in Docker

- Create Dockerfile
- Create dockercompose.yml
- Build the project `$ docker build .`
- Set up project
  - Run `$ docker compose run {app-name} bash` to acesss internal terminal
  - Install rails: `$ gem install rails`
  - Install dependencies in gemfile: `$ bundle install`
- Start server `$ docker compose up`
- Start a new rails project in teh internal terminal:
  - `$ docker compose run {app-name} bash`
  - `$ rails new . -d mysql`
- Give permission to app folders `$ suod chown -R {user-name} {app-folder}`
- Configure db on file `config/database.yml` 
- Create db for teh project (internal terminal): `$ rails db:create`

---
1. Configurar db en el archivo config/database.yml -> Copiar desde ejemplo dejando el campo database: app_name_development
