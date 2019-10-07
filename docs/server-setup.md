# Setup server ubuntu 19.04

# Add user
```adduser username```

# Give root permissions
```usermod -aG sudo username```

# Ajust sshd config
```
#open ssh config file

vi /etc/ssh/sshd_config

#search for Port
#change to your preference ex:Port 34567 (make sure to remember it)
#search for PubKeyAuthentication on /etc/ssh/sshd_config/ and remove the # and set it to yes if it says no.
```
# generate ssh keys
On your host

Edit .ssh/config and add this section:
```
Host alias
	Hostname ip adress
	User username
	Port 34567
```
```
ssh-keygen -t rsa
cd
scp .ssh/id_rsa.pub username@hostname:
```
On the server
```
ssh-keygen -t rsa
cd
cat id_rsa.pub >> .ssh/authorized_keys
```


