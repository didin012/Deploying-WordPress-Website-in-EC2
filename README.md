# WordPress-Website-in-EC2

## On this project you will be able to:
1.	Create an EC2 instance in AWS
2.	Access the instance via SSH
3.	Utilize some Unix commands
4.	Create a Wordpress site

## Hosting Wordpress Website in EC2

1.	Install Apache webserver<br>
```$ sudo apt install apache```
2.	Install PHP runtime<br>
```$ sudo apt install php libapache2-mod-php php-mysql```
3.	Install mysql server<br>
```$ sudo apt-get update```<br>
```$ sudo apt install mysql-server```
4.	Login to mysql to change auth plugin to native password<br>
```$ sudo mysql -u root```<br>
```ALTER USER ‘root’@localhost IDENTIFIED WITH my_sql_native_password BY ‘<yourpassword>’;```<br>
```CREATE USER ‘<your user>’@localhost IDENTIFIED BY ‘<yourpassword>’;```
5.	Create Database inside mysqlserver and grant privileges on on it.<br>
```$ CREATE DATABASE <db_name>;```<br>
```$ GRANT ALL PRIVILEGES ON <db name>.* TO ‘<your_username>’@localhost;```
6.	Go to Downloads in Wordpress and copy the download link for the tar.gz file then download it into our instance.<br>
```$ wget <insert link>```
7.	Unzip it<br>
```$ tar -xvf <filename>```
8.	Move it into /var/www/html/<br>
```$ mv wordpress/ /var/www/html/```
