---
title: Installation
slug: installation
description: How to install Laramie
---

# Installation

Laramie is magical a composer pagckage for [Laravel](https://laravel.com) that imparts amazing CMS abilities. Installing it couldn't be easier:

``` bash
composer install laramie-cms/laramie
```

## Requirements

Laramie is an amazing CMS-granting package _for_ Laravel... so Laravel is a requirement (see [Laravel's documentation](https://laravel.docm/docs/installation) for instructions on how to install Laravel).

Server requirements are minimal and are for the most part identical to [Laravel's](https://laravel.com/docs/installation#server-requirements). However, the one caveat is that Laramie's juju **requires** running postgres 9.4 or greater (for now).

If you'd just like to kick the tires, [Homestead](https://laravel.com/docs/homestead) should work (untested). If you have [Docker](https://docs.docker.com/engine/installation/) installed, the following `docker-compose.yml` file should get you started as well (add it to the root of the project):

- **docker-compose.yml**
	``` yaml
	version: '3'
	services:
	  web:
		image: laramie/docker-quickstart
		command: php -S 0.0.0.0:8765 -t /var/www/web/public
		container_name: laramie
		ports:
		  - "8765:8765"
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
	```
- **.env**
	``` bash
		...
		DB_CONNECTION=pgsql
		DB_HOST=laramie-postgres
		DB_DATABASE=laramie
		DB_USERNAME=dev
		DB_PASSWORD=123
	```
