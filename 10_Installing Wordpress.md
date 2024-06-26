### How to Install Wordpress
After ssh into the ec2 as we did previously,we will now through the ec2 instance install wordpress and move the files to EFS
<br>
The purpose of moving the file to EFS is because EFS has high availability,so our data will be stored across multiple availability zones
<br>
Now lets begin the wordpress installation,type the below commands
```bash
sudo su
yum update -y
mkdir -p /var/www/html
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport <yourEfsMountHere>:/ /var/www/html
```
<br>
Now in last code above replace "yourEfsMountHere" with your EFS mount below 👇 I will show you how to get your EFS mount information
<br
### Create HTML Directory and mount EFS to it
<br>

To get your EFS mount information,in your AWS management console in your region,on the search bar type EFS,and click on your EFS to open it as shown below
![Installing_Wordpress1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/e5b81d79-4e2b-416d-b42d-cef4d5bc55bf)
<br>
![Installing_Wordpress2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/f6be8264-4a2a-4987-a9f6-896f241d4418)
<br>
next click on attach at the top right corner as shown below
![Installing_Wordpress3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/dd3136e7-d583-4049-b289-99e717134e5d)
<br>
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport <yourEfsMountHere>:/ /var/www/html
<br>
Under Using the NFS client,you will see your EFS mount information just,now all you need do is copy the EFS info up till backslash(/) symbol,then space /var/www/html,as illustrated
in code above
<br>
![Installing_wordpress4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/454aa852-d46b-419c-8cb1-7c33f19243cf)

Next is to copy the last mount code and paste it as last line on your terminal as shown above
<br>
To test if you have successfully mounted the EFS type "df -h" and should be able to see your mount EFS on the last line
<br>
*sudo su
yum update -y
mkdir -p /var/www/html
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport <yourEfsMountHere>:/ /var/www/html*
<br>
Now I think its important I explain above codes which I executed previously so that you have a feel of what is going on
<br>
*sudo su*-->This command will elevate the users permissions to administrative permission thereby making the user a root user
<br>
*yum update -y*-->This commsnd updates the packages in the ec2 instance to latest versions,the flag y command(-y) automatically answers yes to any prompt during the update process
<br>
*mkdir -p /var/www/html*--> This command will help to create a directory named var/www/html,the flag p(-p) indicates the creation of parent directory inside the directory,and  seems we will be installing apache server,the directory var/www/html will help to save the index files
<br>
*sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-096a3d3f272ac3543.efs.ap-southeast-1.amazonaws.com:/ /var/www/html*-->so basically this command mounts the EFS files system to the directory (/var/www/html) using the NFS protocol(that is files or directories can be shared over NFS network)
<br>
*nfsvers*=4.1--> This command specifies the NFS version 4.1
<br>
*rsize*=1048576--> This command sets the read buffer size to 1048576 bytes
<br>
*wsize*=1048576--> This command sets the write buffer to 1048576 bytes
<br>
*hard*--> This command sets the mount to "hard" so that it can authomatically retry indefinately incase of server or network issues
<br>
*timeo=600*-->this command sets the timeout for the NFS to 600seconds which is 10mints
<br>
*retrans=2*--> This command sets the number of retransmission to 2 which means the client will have to retry failed operations twice
<br>
*noresvport*-->This command allows the NFS client to use any available port for communication
<br>
*fs-096a3d3f272ac3543.efs.ap-southeast-1.amazonaws.com:/*--> This command specifies the DNS name of the filesytem and symbol :/ signifies the root directory to mount
<br>
It is important to note that in order to install the wordpress we will need the LAMP packages.
<br>
LAMP is acronym for Linux(operating system),Apache(Webserver),Mysql(Database) and PHP 7.4(Server-side scripting language)
<br>
### 2. Install Apache Server 
The Apache is an open source http webserver for delivering web content,another name for Apache is httpd
<br>
Now its time to install the apache server and below commands will be used
<br>

```bash
sudo yum install -y httpd httpd-tools mod_ssl

sudo systemctl status httpd 

sudo systemctl enable httpd

sudo systemctl start httpd
```
sudo yum install -y httpd httpd-tools mod_ssl --> This command installs the Apache server package and (httpd-tools) installs neccessary tools,(mod_ssl)ensures secure connection 
<br>
sudo systemctl status httpd --> This command is used to check the status of services in this its checking status for httpd
<br>
sudo systemctl enable httpd--> This command is used to enable the httpd to start authomatically at boot time
<br>
sudo systemctl start httpd--> This command is used to start the httpd service immediately.It initiates the Apache http server allowing it to handle incoming requests
<br>
![Installing_Wordpress5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/ab069ad0-8de5-4585-976a-9107191dd697)
<br>
After running all commands above,next run the command sudo systemctl status httpd to know if the httpd server is active as shown above
<br>

### 3. Install PHP 7.4
<br>
Now run below commands to install PHP 7.4
<br>

```bash
sudo amazon-linux-extras enable php7.4
sudo yum clean metadata
sudo yum install php php-common php-pear -y
sudo yum install php-{cgi,curl,mbstring,gd,mysqlnd,gettext,json,xml,fpm,intl,zip} -y
```
![Installing_wordpress6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/d5407efe-f9f4-466c-a82a-c7da4348990e)

![Installing_wordpress7](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/41f97513-ef42-46c6-b264-4aa56474a6b9)

![Installing_wordpress8](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/008b2f1f-bdda-430d-af72-f7dc8721cb13)

<br>

```bash
sudo amazon-linux-extras enable php7.4
sudo yum clean metadata
sudo yum install php php-common php-pear -y
sudo yum install php-{cgi,curl,mbstring,gd,mysqlnd,gettext,json,xml,fpm,intl,zip} -y
```
<br>

*sudo amazon-linux-extras enable php7.4* --> This command enables amazon linux extras for php7.4
<br>
*sudo yum clean metadata*-->This command cleans the local package metadata cache
<br>
*sudo yum install php php-common php-pear -y*-->This command installs php itself along with common php libraries,the flag y(-y) will help to authomatically respond yes to any prompts.
*sudo yum install php-{cgi,curl,mbstring,gd,mysqlnd,gettext,json,xml,fpm,intl,zip} -y*--> This command installs additional php extensions and modules
The extensions listed in the command include CGI (php-cgi), cURL (php-curl), Multibyte String (php-mbstring), GD Graphics Library (php-gd), MySQL Native Driver (php-mysqlnd), Gettext (php-gettext), JSON (php-json), XML (php-xml), FastCGI Process Manager (php-fpm), Internationalization (php-intl), and ZIP (php-zip)
<br>

### 4 Install MySQL 5.7
Now runn below commands

```bash
sudo rpm -Uvh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
sudo yum install mysql-community-server -y
sudo systemctl enable mysqld
sudo systemctl start mysqld
```
<br>

*sudo rpm -Uvh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm*-->This command installs the mysql community server  configuration package
*sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022*--> This command installs the GPG key used for sign to mysql packages,ensuring their authenticity.
*sudo yum install mysql-community-server -y*-->This command installs mysql community server package and the flag y(-y) will help to respond yes to any prompts
*sudo systemctl enable mysqld*--> This command enables the Mysql service to start authomatically whenever it boots.
*sudo systemctl start mysqld*-->This command help to start mysql service
<br>

###5. Set Permissions
```bash
sudo usermod -a -G apache ec2-user
sudo chown -R ec2-user:apache /var/www
sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
sudo find /var/www -type f -exec sudo chmod 0664 {} \;
sudo chown apache:apache -R /var/www/html
```
<br>

*sudo usermod -a -G apache ec2-user*--> This command will help to add the ec2-user to Apache group,this will enable the ec2-user to able to access files and directories owned by the Apache group
<br>
*sudo chown -R ec2-user:apache /var/www* -->This command changes the ownership of /var/www and its content to the ec2-user,thereby ensuring that the ec2-user have neccessary permissions to manage the files.The /var/www is a default root directory for storing web content in open source web servers like Apache
<br>
*sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;* --> This command sets the directory permissions of the root directory /var/www to 2775. The 2 at the begining ensures that the new files and directories inherit the group ownership and the 775 permissions grant read,write, and execute permissions to the owner and group
<br>
*sudo find /var/www -type f -exec sudo chmod 0664 {} \;* --> The command set the permissions of /var/www and its subdirectories to 0664.The
6 at the begining grants read and write permissions to the owner and group and grants read permissions to others.
<br>
*sudo chown apache:apache -R /var/www/html* --> This command changes the ownership and content of /var/www/html directory to Apache,this will ensure that the webserver now runnning as the Apache user has the neccessary permisions to read and serve web content.

### Download wordpress files
<br>

```bash
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
cp -r wordpress/* /var/www/html/
```
<br>
![Installing_wordpress9](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/b93f9b61-27e1-4a9e-adee-0c870d7b6a6e)

*wget https://wordpress.org/latest.tar.gz* --> wget is short form for world wide web get,this command  uses the wget tool to downlaod the latest version of wordpress in a compressed format(compressed tarball) from the official wordpress website.
<br>
*tar -xzf latest.tar.gz* --> This command decompressess the comprised file
<br>
*cp -r wordpress/* /var/www/html/* --> This command recursively (-r) copy all files from the extracted wordpress directory to the root directory of the webserver  (/var/www/html/)
<br>
Now after running all above commands,on terminal type ls and you will see wordpress folder and latest.tar.gz
<br>

### 7.Create the wp-config.php file
<br>

``` bash
cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php

```
<br>
 The above command is used to make a duplicate of of the wordpress sample configuration file(wp-config-sample.php) and rename it to wp-config.php.The purpose for creating a copy is to have the original sample file as a backup.To see the newly duplicated file,type the command ls wordpress/
 <br>
 
### 8.Edit The wp-config.php file
To complete this task you can choose to use the vim or nano text editor,I will be using the nano text editor,use below command
<br>
The below code will be used to open the nano text editor

```bash
nano /var/www/html/wp-config.php
```
![install_wordpress10](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/fa638e30-6f93-4b19-8004-8c445e84bda1)


After opening the nano text editor,keep pressing down until you see DB_NAME.Now in order to fill this part,you need your RDS credentials as seen above
<br>
![Install_wordpress11](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/c80ffe6b-c739-4122-aa47-296fe250bfda)

![Install_wordpress12](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/9c55c00a-8d08-46a3-9b02-dc801374d6ca)

You can get your RDS credentials by opening your RDS from the management console,in the search bar in your managemnet console type RDS,click your database to open it and below you will see different tabs,click on configuration tab,on the left part  you will see your DB name below,and your username is the master username,to see your host,click on connectivity & Security,you will see this under endpoint & port as seen above
<br>
The final step now is restart the webserver,command to restart the webserver is 

```bash
sudo systemctl restart httpd
```

### Login
![Install_wordpress13](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/6fd7bcdc-4f55-432c-906f-0cfe676dff7f)


This will be your first login into wordpress and to login  just copy your instance's "Public IPv4 address" again and paste it on your browser,you will see a wordpress welcome page, as seen above

<br>

![Install_wordpress14](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/41c688ac-7a18-4b18-85bc-d6a1f10a22a8)

![Install_wordpress15](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/3b122cc5-43fc-4521-834c-ad3318295ac9)

![Install_wordpress16](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/4c2b652f-fbb6-46b7-b53d-27cd84d95404)

![Install_wordpress16](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/446c76ad-bc85-4dd6-8bce-8c77ae1a6d60)

<br>
Once your wordpress is displayed ,you will now need to create and input your site title,username and password,then click install wordpress at the bottom left,next you will be prompted to input your username and password,after which you will be taken to your wordpress admin page as seen above
