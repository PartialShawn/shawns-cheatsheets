# PHP Cheatsheet

## Newish featuers to keep in mind

- Use `??` for `isset()` checks: `$var = $x[$y] ?? null;`
- php8.5:
  - Chain with pipe operator (`|>`) on separate lines. Eg. `$var = 'Hello, world!' |> strtoupper(...) |> str_shuffle(...) |> trim(...);`

## Singletons

```
class ExampleSingleton
{
    private static $instance;
    private $x;

    private function __construct()
    {
        $this->x = /* ... */;
    }

    public static function getInstance()
    {
        if (!isset(self::$instance)) {
            self::$instance = new self;
        }

        return self::$instance;
    }

    public function getX($key)
    {
        return $this->x[$key];
    }
}

$x = ExampleSingleton::getInstance();
$ret = $x->getX("test");
```

* [Singleton in PHP (complete guide)](https://mderis.medium.com/singleton-in-php-complete-guide-31fa96c45ac9) 2023
* [Singleton](https://phptherightway.com/pages/Design-Patterns.html#singleton) from PHP: The Right Way

## Exceptions and Error Handling

Settings for httpd.conf, .htaccess, php.ini, etc.

On a development server:
- `error_reporting` should be set to E_ALL value;
- `display_errors` should be set to 1
- `log_errors` could be set to 1

On a production server
- `error_reporting` should be set to E_ALL value;
- `display_errors` should be set to 0
- `log_errors` should be set to 1

Eg:
```
error_reporting(E_ALL);
ini_set('display_errors', 1);
```

### PHP Errors

Convert errors to exceptions:

```
set_error_handler(function ($level, $message, $file = '', $line = 0)
{
    throw new ErrorException($message, 0, $level, $file, $line);
});
```

### Server Handlers

Set server to show the nice error page. Eg., all 5xx to a 500.html page.

### Handle in PHP

Basic way to handle exceptions, to which one could add a nicer display.

```
set_exception_handler(function ($e)
{
    error_log($e);
    http_response_code(500);
    if (ini_get('display_errors')) {
        echo $e;
    } else {
        echo "<h1>500 Internal Server Error</h1>
              An internal server error has been occurred.<br>
              Please try again later.";
    }
});
```

### Stuff or DB/PDO
$pod_object->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );


### Outdated Info

On old versions of PHP, use `trigger_error()` with, eg. `json_last_error_msg()` or `mysql_error()`, or throw a new exception for the error:

```
class NewException extends ErrorException {}
...
if ($error = json_last_error())
    throw new NewException(json_last_error_msg(), $error);
```








## TODO

- Look at my JSON decoder and encoders and turn on JSON_THROW_ON_ERROR https://www.php.net/manual/en/function.json-decode.php

Character encoding

* https://www.php.net/manual/en/ref.iconv.php
* https://www.php.net/manual/en/ref.mbstring.php