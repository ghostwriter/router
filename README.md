# router

[![Compliance](https://github.com/ghostwriter/router/actions/workflows/compliance.yml/badge.svg)](https://github.com/ghostwriter/router/actions/workflows/compliance.yml)
[![Supported PHP Version](https://badgen.net/packagist/php/ghostwriter/router?color=8892bf)](https://www.php.net/supported-versions)
[![GitHub Sponsors](https://img.shields.io/github/sponsors/ghostwriter?label=Sponsor+@ghostwriter/router&logo=GitHub+Sponsors)](https://github.com/sponsors/ghostwriter)
[![Code Coverage](https://codecov.io/gh/ghostwriter/router/branch/main/graph/badge.svg)](https://codecov.io/gh/ghostwriter/router)
[![Type Coverage](https://shepherd.dev/github/ghostwriter/router/coverage.svg)](https://shepherd.dev/github/ghostwriter/router)
[![Psalm Level](https://shepherd.dev/github/ghostwriter/router/level.svg)](https://psalm.dev/docs/running_psalm/error_levels)
[![Latest Version on Packagist](https://badgen.net/packagist/v/ghostwriter/router)](https://packagist.org/packages/ghostwriter/router)
[![Downloads](https://badgen.net/packagist/dt/ghostwriter/router?color=blue)](https://packagist.org/packages/ghostwriter/router)

work in progress

> **Warning**
>
> This project is not finished yet, work in progress.

## Installation

You can install the package via composer:

``` bash
composer require ghostwriter/router
```

## Usage

```php
// work in progress

$middlewares = [
    ErrorHandlerMiddlewareInterface::class => ErrorHandlerMiddleware::class,
];

$route = new Route(['GET','HEAD'], '/', IndexRequestHandler::class, [GuestMiddleware::class], 'home');

$router = new Router($middlewares); // MiddlewareInterface

$router->withRoute($route);

$request = new ServerRequest();

$matched = $router->match($request); // CurrentRoute/RouteInterface


$router->addRoute('GET', '/', HomeHandler::class, [GuestMiddleware::class]);

$router->get('/about', AboutHandler::class, [GuestMiddleware::class]);

$router->get('/auth/github', GitHubLoginHandler::class, [GuestMiddleware::class], 'auth.login.github');

    // create, read, edit, update, store, delete, view, show 
$router->middleware([GuestMiddleware::class], function($router){
    $router->get('/auth/login', LoginCreateHandler::class, 'auth.login.create');
    $router->post('/auth/login', LoginStoreHandler::class, 'auth.login.store');

    $router->get('/auth/register', RegisterCreateHandler::class, 'auth.register.create');
    $router->post('/auth/register', RegisterStoreHandler::class, 'auth.register.store');

    $router->get('/posts', PostIndexHandler::class, 'members.index');
    $router->get('/posts/{post:id}', PostShowHandler::class, 'members.show');
});

$router->middleware([AuthMiddleware::class], function($router){
    $router->get('/users', MembersIndexHandler::class, 'members.index');
    $router->get('/users/{member:id}', MemberShowHandler::class, 'members.show');

    $router->get('/posts/create', PostCreateHandler::class, 'members.create');
    $router->post('/posts', PostStoreHandler::class, 'members.store');
    $router->get('/posts/{post:id}/edit', PostEditHandler::class, 'members.edit');
    $router->put('/posts/{post:id}', PostUpdateHandler::class, 'members.update');
    $router->delete('/posts/{post:id}', PostDeleteHandler::class, 'members.delete');
});
```

### Changelog

Please see [CHANGELOG.md](./CHANGELOG.md) for more information on what has changed recently.

### Security

If you discover any security-related issues, please use [`Security Advisories`](https://github.com/ghostwriter/router/security/advisories/new) instead of using the issue tracker.

### Credits

- [Nathanael Esayeas](https://github.com/ghostwriter)
- [All Contributors](https://github.com/ghostwriter/psalm-plugin/contributors)

### License

The BSD-3-Clause. Please see [License File](./LICENSE) for more information.
