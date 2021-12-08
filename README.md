# docker-laravel 🐳

## Introduction

Build a simple laravel development environment with docker-compose.

## Usage

```bash
$ git clone 
$ cd docker-laravel
$ make create-project # Install the latest Laravel project
$ make install-recommend-packages # Optional
```

http://localhost

## Container structures

```bash
├── app
├── web
└── db
```

### app container

- Base image
  - [php](https://hub.docker.com/_/php):8.0-fpm-bullseye
  - [composer](https://hub.docker.com/_/composer):2.1

### web container

- Base image
  - [nginx](https://hub.docker.com/_/nginx):1.20-alpine
  - [node](https://hub.docker.com/_/node):16-alpine

### db container

- Base image
  - [mysql/mysql-server](https://hub.docker.com/r/mysql/mysql-server):8.0
