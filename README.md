# Hydra

Syntax
hydra username password options service://server:port

Example:
hydra -l user -P passlist.txt ftp://192.168.0.1:2221

Options
-l - single username
-L - username List
-p - single password
-P - password List
-V - Show output on screen
-t - tasks(threads)
-o - output file
-m - module options
-f - stop when password is found(otherwise it will carry on)


Password options
Use -e
s --> use username as password
n --> try an empty password
r --> reverse the username and use as password

## Hydra For SSH service

* with username and password list
``` hydra ssh://192.168.1.1:2222 -L ./users.txt -P ./password.txt -V -f```

* with one username and password list
``` hydra ssh://192.168.1.1:2222 -l admin -P ./password.txt -V -f```

* with reducing thread to bypass firewall
``` hydra ssh://192.168.1.1:2222 -l admin -P ./password.txt -V -f -t 2```

## Hydra For MYSQL service

* with username and password list and save in file
``` hydra mysql://127.0.0.1 -l root -P ./password.txt -V -f -o pass_cracked.txt``` 

## Hydra For FTP service

* with username and null password
```hydra ftp://192.168.1.1 -l anonymous -e n ```

## Login page 

```hydra 192.168.0.1 http-post-form "/:userName=^USER^&mypass=^PASS^&loginBtn=Submit:The username or password is incorrect, please input again" -L ./users.txt -P ./passwords.txt -V -f ```


userName : It is name of username form field
mypass   : It is name of password form field
loginBtn : Btn Field name
Message after semicolon is message which indicates login failed





# John the ripper

* When Hash and format is given
```john hash.txt --format=RAW-MD5```

* For single mode with following hash type
username:hash::::
```john --single hash.txt --format=RAW-MD5 ```

* using wordlist 
``` john --wordlist-word.txt a2.txt --format=Raw-SHA1```

* using rules like ShiftToogle (change upper to lowercase and viceversa)

``` john --rules=ShiftToggle xyz.txt --wordlist=word.txt```


* For cracking the shadow file
	- First unshadow the file(combine shadow file and passwd file)
		```sudo unshadow /etc/passwd /etc/shadow```

* For example we copied the hash retrived after unshadow of root 
and saved in document in xyz.txt

``` john xyz.txt --wordlist=rockyou.txt```
```john --show xyz.txt```

* Cracking the zip file
```zip2john xyz.zip > ziphash.txt```
```john ziphash.txt --wordlist=/opt/rockyou.txt```






