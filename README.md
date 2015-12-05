## Nice Artisan ##

This package is to add a web interface for Laravel 5 Artisan.

It's still a work in progress.

### Installation ###

Add Nice Artisan to your composer.json file :
```
    composer require bestmomo/nice-artisan
```

Update Composer :
```
    composer update
```

The next required step is to add the service provider to config/app.php :
```
    Bestmomo\NiceArtisan\NiceArtisanServiceProvider::class,
```

And copy the package config to your local config with the publish command:
```
    php artisan vendor:publish
```

You can change options and commands in `config/commands.php`. The menu is dynamically created with this config.

Now it must work with this url :
```
    .../niceartisan
```



### Middleware ###

If you want to use this package on a production application you must protect the urls with a middleware for your security !

Add a route middleware to your application, for example :
```
<?php 

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\RedirectResponse;

class NiceArtisan {

    /**
     * Handle an incoming request.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \Closure  $next
     * @return mixed
     */
    public function handle($request, Closure $next)
    {
        $user = $request->user();

        if ($user && $user->isAdmin())
        {
            return $next($request);
        }
        return new RedirectResponse(url('/'));
    }

}
```

And register it in Kernel with `nice_artisan` name :

```
protected $routeMiddleware = [
    ....
    'nice_artisan' => \App\Http\Middleware\NiceArtisan::class,
];

``` 

### Screenshots ###

![nice-artisan1](https://cloud.githubusercontent.com/assets/2959682/11610549/a9a3055c-9ba6-11e5-936b-f1d3830baf62.jpg)
![nice-artisan2](https://cloud.githubusercontent.com/assets/2959682/11610548/a9a308e0-9ba6-11e5-9cee-94d7cc373024.jpg)
![nice-artisan3](https://cloud.githubusercontent.com/assets/2959682/11610547/a9a00942-9ba6-11e5-88b6-9c30f25f220f.jpg)

