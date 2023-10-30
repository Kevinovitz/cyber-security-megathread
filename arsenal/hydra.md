# Hydra X
% bruteforce, access

## HTTP/HTTPS - port 80/430 using 4 threads
#plateform/linux #target/remote #protocol/http #port/80 #cat/ATTACK/BRUTEFORCE-SPRAY 
```bash
hydra -l <username> -P <passlist> <ip> -t 4
```
## FTP - port 21 using 4 threads
#plateform/linux #target/remote #protocol/ftp #port/21 #cat/ATTACK/BRUTEFORCE-SPRAY 
```bash
hydra -l <username> -P <passlist> ftp://<ip> -t 4
```
## SSH - port 22 using 4 threads
#plateform/linux #target/remote #protocol/ssh #port/22 #cat/ATTACK/BRUTEFORCE-SPRAY 
```bash
hydra -l <username> -P <passlist> <ip> ssh -t 4
```
## Webform - POST/GET - use field values
#plateform/linux #target/remote #protocol/webform #cat/ATTACK/BRUTEFORCE-SPRAY 
```bash
hydra -l <username> -P <passlist> <ip> http-post-form "/<loginpage>:<username_field_value>=^USER^&<password_field_value>=^PASS^&<button_name>=<button_value>:F=<incorrect_string>" -t 4
```
## SMTP/SMTPS - port 587 using 4 threads
#plateform/linux #target/remote #protocol/smtp #port/587 #cat/ATTACK/BRUTEFORCE-SPRAY 
```bash
hydra -l <email> -P <passlist> smtp://<ip> -s <port> -t 4	
```

= userlist: users.txt
= passlist: /usr/share/wordlists/rockyou.txt
