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

$app->get('/', function (Request $request, Response $response, $args) {
	$response->getBody()->write("Hello world!");
	return $response;
});

$app->run();
```