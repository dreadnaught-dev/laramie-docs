---
title: Installation
slug: installation
description: How to install Larami
---

# Installation

- [Server requirements](#requirements)
- [Installing Laramie](#install-laramie)
- [Trying things out](#kicking-tires)

<a name="requirements"></a>
## Requirements

Laramie is a composer package _for_ Laravel. So Laravel is requirement number one. For Laravel's requirements and installation instructions, [see here](https://laravel.com/docs/installation). In addition to Laravel's requirements, Laramie's juju depends on the following:

- PostgreSQL 9.4 or greater with a user that has privileges to create database extensions (a user with advanced privileges is only needed for the initial migration)
- [Laravel's authentication facilities](https://laravel.com/docs/authentication) must be enabled, and at least one user should be configured.

<a name="install-laramie"></a>
## Installing Laramie

Laramie is simply a composer package. Installing it couldn't be easier:

``` bash
composer require laramie-cms/laramie
```

Next, register Laramie's service providers with Laravel by modifying `config/app.php`:


```php
'providers' => [
    // Other Service Providers

    Laramie\Providers\LaramieServiceProvider::class,
    Laramie\Providers\LaramieEventServiceProvider::class,
],
```

Complete the installation:

``` bash
php artisan vendor:publish
php artisan migrate
php artisan laramie:authorize your-registered-user@email.com
```

Congratulations! That's all there is to it! You should now be able to visit your-site.dev/admin and start managing your content.

<a name="kicking-tires"></a>
## Trying things out

If you'd like to try Laramie out, [Homestead](https://laravel.com/docs/homestead) should work (although it's untested). Alternatively, if you have [Docker](https://docs.docker.com/engine/installation/) installed, the following `docker-compose.yml` file should be enough to get you started (add it to the root of the project and then run `docker-compose up`). Note that this method is more advanced. See the page on [running with Docker](/docs/{{version}}/docker) for more details.

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

Once your containers are up and running, you'll need to modify your `.env` file to connect to the db service:

``` bash
...
DB_CONNECTION=pgsql
DB_HOST=laramie-postgres
DB_DATABASE=laramie
DB_USERNAME=dev
DB_PASSWORD=123
```

That's it! From here you should be able to follow the installation instructions above. Once those have been completed, you can see your site by visiting [http://localhost:8765](http://localhost:8765).