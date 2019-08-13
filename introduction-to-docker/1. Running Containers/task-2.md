# Docker Essentials: Task Two

Our super-secret project is blowing up 💥

Well, we think it is! We're not sure how many views we're
getting.

We're going to switch to PHP and write to a file every time
someone views our secret-project!

Awesome-sauce 💯

```php
# main.php
<?php
declare(strict_types=1);

define("DATA_FILE", $_ENV["DATA_FILE"] ?: "/data/views.json");
define("DEFAULT_DATA", ["views" => 0]);

if (false === file_exists(DATA_FILE)) {
    $fileHandle = fopen(DATA_FILE, "w") or die("Cannot write to data file!");

    fwrite($fileHandle, json_encode(DEFAULT_DATA));
    fclose($fileHandle);
}

$data = json_decode(file_get_contents("/data/views.json"));

$views = $data->views + 1;

echo "<p>Hello! This super-secret project, served by a container, now has ${views} views.</p>" . PHP_EOL;

$fileHandle = fopen(DATA_FILE, "w") or die("Cannot write to data file!");
fwrite($fileHandle, json_encode(["views" => $views]));
fclose($fileHandle);
```
