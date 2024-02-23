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
9.	Open a browser then access your website<br>
<instance’s IP>/wordpress

![image](https://github.com/didin012/WordPress-Website-in-EC2/assets/104528282/e5bcfea6-9a6f-4067-bcfc-cd94d00942ad)

10.	Click **Lets go** then enter the following credentials based on what you have input earlier.
11.	After proceeding you’ll get an error in the screen, copy the text then go to the terminal and create a file inside ```/var/www/html/```.

![image](https://github.com/didin012/WordPress-Website-in-EC2/assets/104528282/f8e47ce8-6f14-4946-9874-d2aa8763afcd)

```$ cd /var/www/html/can```<br>
```$ sudo vim wp-config.php```<br>

**[COPY CONTENTS]**
Run the vim command to save: ```:wq```
12.	Proceed to run installation, enter your required details on the next screen.
13.	After filling up the details, login to Wordpress

### You have successfully logged on to your Wordpress site

## OPTIONAL
14.	Remove ```/wordpress``` in your link to make it standalone to your IP address, on terminal type this:<br>
```$ cd /etc/apache2/sites-available/```<br>
```$ sudo vim 000-default.conf```
15.	Add the ```/wordpress``` on the ```DocumentRoot```

![image](https://github.com/didin012/WordPress-Website-in-EC2/assets/104528282/d079379c-b84b-46db-8a76-d44bcd49d7fd)
Run the vim command to save: ```:wq```

16.	Restart Apache2 <br>
```$ sudo systemctl restart apache2```
17.	Type in your bare IP address in the search bar of any web browsers.

![image](https://github.com/didin012/WordPress-Website-in-EC2/assets/104528282/8b6bb9e0-6d6a-4b53-b26c-12d322c7e1de)

### You have successfully deployed a WordPress website using EC2 instance



