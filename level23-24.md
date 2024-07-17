# Level 23 -> Level 24

http://natas23.natas.labs.overthewire.org/?passwd=11iloveyou

```
if(strstr($_REQUEST["passwd"],"iloveyou") && ($_REQUEST["passwd"] > 10 )){
            echo "<br>The credentials for the next level are:<br>";
            echo "<pre>Username: natas24 Password: <censored></pre>";
        }
```

from analysing the code above we can understand why the **11iloveyou** value works  

strstr("11iloveyou", "iloveyou") -> 11  

then this 11 is comapred to check if it is greater than 10  

