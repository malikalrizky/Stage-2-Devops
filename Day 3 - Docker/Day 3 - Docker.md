# Day 3

# Docker

## Buat Script Untuk Instalasi Docker Secara Otomatis

```
#!/bin/bash

sudo apt-get -y update

sudo apt-get -y install \ ca-certificates \ curl \ gnupg \ lsb-release \ apt-transport-https \ software-properties-common

sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get -y update

sudo apt-get -y install docker-ce docker-ce-cli containerd.io docker-compose-plugin

docker -v
```

## Frontend App in Docker

### Clone aplikasi lalu buat file bernama Dockerfile pada folder aplikasi dan masukkan konfigurasi di bawah ini

```
FROM node:[version]
WORKDIR [directory]
COPY . .
RUN npm install
EXPOSE 3000
CMD [ "npm", "start" ]
```

![](/media/day3/1.png)

![](/media/day3/2.png)

### Jalankan perintah build untuk melakukan build Dockerfile yang telah dibuat agar dapat menjadi Docker Images.

![](/media/day3/3.png)

![](/media/day3/4.png)

### Push images yang ada di local ke dalam server di Dockerhub/docker registry.

![](/media/day3/5.png)

![](/media/day3/11.png)

### Buat Docker Container

```
docker container create --name (name) -p (custom-port):(application-port) (images):(tag)
```

![](/media/day3/8.png)

### Jalankan Docker Container

docker container start (name)

![](/media/day3/9.png)

### Buat file bernama docker-compose.yaml

```
version: '3.8'
services:
 frontend:
   build: .
   container_name: dumbways-frontend
   image: malikalrk/dumbways-fe:1.0
   stdin_open: true
   ports:
    - 3000:3000
```

![](/media/day3/10.png)

![](/media/day3/15.png)

### Jalankan docker compose yang telah dibuat

![](/media/day3/12.png)

### Integrasikan Frontend dan Backend

Edit file API

![](/media/day3/6.png)

### Coba Akses Aplikasi pada Web

![](/media/day3/13.png)
