# MySQL/Maria DB Cheatsheet

* MariaDB supports UCA1400: `uca1400_as_ci` where as MySQL support UCA 900:`utf8mb4_0900_ai_ci`. MariaDB never supported 900. (UCA: Unicode Collation Algorithm)
*  `utf8mb4_unicode_520_ci` is acceptable when 1400/900 is not available. Previously, `utf8mb4_general_ci` was preferred.



* Set UTF-8 character sets in `my.ini`
* nvarchar and ntext are not required as MariaDB and MySQL use UTF-8.
* https://mariadb.com/docs/server/reference/data-types/string-data-types/character-sets/supported-character-sets-and-collations
* https://www.toptal.com/php/a-utf-8-primer-for-php-and-mysql

## Further Reading

* [How to support full Unicode in MySQL databases](https://mathiasbynens.be/notes/mysql-utf8mb4) includes converting.