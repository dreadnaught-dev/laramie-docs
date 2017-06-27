---
title: Installation
slug: installation
description: How to install Larami
---

# Installation

- [Intro](#intro)
- [Installation](#installation)
- [Requirements](#requirements)

<a name="intro"></a>
## Intro

Laramie is a magical composer package for [Laravel](https://laravel.com/) that grants your application amazing CMS abilities. Installation is totally non-destructive, so you can install it and not worry about it wrecking existing work. Drop it in and leverage it for your whole application or just parts of it.

But like other magic, it comes at a cost. You should probably know what that is up front:
- First, as it's a package _for_ Laravel, Laravel is a requirement. Easy.
- Laramie's juju requires running postgres 9.4 or greater (for now). So if you're dropping it into an existing app, it won't work if you're on MySQL.
- Not strictly required, but you'll likely want to access Laramie-controlled data via a Laramie service rather than Eloquent (again, Laramie is not an all-or-none proposition. Use Laramie just where it makes sense).

If you can live with those things, Laramie might just be the CMS for you:
- TODO -- list of what's provided

<a name="installation"></a>
## Installation

Laramie is simply a composer package, so installing it couldn't be easier:

``` bash
$ composer require laramie-cms/laramie
```

Add a couple of Laramie service providers to config/app.php:


```php
'providers' => [
    // Other Service Providers

    Laramie\Providers\LaramieServiceProvider::class,
    Laramie\Providers\LaramieEventServiceProvider::class,
],
```

Complete the installation:

``` bash
$ php artisan vendor:publish
$ php artisan make:auth
$ php artisan migrate
$ php artisan laramie:authorize user@email.com
```

<a name="requirements"></a>
## Requirements

Laramie is an amazing CMS-granting package _for_ Laravel... so Laravel is a requirement (see [Laravel's documentation](https://laravel.com/docs/installation) for instructions on how to install Laravel).

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
