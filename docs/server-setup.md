# Ichi server setup

# Add user and give root permissions

```
adduser username
usermod -aG sudo usernam
```

# generate ssh keys and ajust sshd config

```
#open ssh config file

vi /etc/ssh/sshd_config

#search for Port
#change to your preference ex:Port 34567 (make sure to remember it)
#search for PubKeyAuthentication on /etc/ssh/sshd_config/ and remove the # and set it to yes if it says no.
```
**On your host**
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
**On the server**
```
ssh-keygen -t rsa
cd
cat id_rsa.pub >> .ssh/authorized_keys
```
From your host you can now simply ssh passwordlessly:
```
ssh alias
```


Finally disable ssh root login
```
#open ssh config file

vi /etc/ssh/sshd_config

# search for PermitRootLogin, remove the # if its commented and change it from Yes to No
```

# Configuring Firewall

Enabling UFW (firewall), allow SSH connections, installing fail2ban

```
ufw default deny incoming
ufw default allow outgoing
apt install fail2ban
cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
ufw allow 34567 (this is assuming you’re using port 34567, replace ssh with another port if you used another port)
ufw enable
vi /etc/fail2ban/jail.local
```
in **/etc/fail2ban/jail.local** Search for ssh and erase the # in front of [sshd] and enabled = true below it

# Install docker.io

Set up the repository
```
#update the apt package index:

apt update

#install packages to allow apt to use a repository over HTTPS:

apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```
Add Docker’s official GPG key
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
Set up the stable repository
```
add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

Install docker
```
apt update
apt install docker-ce
```
Verify that Docker CE is installed correctly by running the hello-world image.
```
docker run hello-world
```
Add user to docker group
```
usermod -aG docker username
```
