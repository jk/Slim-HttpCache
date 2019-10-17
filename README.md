# Slim Framework HTTP Cache

[![Build Status](https://travis-ci.org/slimphp/Slim-HttpCache.svg?branch=master)](https://travis-ci.org/slimphp/Slim-HttpCache)

This repository contains a Slim Framework HTTP cache middleware and service provider.

## Requirements

- PHP 7.1 or newer

## Install

Via Composer

``` bash
$ composer require slim/http-cache
```

## Usage

```php
// Create Container using PHP-DI
$container = new Container();

// Set container to create App with on AppFactory
AppFactory::setContainer($container);
$app = AppFactory::create();

// Register middleware
$app->add(new \Slim\HttpCache\Cache('public', 86400));

// Fetch DI Container
$container = $app->getContainer();

// Register service provider
$container->set('cache', function () {
    return new \Slim\HttpCache\CacheProvider();
});

// Example route with ETag header
$app->get('/foo', function ($req, $res, $args) {
    $resWithEtag = $this->cache->withEtag($res, 'abc');

    return $resWithEtag;
});

$app->run();
```

## Testing

``` bash
$ vendor/bin/phpunit
```

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security

If you discover any security related issues, please email security@slimframework.com instead of using the issue tracker.

## Credits

- [Josh Lockhart](https://github.com/codeguy)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
