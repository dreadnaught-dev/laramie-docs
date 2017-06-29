---
title: Running with Docker
slug: running-with-docker
description: Directions on how to get Laramie running on Docker
---

#Running with Docker

- [Introduction](#introduction)
- [Get Docker](#get-docker)
- [Get your containers up](#containers)
- [Configure your containers](#configure)


<a name="introduction"></a>
##Introduction

Other options for getting started may be easier (see <a href="https://laravel.com/docs/homestead" target="_blank">Homestead</a> or <a href="https://forge.laravel.com/" target="_blank">Forge</a>), but if you already have Docker installed (or want to) and eschew installing a full-blown virtual machine just to test things out, running Laramie on Docker isn't too hard (plus you get get some hacker points).

This guide assumes that you're starting out with <a href="https://laravel.com/docs/installation#installing-laravel" target="_blank">Laravel installed somewhere</a> but not actively being served. Cool? Let's get started.


<a name="get-docker"></a>
##Get Docker

First things first: if you don't already have it, <a href="https://www.docker.com/community-edition#/download" target="_blank">install Docker</a>. If it's already installed, wonderful!


<a name="containers"></a>
##Get your containers up

We're going to use a `docker-compose.yml` file to describe the environment that we'll use for running our application (don't worry, we'll go over it in a minute):

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

Notice that our `docker-compose.yml` file lists several containers. Here's what they do:
- **web**: This container includes php and its postgres bindings. It's what's going to actually run the web application.
- **db**: This is the PostgreSQL db server. Our web container is going to connect to it for the db.
- **adminer**: This is a convenience application so that you can get insight into what the db looks like and run SQL queries without installing a postgres-specific db explorer (although you can). After your containers are running, simply visit `http://localhost:8081` and use the following credentials to connect to your db:
  <a name="db-settings"></a>
  ```
  System: PostgreSQL
  Server: laramie-postgres
  Username: dev
  Password: 123
  ```

<a name="configure"></a>
##Configure your containers

We're getting close. Just a couple of things left to do:

First, the application needs a database to connect to. Connect to the postgres server by using adminer as [described above](#db-settings) (or you can use a native app if you'd like). Create a new database (for the purposes of this tutorial, we're calling it `laramie`)

Next, modify your app's `.env` file with the following:

```bash
DB_CONNECTION=pgsql
DB_HOST=laramie-postgres
DB_DATABASE=laramie
DB_USERNAME=dev
DB_PASSWORD=123
```

Finally, we need to execute the migrations. However, we're going to have to connect to our Docker web server to do so (here's where some hacker points come in).

```bash
docker exec -it laramie /bin/bash `#think of this as ssh'ing into the container`
php /var/www/web/artisan vendor:publish `#copy some of Laramie's assets to public locations`
php /var/www/web/artisan make:auth `#if you haven't done so already, tell Laravel to make its auth tables, etc`
php /var/www/web/artisan migrate `#run the migrations`
```

Keep this terminal open, we'll use it again in a second. Now we just need to authorize a user for access. For that, we need a user. The easiest way to do that is to register one through the site's frontend (<a href="http://localhost:8080/register" target="_blank">http://localhost:8080/register</a>).

Once you have a registered user, you can authorize them to access the admin:

```bash
php /var/www/web/artisan laramie:authorize your-user@email.com
```

Done! You should now be able to access <a href="http://localhost:8080/admin" target="_blank">http://localhost:8080/admin</a>.