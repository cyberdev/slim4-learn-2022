# slim4-learn-2022
Learning Slim in 2022

**Installation**
```batch
composer require slim/slim:"4.*"
composer require slim/psr7
composer require nyholm/psr7 nyholm/psr7-server
composer require guzzlehttp/psr7 "^2"
composer require laminas/laminas-diactoros
```

**Basic Usage Hello World App**
```php
<?php
use Psr\Http\Message\ResponseInterface as Response;
use Psr\Http\Message\ServerRequestInterface as Request;
use Slim\Factory\AppFactory;

require __DIR__ . '/../vendor/autoload.php';

$app = AppFactory::create();

/**
 * The routing middleware should be added earlier than the ErrorMiddleware
 * Otherwise exceptions thrown from it will not be handled by the middleware
 */
$app->addRoutingMiddleware();

/**
 * Add Error Middleware
 *
 * @param bool                  $displayErrorDetails -> Should be set to false in production
 * @param bool                  $logErrors -> Parameter is passed to the default ErrorHandler
 * @param bool                  $logErrorDetails -> Display error details in error log
 * @param LoggerInterface|null  $logger -> Optional PSR-3 Logger
 *
 * Note: This middleware should be added last. It will not handle any exceptions/errors
 * for middleware added after it.
 */
$errorMiddleware = $app->addErrorMiddleware(true, true, true);

$app->get('/', function (Request $request, Response $response, $args) {
	$response->getBody()->write("Hello world!");
	return $response;
});

$app->run();
```
**Run with PHP's built-in webserver**
```batch
php -S localhost:8080 -t public public/index.php
```