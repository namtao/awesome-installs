# Ubuntu Software Setup

This repository provides **ready-to-use installation commands** for popular software on Ubuntu.  
Just copy and paste into your terminal.  

---

## Table of Contents

- [Ubuntu Software Setup](#ubuntu-software-setup)
  - [Table of Contents](#table-of-contents)
  - [Set Timezone](#set-timezone)
  - [Ngrok](#ngrok)
  - [Docker](#docker)
  - [Git](#git)
  - [Anaconda](#anaconda)
  - [Portainer](#portainer)
  - [Cockpit](#cockpit)
  - [OpenSSL](#openssl)

---

## Set Timezone

**About:** Setting the correct timezone ensures that your system's time is accurate for your location.

```bash
sudo timedatectl set-timezone Asia/Ho_Chi_Minh
timedatectl
```

## Ngrok

**About:** Ngrok is a tool that allows you to expose a local server to the internet securely.

```bash
sudo snap install ngrok
ngrok config add-authtoken <YOUR_AUTHTOKEN>
ngrok http 5000

nohup ngrok http 5000 > ngrok.log 2>&1 &
tail -f ngrok.log
ps aux | grep ngrok
kill -9 <PID>
```

## Docker

**About:** Docker allows you to build, run, and manage applications inside containers.
It is recommended to re-login or reboot after installation.

```bash
sudo apt update
sudo apt install ca-certificates curl gnupg -y

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

docker --version
```

## Git

**About:** Git is a distributed version control system used for tracking changes in source code during software development.

```bash
sudo apt update
sudo apt install git -y
git --version

ls -al ~/.ssh
ssh-keygen -t ed25519 -C "your_email@example.com"

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

ssh-add -l
cat ~/.ssh/id_ed25519.pub
Settings → SSH and GPG keys → New SSH key

ssh -T git@github.com
git clone git@github.com:nam/test.git
```

## Anaconda

**About:** Anaconda is a popular distribution of Python and R for scientific computing and data science.

```bash
cd /tmp
wget https://repo.anaconda.com/archive/Anaconda3-2024.10-1-Linux-x86_64.sh
bash Anaconda3-2024.10-1-Linux-x86_64.sh
echo 'export PATH=~/anaconda3/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
conda --version
```

## Portainer

**About:** Portainer is a lightweight management UI that allows you to easily manage your Docker environments.

```bash
sudo docker volume create portainer_data
sudo docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

## Cockpit

**About:** Cockpit is a web-based graphical interface for servers, making it easy to manage and monitor your system.

```bash
sudo apt install cockpit
sudo systemctl enable --now cockpit.socket
sudo ufw allow 9090/tcp
```

## OpenSSL

**About:** OpenSSL is a robust, full-featured open-source toolkit implementing the Secure Sockets Layer (SSL) and Transport Layer Security (TLS) protocols.

```bash
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
```
