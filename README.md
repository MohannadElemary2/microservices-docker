
# Microservices Dockerization 🐳

## Introduction

This is the dockerization of the microservices application [Here](https://github.com/MohannadElemary2/microservices)

## Usage

```bash
$ git clone https://github.com/MohannadElemary2/microservices-docker.git
$ cd microservices-docker
$ git clone https://github.com/MohannadElemary2/microservices
$ mv microservices backend
$ docker-compose build
$ docker-compose up -d
```

http://localhost

## Container structures

```bash
├── registration
├── web
├── db
├── zookeeper
├── kafka
├── kafka-topics-creator
├── mongo
└── notifications
```

## registration container
The laravel app container.

- Base image
  - [php](https://hub.docker.com/_/php):8.0-fpm-bullseye
  - [composer](https://hub.docker.com/_/composer):2.1

## web container
The web server (nginx) container.

- Base image
  - [nginx](https://hub.docker.com/_/nginx):1.20-alpine
  - [node](https://hub.docker.com/_/node):16-alpine

## db container
The MySQL database container.

- Base image
  - [mysql/mysql-server](https://hub.docker.com/r/mysql/mysql-server):8.0

## zookeeper container
The zookeeper service container.

- Base image
  - [bitnami/zookeeper](https://hub.docker.com/r/bitnami/zookeeper):3.7

## kafka container
The kafka broker service container.

- Base image
  - [bitnami/kafka](https://hub.docker.com/r/bitnami/kafka):3

## kafka-topics-creator container
This container creates the `email-notifications` topic while startup and then terminats .

- Base image
  - [confluentinc/cp-kafka](https://hub.docker.com/r/confluentinc/cp-kafka):latest

## mongo container
The MongoDB database container.

- Base image
  - [mongo](https://hub.docker.com/_/mongo)

## notifications container
The Python app container. It's just starts the Python app and running the `run_consumer` command to create the kafka consumer.

- Base image
  - [python](https://hub.docker.com/_/python):3
