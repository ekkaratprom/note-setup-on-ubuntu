## [Install Jenkins](https://www.jenkins.io/doc/book/installing/#debianubuntu)

```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt install default-jdk
sudo apt-get install jenkins
```

Install nodejs and npm
```
curl -sL https://deb.nodesource.com/setup_10.x -o nodesource_setup.sh
sudo bash nodesource_setup.sh
sudo apt-get install -y nodejs

npm install -g @angular/cli
```

Start Jenkins server
```
sudo systemctl start jenkins
sudo systemctl status jenkins

sudo ufw allow 8080
sudo ufw allow 22
sudo ufw status

http://your_server_ip_or_domain:8080
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```


## Fronend with NGINX

```
sudo apt update
sudo apt install nginx

sudo ufw app list
sudo ufw allow 'Nginx HTTP'
sudo ufw status

systemctl status nginx

http://your_server_ip


sudo systemctl stop nginx
sudo systemctl start nginx
sudo systemctl restart nginx
sudo systemctl reload nginx

sudo systemctl enable nginx
```

Step to build and deploy
```
cd frontend
npm install
ng build --prod


/etc/nginx/sites-available/default
/var/www/html

scp -r frontend/dist/my-app/* root@159.65.3.177:/var/www/html
```


Generate keys
```
su jenkins
whoami
/var/lib/jenkins/.ssh/
/var/lib/jenkins/.ssh/id_rsa.pub
```

## Backend with java

```
sudo apt-get update
sudo apt install default-jdk
```

Build and Deploy
```
cd backend
./gradlew bootJar


scp backend/build/libs/web_service-0.0.1-SNAPSHOT.jar root@<ip>:/root/demo.jar

```

## File :: /etc/systemd/system/helloworld.service
```
[Unit]
Description=Spring Boot HelloWorld
After=syslog.target
After=network.target[Service]
User=username
Type=simple

[Service]
ExecStart=/usr/bin/java -jar /root/demo.jar
Restart=always
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=helloworld

[Install]
WantedBy=multi-user.target
```

Start/Stop
```
sudo systemctl start helloworld
sudo systemctl status helloworld
```

https://www.linode.com/docs/development/java/how-to-deploy-spring-boot-applications-nginx-ubuntu-16-04/


## Install mongodb server
https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/

```
wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list

sudo apt-get update
sudo apt-get install -y mongodb-org

sudo systemctl start mongod
sudo systemctl daemon-reload
sudo systemctl status mongod
sudo systemctl restart mongod
```
