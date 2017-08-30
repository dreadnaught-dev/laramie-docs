---
title: Customize your dashboard
slug: customize-your-dashboard
description: How to customize your generic Laramie admin dashboard
---

# Customize your dashboard <span class="subtitle">in two easy-ish steps</span>

Customizing your dashboard is simply a matter of getting data into your dashboard and then displaying it. This page will help with that.

## 1. Inject data into your dashboard view

To show anything dynamic, you need to get data into your application's dashboard. To do so, modify your app service provider's boot method to inject the data you need (see app/Providers/AppServiceProvider.php).

You may leverage Laramie's data service to inject model-related data, but you're free to inject any data you want, whether it be Laramie-administered data, data from another table (or database entirely), data that's the result of a curl call... whatever.

```
public function boot()
{
    ...
    // Inject data into your dashboard as needed
    View::composer(['laramie::dashboard'], function ($view) {
        $view->with('salesFigures', $myAppDataService->getSalesFigures());
        $view->with('stockPrices', $myAppDataService->fetchStockPrices());
    });
}
```

## 2. Lay your data out

When you installed Laramie, you ran `php artisan vendor:publish`. This command copied some of Laramie's assets out to your application so that you could more easily modify them. The generic dashboard blade was copied to `resources/views/vendor/laramie/dashboard.blade.php`. This is the file you're going to modify.

Laramie's admin was built upon a light-weight CSS framework called [Bulma](http://bulma.io/). If you'd like to achieve a WordPress-esque admin layout, you'll likely want to bone up on Bulma's [card](http://bulma.io/documentation/components/card/), [tile](http://bulma.io/documentation/layout/tiles/), and [box](http://bulma.io/documentation/elements/box/) documentation -- it's pretty straight-forward. But in the end it's all just good ol' HTML and blade syntax, so do whatever floats your boat.

-----

### Example layout components

Note that these examples were taken straight from Bulma's website (see [Bulma's documentation](http://bulma.io/) for more).

### Box
<div class="box">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus nec iaculis mauris. <a>@bulmaio</a>.</p>
</div>
```
<div class="box">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus nec iaculis mauris. <a>@bulmaio</a>.</p>
</div>
```

### Card
<div class="card">
    <header class="card-header">
        <p class="card-header-title">
            Component
        </p><a class="card-header-icon"><span class="icon"><i class="fa fa-angle-down"></i></span></a>
    </header>
    <div class="card-content">
        <div class="content">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus nec iaculis mauris. <a>@bulmaio</a>.
            <a>#css</a> <a>#responsive</a><br>
            <small>11:09 PM - 1 Jan 2016</small>
        </div>
    </div>
</div>
```
<div class="card">
    <header class="card-header">
        <p class="card-header-title">
            Component
        </p><a class="card-header-icon"><span class="icon"><i class="fa fa-angle-down"></i></span></a>
    </header>
    <div class="card-content">
        <div class="content">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus nec iaculis mauris. <a>@bulmaio</a>.
            <a>#css</a> <a>#responsive</a><br>
            <small>11:09 PM - 1 Jan 2016</small>
        </div>
    </div>
</div>
```

### Tiles
<div class="tile is-ancestor">
    <div class="tile is-vertical">
        <div class="tile">
            <div class="tile is-parent is-vertical">
                <article class="tile is-child notification is-primary">
                    <p class="title">Vertical...</p>
                    <p class="subtitle">Top tile</p>
                </article>
                <article class="tile is-child notification is-warning">
                    <p class="title">...tiles</p>
                    <p class="subtitle">Bottom tile</p>
                </article>
            </div>
            <div class="tile is-parent">
                <article class="tile is-child notification is-info">
                    <p class="title">Middle tile</p>
                </article>
            </div>
        </div>
    </div>
</div>
```
<div class="tile is-ancestor">
    <div class="tile is-vertical">
        <div class="tile">
            <div class="tile is-parent is-vertical">
                <article class="tile is-child notification is-primary">
                    <p class="title">Vertical...</p>
                    <p class="subtitle">Top tile</p>
                </article>
                <article class="tile is-child notification is-warning">
                    <p class="title">...tiles</p>
                    <p class="subtitle">Bottom tile</p>
                </article>
            </div>
            <div class="tile is-parent">
                <article class="tile is-child notification is-info">
                    <p class="title">Middle tile</p>
                </article>
            </div>
        </div>
    </div>
</div>
```