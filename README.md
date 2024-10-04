

# How to install
```
$ git clone ....
```

# How to run via docker compose

```
$ cd php/clouded-php/lamp
docker-compose up -d
```

# How to run single php container
```
$ cd clouded-php
$ docker build -t my-php-app .
$ docker run -d -p 8080:80  -v ./src:/var/www/html/ --name my-running-app my-php-app


# query localhost on port 8080
$ curl localhost:8080
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PHP - Hello, World!</title>
</head>
<body>
        <h1>Hello, World!</h1>
</body>
</html>

```


# Content Example
Random php project, for example - https://github.com/thegr8dev/doctorpatientportal

requirements - LAMP, see docker-compose steps above.

```
# 1. Populate www directory in lamp -
$ git clone https://github.com/thegr8dev/doctorpatientportal.git
$ cp doctorpatientportal lamp/www/doctors-portal

# 2. Configure DB connection -
# 2.a get mariaDB container IP address
$ docker inspect lamp-mariadb-1 | grep IPAddress

# 2.b edit DB connection details to point to mysql/mariaDB running instance
$ vi lamp/www/doctors-portal/includes/conn.php
#     $server_name="<xx.yy.zz.ww>";
#     $server_name="172.18.0.2";    # Example

# 3. populate db
$ docker exec -i lamp-mariadb-1 mysql -u root -p<<*****>> < lamp/www/doctors-portal/sqlfiles/dpp.sql

# 4. Enjoy
$ curl -I localhost:80/doctors-portal/index.php
```


### References
https://www.php.net/manual/en/tutorial.requirements.php

https://linuxiac.com/how-to-set-up-lamp-stack-with-docker-compose/
