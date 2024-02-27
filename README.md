# Laravel App

Laravel application, at the moment, serves two purposes. `Authentication` and (JSON only) `application programming interface (API)`.
Both of these functionalities are made possible with the assistance of one or more packages. More notably we have:

-   Laravel's (own) [Passport](https://github.com/laravel/passport) for `authentication`, which seems to be the official implementation of
    [thephpleague/oauth2-server](https://github.com/thephpleague/oauth2-server).
-   [Laravel JSON API](https://github.com/laravel-json-api/laravel) package for (JSON only) `API`.

\*\* Further research has to be made on these packages. [oauth2-server-bundle](https://github.com/thephpleague/oauth2-server-bundle) // For Symphony

## Passport Authentication/Authorization

The default authentification package for managing requests is [Laravel Passport]().

Changes to this package have been made that we have yet to explore.
However thus far, we've encountered that there is a change in the way passport is registering their routes.

`routes/oauth.php` file registers the routes for the `/login` view `get` and `post` routes.
Loaded by `App/Providers/RouteServiceProvider` with `web (middleware)`.
`post` route logic is managed by `App\Http\Controllers\Auth\AuthenticationController` login method.

`resources/views/login.blade` is an HTML layout that includes in the document head

```
<meta name="csrf-token" content="{{ csrf_token() }}">

<title>{{ config('app.name') }}</title>

@vite('resources/js/login.js')
```

and mounts a Vue "app" in `body#app` that has at the moment only two components. The login form and the login view. That should take care of the front-end logic (only).

Inside `vite.config.js` we declare within the plugins the correct js that will be executing this task as well.

```
laravel({
    input: [
        path.resolve(__dirname, "./resources/js/login.js"),
    ],
}),
```

### Installation

If project template is being used of the first time then we'll have to run:

```
php artisan passport:keys
```

Public client will have to be created as well with the following command:

```
php artisan passport:client --public
```

Note the client ID as it will be important for the future.There is no Client Secret for this auth method.