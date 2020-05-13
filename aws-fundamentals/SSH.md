# SSH Into Amazon Linux EC2

## Linux/MAC
chmod 0400 [location of key file] 

ssh -i [location of key file] ec2-user@[IPv4 public IP]

## Windows 10

ssh -i [location of key file] ec2-user@[IPv4 public IP]

#### UNPROTECTED PRIVATE KEY FILE Fix
    * right click on key file
    * click on security
    * click on advanced tab
    * make sure owner of key is yourself
    * disable inheritance
    * remove all other users besides yourself