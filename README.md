# n8n 
![Typing SVG](https://readme-typing-svg.herokuapp.com?color=%FF00000&lines=Розгортання+N8N+на+localhost+з+HTTPS)

![Cent OS](https://img.shields.io/badge/cent%20os-002260?style=for-the-badge&logo=centos&logoColor=F0F0F0)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=for-the-badge&logo=Cloudflare&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)

На VirtualBox встановив CentOS 9 з Docker. Налаштував HTTPS для n8n через тунель Cloudflare, щоб уникнути "Telegram Trigger: Bad Request: bad webhook: An HTTPS URL must be provided for webhook".

# CentOS 9 Stream
https://mirror.stream.centos.org/9-stream/BaseOS/x86_64/iso/

CentOS-Stream-9-latest-x86_64-boot.iso (1.2 GiB) 

Після встановлення Minimal – 1.7Gb

------------------------------------------------------------------------------

# VirtualBox 
https://www.virtualbox.org
### в Мережа змінити з NAT на "Проміжний адаптер" і вибрати фізичну карту
------------------------------------------------------------------------------
ip -br a

nmtui
- 192.168.0.8
- 192.168.0.1
------------------------------------------------------------------------------

sudo systemctl status sshd

### Далі вся взаемодія з CentOS 9 через PuTTY 
https://www.putty.org

------------------------------------------------------------------------------
## При налаштуванні не під root може бути таке сповіщення "vkm немає у файлі sudoers."

### Якщо у вас є доступ до root-користувача, увійдіть у систему:

su -

usermod -aG wheel vkm

------------------------------------------------------------------------------

# DOCKER INSTALL 
https://docs.docker.com/engine/install/centos/#install-using-the-repository

## Set up the repository
sudo dnf -y install dnf-plugins-core

sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

## Install Docker Engine
### 1. Install the Docker packages.
sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

Загальний обсяг отримання: 107 M     Розмір після встановлення: 426 M

### 2. Start Docker Engine.
sudo systemctl enable --now docker

sudo docker version

sudo docker compose version

sudo docker run hello-world

------------------------------------------------------------------------------

# N8N 

## Створити папки:
mkdir -p ./n8n && cd ./n8n && mkdir -p ./n8n_data

### Створити файл зі змінними
nano .env

### Створити файл розгортання N8N
nano docker-compose.yml  

### Розгорнути N8N
sudo docker compose up -d

### для зупинки N8N
sudo docker compose down

-----------------------------------------------------------------------------
## Cloudflare Networks/ Tunnels (Status=HEALTHY)
https://one.dash.cloudflare.com/7db9c7b5293af7b77182c60d7a5fa332/networks/tunnels
### Overview
- Install and run a connector (your_TOKEN)
### Public Hostname 
- Domain = your_domain
- Service = http://n8n:5678

## DNS Records
- Type = CINAME
- Name = your_domain
- Target = Tunnel ID.cfargotunnel.com


-----------------------------------------------------------------------------
# Посилання 
- безкоштовний домен
https://nic.ua/uk/my/domains
- Cloudflare
https://dash.cloudflare.com
- Віддалений доступ до сервера розумного будинку Home Assistant. Keenetic чи тунель Cloudflare?
https://youtu.be/WKNmMcLRhvs?t=341
- По цьому зразку зробив свій
https://github.com/n8n-io/n8n-docker-caddy

