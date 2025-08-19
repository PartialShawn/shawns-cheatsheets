# PHP Cheatsheet

## Newish features to keep in mind

- Use `??` for `isset()` checks: `$var = $x[$y] ?? null;` and `$var = $x->y ?? null;`
- php8.5:
  - Chain with pipe operator (`|>`) on separate lines. Eg. `$var = 'Hello, world!' |> strtoupper(...) |> str_shuffle(...) |> trim(...);`
- `declare(strict_types=1);`
- `password_hash()`
- https://www.php.net/manual/en/book.intl.php
- empty vs isset
- https://www.php.net/memcached

## RegEx

* Can be deliminated by `/` or `#` or some other stuff.

* Did this one have problems? https://regexr.com/
* https://regex101.com/ or this one?

* https://medium.com/@olivia.j.01101001/how-to-use-php-regular-expressions-for-pattern-matching-and-data-validation-d58dacb06ea1




## Templating in pure PHP

* https://stackoverflow.com/questions/3988627/using-template-on-php/3989380
* https://css-tricks.com/php-is-a-ok-for-templating/
* https://codeshack.io/lightweight-template-engine-php/
* https://www.php.net/manual/en/ref.outcontrol.php

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



## Set UTF-8
* Set PHP to UTF-8 encoding in php.ini / language options
* Send `header('Content-Type: text/html; charset=utf-8');`
* Set PHP's encoding:
    ```
    mb_internal_encoding('UTF-8'); 
    mb_http_output('UTF-8'); 
    mb_regex_encoding('UTF-8'); 
    ```
* For XML set `<?xml version="1.0" encoding="UTF-8"?>` and strip out invalid XML characters.
* First HTML meta should be `<meta charset="utf-8">`
* HTML forms should have `<form accept-charset="utf-8">`
* Use `UTF-8` enconding settings for function for portability:
  * `htmlspecialchars($str, ENT_NOQUOTES, "UTF-8")`
  * `htmlentities()`
  * `$mysqli->set_charset("utf8")`
* Use `/.../u` unicode flag
* https://www.toptal.com/php/a-utf-8-primer-for-php-and-mysql
* The above should say:
  * `$pdo = new PDO('mysql:host=...;charset=utf8mb4')`
  * `$mysqli->set_charset('utf8mb4');`


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
/* Throw exception on error */
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
/* Handle exceptions */
set_exception_handler(function ($e)
{
    error_log($e->__toString());
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

You can have separate logging based on `$errno` with `E_USER_ERROR`, `E_USER_WARNING`
and `E_USER_NOTICE`. I'm not sure if there may be a separate case from all of those.
Also, you could divide it by day or week in the filename.

### Stuff or DB/PDO
$pod_object->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );


### Outdated Info

On old versions of PHP, use `trigger_error()` with, eg. `json_last_error_msg()` or `mysql_error()`, or throw a new exception for the error:

```
class NewException extends ErrorException {}
...
if ($error = json_last_error()
    throw new NewException(json_last_error_msg(), $error);
```








## Quickies

* Loading large files: https://www.sitepoint.com/performant-reading-big-files-php/ and also https://www.uptimia.com/questions/how-to-read-a-large-file-line-by-line-in-php which uses SplFileObject


## TODO

- Look at my JSON decoder and encoders and turn on JSON_THROW_ON_ERROR https://www.php.net/manual/en/function.json-decode.php

Character encoding

* https://www.php.net/manual/en/ref.iconv.php
* https://www.php.net/manual/en/ref.mbstring.php



## Common Resources

* https://phpdelusions.net/
* http://phpsadness.com/
* https://news.ycombinator.com/item?id=12318615
## Random Stuff

Some history:

From https://en.wikipedia.org/wiki/PHP retrieved 2025:

> The fact that PHP was not originally designed, but instead was developed organically has led to inconsistent naming of functions and inconsistent ordering of their parameters.[26] In some cases, the function names were chosen to match the lower-level libraries which PHP was "wrapping",[27] while in some very early versions of PHP the length of the function names was used internally as a hash function, so names were chosen to improve the distribution of hash values.

And the flame war over double colons: https://philsturgeon.com/wtf-is-t-paamayim-nekudotayim/