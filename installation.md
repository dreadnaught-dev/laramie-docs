# Installation

- [Server requirements](#requirements)
- [Installing Laramie](#install-laramie)
- [Trying things out](#kicking-tires)

<a name="requirements"></a>
## Requirements

Laramie is a composer package _for_ Laravel. So Laravel is requirement number one. For Laravel's requirements and installation instructions, [see here](https://laravel.com/docs/installation). In addition to Laravel's requirements, Laramie's juju also requires:

- PostgreSQL 9.4 or greater with a user that has privileges to create database extensions (a user with advanced privileges is only needed for the initial migration).
- [Laravel's authentication facilities](https://laravel.com/docs/authentication) must be enabled, and at least one user should be configured (for the purpose of this guide, we're assuming their email is `your-user@email.com`).
- The `gd` or `imagick` php extension(s) should be installed (for image manipulation).

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
php artisan laramie:authorize your-user@email.com
```

Congratulations! That's all there is to it! You should now be able to visit <a href="http://your-site.dev/admin" target="_blank">http://your-site.dev/admin</a> to start managing your content.

<a name="kicking-tires"></a>
## Trying things out

If you'd like to try Laramie out, [Homestead](https://laravel.com/docs/homestead) should work (although it's untested). Alternatively, if you have [Docker](https://docs.docker.com/engine/installation/) installed (or would like to), see [Testing on Docker](/docs/{{version}}/testing-on-docker)
