---
title: Running with Docker
slug: running-with-docker
description: Directions on how to get Laramie running on Docker
---

#Running with Docker

- [Introduction](#introduction)
- [Get Docker](#get-docker)
- [Get your containers up](#containers)


<a name="introduction"></a>
##Introduction

Other options for getting started may be easier (see <a href="https://laravel.com/docs/homestead" target="_blank">Homestead</a> or <a href="https://forge.laravel.com/" target="_blank">Forge</a>), but if you already have Docker installed (or want to) and eschew installing lots of additional stuff just to get a web application up, running Laramie on Docker isn't too hard (plus you get get some hacker points).

This guide assumes that you're starting out from scratch: no Docker, no system-level php, no nothing. Cool? Let's get started.


<a name="get-docker"></a>
##Get Docker

First things first: <a href="https://www.docker.com/community-edition#/download" target="_blank">install Docker</a>. If you already have it, wonderful!


<a name="containers"></a>
##Get your containers up

We're going to use a `docker-compose.yml` file to describe the environment that we'll use for running our application (don't worry, we'll quickly describe this file in a minute):

```yaml
version: '3'
services:
  web:
    image: laramie/docker-quickstart
    command: php -S 0.0.0.0:8080 -t /var/www/web/public
    container_name: laramie
    ports:
      - "8080:8080"
    volumes:
      - ./:/var/www/web
    links:
      - db
  db:
    image: postgres:9.6
    container_name: laramie-postgres
    environment:
      - POSTGRES_USER=dev
      - POSTGRES_PASSWORD=123
    ports:
      - "5432:5432"
  adminer:
    image: dehy/adminer
    container_name: adminer
    links:
        - "db"
    ports:
      - "8081:80"
```

Save this to a file named `docker-compose.yml` at the root of your Laravel / Laramie project.

Next, execute `docker-compose up` (or `docker-compose up -d` to run it in the background). The first time you run this command it's going to take a little while -- which is ok -- Docker has to reach out and fetch all the required images.

TODO -- modify docker setup to contain composer.php and bootstrap