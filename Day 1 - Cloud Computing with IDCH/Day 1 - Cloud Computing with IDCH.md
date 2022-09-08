# Day 1 Stage 2

# Cloud Computing with IdCloudHost

Cloud computing is the delivery of computing services including servers, storage, databases, networking, and software over the internet to offer faster innovation, flexible resources, and economies of scale.

# Create App in Server with IdCloudHost

1. Create virtual machine and choose the specification

![](/media/day1/1.png)

note: Make sure to check the public ip option to make it publicly accessed

![](/media/day1/2.png)

Floating IP: a public, static IP address for instances created only in a private subnet (that is, without a public network interface)

VPC network: a Virtual Private Cloud network is a service that is completely controlled by a single organization and not shared with others (usually a secret data). To connect with VPC we must use VPN.

![](/media/day1/3.png)

The virtual machine will build automatically by IDCloudHost

![](/media/day1/Screenshot%20(51).png)

Create a virtual host name using IP address from IDCH

### Create and setup ssh

Generate ssh-keygen

![](/media/day1/Screenshot%20(60).png)

![](/media/day1/Screenshot%20(61).png)

Send ssh-keygen to every server

![](/media/day1/Screenshot%20(63).png)

Copy the public key into authorized_keys

![](/media/day1/Screenshot%20(64).png)

Try the ssh-key

![](/media/day1/Screenshot%20(66).png)

Connect and remote between server

![](/media/day1/Screenshot%20(67).png)

### Install the App and PM2

Install nvm and pm2 first if there's none

![](/media/day1/Screenshot%20(72).png)

Install the app

![](/media/day1/Screenshot%20(73).png)

Create file ecosystem

![](/media/day1/Screenshot%20(75).png)

Edit the file ecosystem script to `npm start`

![](/media/day1/Screenshot%20(76).png)

Start the app

![](/media/day1/Screenshot%20(77).png)

Try open the app using IP:port

![](/media/day1/Screenshot%20(78).png)

### Setup DNS Cloudflare and Reverse Proxy Nginx

Open DNS tab, add new DNS and insert IP address 

![](/media/day1/Screenshot%20(81).png)

Create reverse proxy config

![](/media/day1/Screenshot%20(83).png)

![](/media/day1/Screenshot%20(84).png)

![](/media/day1/Screenshot%20(85).png)

Try open the app using DNS

![](/media/day1/Screenshot%20(86).png)