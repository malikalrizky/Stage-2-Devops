# Day 1 Stage 2

# Manage Server and Backend

## Install and setup mysql server

![](/media/day2/Screenshot%20(28).png)

When trying to secure install mysql there's some error

https://www.tecmint.com/install-mysql-8-in-ubuntu/

![](/media/day2/Capture.JPG)

![](/media/day2/Screenshot%20(30).png)

![](/media/day2/Screenshot%20(33).png)

![](/media/day2/Screenshot%20(34).png)

There's also [another way](https://www.tecmint.com/install-mysql-8-in-ubuntu/) 

![](/media/day2/mysql1.png)

Create new user and create database

![](/media/day2/Screenshot%20(41).png)

Change database config bind address to `0.0.0.0` so it could be accessed from all traffic

![](/media/day2/Screenshot%20(53).png)

![](/media/day2/Screenshot%20(54).png)

![](/media/day2/Screenshot%20(56).png)

### Setup Backend Server and Integration to Database

Install the app like usual

![](/media/day2/Screenshot%20(90).png)

![](/media/day2/Screenshot%20(93).png)

Install sequelize-cli to integrate and migrating database

`Sequelize is an ORM (Object Relational Mapper) for Node. js. Sequelize lets us connect to a database and perform operations without writing raw SQL queries. It abstracts SQL queries and makes it easier to interact with database models as objects.`

![](/media/day2/Screenshot%20(96).png)

Before migrating change the configuration first

![](/media/day2/Screenshot%20(97).png)

Change the configuration in the Development section;

user: mysql user
password: mysql password
database: mysql database
host: database server

![](/media/day2/Screenshot%20(98).png)

![](/media/day2/Screenshot%20(99).png)

Migrating data from backend server to database server

```
npx sequelize db:migrate
```

![](/media/day2/Screenshot%20(101).png)

Check if the data migrating is success

![](/media/day2/Screenshot%20(102).png)

Start the app and then check if the app is running using IP:port

![](/media/day2/Screenshot%20(103).png)

![](/media/day2/Screenshot%20(104).png)

### Integrating Backend and Database with Frontend App

Open `api.js` in the frontend app and change the baseURL into backend api DNS that has been created

![](/media/day2/Screenshot%20(129).png)

Setup the backend reverse proxy and multilevel domain

![](/media/day2/Screenshot%20(128).png)

Try to access the web server and register

![](/media/day2/Screenshot%20(122).png)

![](/media/day2/Screenshot%20(123).png)

![](/media/day2/Screenshot%20(124).png)

### Setup SSL using CertBot and CloudFlare API Token

Open cloudflare and copy the API Key into a new file

![](/media/certbot/Screenshot%20(105).png)

![](/media/certbot/Screenshot%20(106).png)

![](/media/certbot/Screenshot%20(107).png)

Make sure to give the user a read permission for the file

![](/media/certbot/Screenshot%20(108).png)

Install and setup CertBot with Cloudflare

![](/media/certbot/Screenshot%20(125).png)

![](/media/certbot/Screenshot%20(126).png)

Check the certificate

![](/media/certbot/Screenshot%20(121).png)