# Docker Essentials: Task Three

OK. We need to get serious. That idea you suggested for counting
the views is getting us into a lot of trouble. I tried to claim
it was an MVP, but the board aren't buying it. Whenever there are
concurrent connections, it either errors that it can't write to the
file, or sometimes overrides with an old count 💩

Quick, we need to use MariaDB instead 🙈

## 1. You'll Need a MariaDB Container

```sql
# You can mount SQL files into:
#   /some-dir:/docker-entrypoint-initdb.d
#
# You can also mount this as read-only:
#   /some-dir:/docker-entry-initdb.d:ro
#
CREATE TABLE views (
    id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    timestamp TIMESTAMP
)
```

## 2. You'll Need to Enable the Driver in your PHP Container

```shell
# Enabling MySQL Driver
docker-php-ext-install pdo_mysql
```

## 3. Code

```php
# main.php
<?php
declare(strict_types=1);

define("MYSQL_HOST", $_ENV["MYSQL_HOST"] ?: "mysql");
define("MYSQL_USER", $_ENV["MYSQL_HOST"] ?: "root");
define("MYSQL_PASS", $_ENV["MYSQL_PASS"] ?: "root");
define("MYSQL_DB", $_ENV["MYSQL_DB"] ?: "views");

try {
    $mysqlConnection = new PDO("mysql:host=" . MYSQL_HOST . ";dbname=" . MYSQL_DB, MYSQL_USER, MYSQL_PASS);
    $mysqlConnection->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch(PDOException $exception) {
    echo "<p>Hello! This super-secret project, served by a container. We're not sure how many views right now, but try again soon 😄</p>" . PHP_EOL;
    echo $exception->getMessage();
    exit(0);
}

$views = $mysqlConnection->query("SELECT count(*) FROM views")->fetchColumn();

echo "<p>Hello! This super-secret project, served by a container, now has ${views} views.</p>" . PHP_EOL;

$mysqlConnection->query("INSERT INTO views(timestamp) VALUES(NOW())");
```
