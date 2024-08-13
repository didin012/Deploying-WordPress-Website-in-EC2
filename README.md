# WordPress Website Deployment in EC2

## Infrastructure

![image](https://github.com/didin012/Deploying-WordPress-Website-in-EC2/assets/104528282/7d5392c8-6a3d-41db-90b8-fdc17b985a53)

This project revolves on deploying a WordPress website on an EC2 instance and utilizing the use of CLI for installation. It involves launching an instance, connecting to it via SSH, installing a LAMP stack (Linux, Apache, MySQL, PHP), configuring MySQL, downloading and setting up WordPress files in the Apache document root, completing the WordPress installation through a web browser. There is a slight additional configuration based on specific needs, but this process provides a solid foundation for hosting a WordPress site on AWS.

## On this project you will be able to:
1.	Create an EC2 instance in AWS
2.	Access the instance via SSH
3.	Utilize some Unix commands
4.	Create a Wordpress site

## Launch an EC2 instance
1. Put and select the following configurations provided on the image below.

![image](https://github.com/didin012/Deploying-WordPress-Website-in-EC2/assets/104528282/575b506f-7c16-447f-9551-3fc7fd1158f6)
![image](https://github.com/didin012/Deploying-WordPress-Website-in-EC2/assets/104528282/b23af33c-d28c-4201-93d2-8de3f63dddd4)
![image](https://github.com/didin012/Deploying-WordPress-Website-in-EC2/assets/104528282/242cdf64-58d5-4992-acd5-b646ba70c843)

2. Before Launching the instance make sure to create your own keypair

![image](https://github.com/didin012/Deploying-WordPress-Website-in-EC2/assets/104528282/32d70c5b-efa6-4881-86d0-1f01ce229053)

3. Store this PEM file on your local directory (mine is stored in Documents since I'm using Ubuntu). You will need this to access your instance via SSH
4. Click **Launch Instance** then wait for your instance to run
   
## Associating Elastic IP to your instance
You will need to associate an Elastic IP to your instance so that whenever you restart your instance, the IP will not change and stays the same as previously.
1. Go to EC2 Dashboard
2. Click on Elastic IPs

![image](https://github.com/didin012/Deploying-WordPress-Website-in-EC2/assets/104528282/32e43700-ece3-4502-a4dd-e3b0a43a946e)

3. Click **Allocate Elastic IP Address**
4. Click on **Allocate**
5. On Elastic IPs lists, click on your newly created EIP
6. Click on **Associate EIP**
7. Choose the correct EC2 instance where the WordPress will run
8. Click **Associate**

![image](https://github.com/didin012/Deploying-WordPress-Website-in-EC2/assets/104528282/267bde3d-318f-4dcd-9335-eb3a23cb5c0f)

## Accessing Ubuntu EC2 instance to our CLI
1. Make sure your command line is in the directory on where the PEM key is stored, if not type in this:<br>
````
$ cd <directory>
````
The directory can be /Documents/mykeys/
3. If you are on the directory, type in this command<br>
````
$ ssh -i <keypair_filename> ubuntu@<assigned_elastic_IP_address>
````
the <assigned_elastic_IP_address> can be found on the EC2 instance PublicIPv4 Address

## Hosting Wordpress Website in EC2

1.	Install Apache webserver<br>
````
$ sudo apt install apache
````
2.	Install PHP runtime<br>
````
$ sudo apt install php libapache2-mod-php php-mysql
````
4.	Install mysql server<br>
````
$ sudo apt-get update
$ sudo apt install mysql-server
````
6.	Login to mysql to change auth plugin to native password<br>
````
$ sudo mysql -u root
ALTER USER ‘root’@localhost IDENTIFIED WITH my_sql_native_password BY ‘<yourpassword>’;
CREATE USER ‘<your user>’@localhost IDENTIFIED BY ‘<yourpassword>’;
````
7.	Create Database inside mysqlserver and grant privileges on on it.<br>
````
$ CREATE DATABASE <db_name>;
$ GRANT ALL PRIVILEGES ON <db name>.* TO ‘<your_username>’@localhost;
````
9.	Go to Downloads in Wordpress and copy the download link for the tar.gz file then download it into our instance.<br>
````
$ wget <insert link>
````
11.	Unzip it<br>
````
$ tar -xvf <filename>
````
13.	Move it into /var/www/html/<br>
````
$ mv wordpress/ /var/www/html/
````
15.	Open a browser then access your website<br>
<instance’s IP>/wordpress

![image](https://github.com/didin012/WordPress-Website-in-EC2/assets/104528282/e5bcfea6-9a6f-4067-bcfc-cd94d00942ad)

10.	Click **Lets go** then enter the following credentials based on what you have input earlier.
11.	After proceeding you’ll get an error in the screen, copy the text then go to the terminal and create a file inside ```/var/www/html/```.

![image](https://github.com/didin012/WordPress-Website-in-EC2/assets/104528282/f8e47ce8-6f14-4946-9874-d2aa8763afcd)

````
$ cd /var/www/html/can
$ sudo vim wp-config.php
````

**[COPY CONTENTS]**<br>
Run the vim command to save: ```:wq```<br>
12.	Proceed to run installation, enter your required details on the next screen.<br>
13.	After filling up the details, login to Wordpress

### You have successfully logged on to your Wordpress site

## OPTIONAL
14.	Remove ```/wordpress``` in your link to make it standalone to your IP address, on terminal type this:<br>
````
$ cd /etc/apache2/sites-available/
$ sudo vim 000-default.conf
````
15.	Add the ```/wordpress``` on the ```DocumentRoot```

![image](https://github.com/didin012/WordPress-Website-in-EC2/assets/104528282/d079379c-b84b-46db-8a76-d44bcd49d7fd)<br>
Run the vim command to save: ```:wq```

16.	Restart Apache2 <br>
````
$ sudo systemctl restart apache2
````
18.	Type in your bare IP address in the search bar of any web browsers.

![image](https://github.com/didin012/WordPress-Website-in-EC2/assets/104528282/8b6bb9e0-6d6a-4b53-b26c-12d322c7e1de)

### You have successfully deployed a WordPress website using EC2 instance

## Cleaning Up
1. Select your instance in the **Instances** section then click **Actions** and Terminate Instance

![image](https://github.com/didin012/Deploying-WordPress-Website-in-EC2/assets/104528282/419cf1a3-702b-4317-8720-18b7c9432dbe)

2. Disassociate your Elastic IP address and release it 

![image](https://github.com/didin012/Deploying-WordPress-Website-in-EC2/assets/104528282/926c017e-93da-4d9e-9869-9f0181009dea)
